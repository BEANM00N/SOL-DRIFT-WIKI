## Overview

Measuring the performance of your particles gives you concrete areas to focus your efforts when optimizing. It’s important to verify assumptions before making changes, so you don’t mistakenly optimize where it's not needed, and so you can have a point of comparison to show how much of an impact your changes had.

This document will go over some of the tools Unreal provides for measuring the performance of Niagara particle systems, how to read them and make decisions based on their data.

## Measuring Performance

### Unreal Insights - Measuring Systems in a Level

Capturing a window of representative gameplay, ideally the actual game itself, provides the best data to work with. What may be true for one project does not always hold true for another, or even from level to level within the same project. For example a cutscene with a controlled camera may have the budget to run a 3D fluid sim that would otherwise be too costly to run during normal gameplay.

This also shows a holistic view of your particle systems as they interact with your project. A particle system that is within budget on its own, may take too many resources if dozens of instances are spawned in a short period of time. Even if their spawning is spread out, ticking instances that are off screen will take unnecessary resources.

Unreal Insights will profile your project and show you the timing of engine systems within a frame and the overall timing of a single frame. This allows you to look for spikes in your project’s frame times and dive into what systems are contributing to the slow-down and by how much. With the proper set-up you can pinpoint the specific Niagara systems at play too.

###### Documentation & Tutorials

- [Unreal Insights](https://docs.unrealengine.com/5.3/en-US/unreal-insights-in-unreal-engine)

#### Setting up Insights to get detailed Niagara captures

By default the asset name and some function calls are not included in the Unreal Insights trace. Adding **-StatNamedEvents** to your command line arguments will allow insights to capture these events. There is overhead to capturing these names, so it's best to only use it for finding where the bottlenecks are, then capturing without named events to get representative timings.

The example measurements in this doc were taken from a packaged Lyra game with the Development configuration and the LyraGame target in the Elimination game mode with bots.

Once you have an Insights capture you can use these Niagara timers to look for spikes in the main graph of the timing view. You can combine this with the frames view to get a sense of how the Niagara-specific spikes correlate with frame time spikes.

#### Understanding Niagara Timers

Niagara profiling is broken down into various timers, that can help pinpoint where Niagara is spending most of its time to guide where you can focus your optimization efforts.

_**Game Thread**_

_Ticking_

- **Niagara Manager Tick [GT]** - By default Niagara systems are ticked in batches by the Niagara World Manager. This timer can give an overview of the time spent ticking on the GT and waiting on async tick tasks to complete. Scalability is also handled here. Simulations are batched per tick group, so instances of the same system in different tick groups do not share the same system simulation. **Note:** Soloed systems are ticked individually and will not be batched here.
- **System Simulation Tick [GT]** - Game thread time spent ticking all instances of a system in the same tick group, used to prepare info for the async tick: gathering transforms, processing parameter stores etc. 
- **System Instance Tick [GT]** - Soloed System instance tick.
- **System Instance WaitForAsyncTick [GT]** - Time spent on the game thread waiting on an instance’s async tick.
- **Niagara Manager Update Scalability Managers [GT]** - Time spent updating scalability.

_Activation_

- **Activate (GT)** - Time spent activating a Niagara Component.
- **System Activate [GT]** - Time spent activating a System Instance. 

_**Worker Threads**_

- **FNiagaraSystemSimulationTickConcurrentTask** & **System Simulation Tick [CNC]** - Concurrent work done for system simulation ticking. System and emitter scripts are compiled to a single VM script. This task invokes the Vector VM and executes that script.
    - Transfers data to Emitter Instances
    - Launches System Instance tasks
- **System Instance Tick [CNC]** - Sets up and runs the ticks for the Particle portions of the Emitter scripts. 
-  **Emitter Tick [CNC]** - Time spent ticking the particle stages of the emitter for CPU sims.
    - **Emitter Simulate [CNC]** - Corresponds to Particle Update
    - **Emitter Spawn [CNC]** - Corresponds to Particle Spawn
    - **Emitter Event Handling [CNC]** - Corresponds to Particle Event Handlers
        
          
        

_**Render Thread**_

- **Compute Dispatch (GPU Emitter Dispatch [RT])**
    - Runs GPU Simulation scripts including particle spawn & update, and simulation stages.
    - Dispatches are ordered in safe to overlap groups
    - Determines the final buffers used for rendering
    - Can be executed in
        - Pre Init Views
        - Post Init Views
        - Post Render Opaque
    - Features used in the GPU simulation determine when they are executed e.g. depth reads, distance field sampling etc.
        - Enable “GPU Tick Information” in the System Editor Show menu to see the features enabled in a simulation.
- **Get Dynamic Mesh Elements**
    - Cost associated with geometry for renderers, which depends on:
        - Number of renderers
        - Number of views the system is visible in
        - Type of renderer
    - CPU emitters need to copy data to GPU
    - Renderer Visibility and Mesh Index require a sort and cull GPU task
    - Per Particle Mesh LODs need to build more mesh batches

  

### Example Capture

Below are screenshots from an example capture taken from a Lyra Game, where there was a frame spike near the beginning of a match. Most of the frame time is spent spawning the player and AI controllers, but there were spikes in Niagara systems relative to other frames, including the gun pad systems which contributed ~0.96ms across all worker threads that frame.

[![](https://dev.epicgames.com/community/api/learning/image/6796dad0-c53f-45da-850a-1229825d5c26?resizing_type=fit)](https://dev.epicgames.com/community/api/learning/image/6796dad0-c53f-45da-850a-1229825d5c26?resizing_type=fit)

Insights view of the frame.

[![](https://dev.epicgames.com/community/api/learning/image/166a4de4-4c26-49ab-9bb5-3f2fbbec69c7?resizing_type=fit)](https://dev.epicgames.com/community/api/learning/image/166a4de4-4c26-49ab-9bb5-3f2fbbec69c7?resizing_type=fit)

Zoomed in view of the Timers tab for that frame, focusing on NS_GunPad

The overall frame time was 33.5ms which is approximately ~30fps. In the rest of the game we’re seeing 70 to 80 fps, so this is a significant spike. However Niagara only spent about .4ms ticking on the GT, so the gun pad systems didn’t contribute much to the GT overhead. 

**NOTE:** The hardware used in this capture has a Threadripper CPU, so the worker thread performance is likely not realistic compared to console hardware, and there may be more GT overhead waiting on tasks threads on different platforms.

[![](https://dev.epicgames.com/community/api/learning/image/8fdafe91-3e33-4427-a8b2-9ec6cdcba1ed?resizing_type=fit)](https://dev.epicgames.com/community/api/learning/image/8fdafe91-3e33-4427-a8b2-9ec6cdcba1ed?resizing_type=fit)

Highlight of the Niagara Manager Tick [GT] timer

If we look more closely at the Niagara Manager Tick, we can see that there are 15 gun pad instances ticking this frame, which is to be expected since they are all being spawned at once. They also remain relevant and ticking since they are only set to cull after 1 second of not being rendered, so there is a lasting overhead to spawning all gun pads at once. Other item pickups will also behave the same.

[![](https://dev.epicgames.com/community/api/learning/image/cd2407b4-e4ee-48ba-8674-a57f16b10754?resizing_type=fit)](https://dev.epicgames.com/community/api/learning/image/cd2407b4-e4ee-48ba-8674-a57f16b10754?resizing_type=fit)

Zoomed view of the Niagara Manager Tick [GT]

So while they may not currently have a significant overhead, especially compared to the rest of the frame, this is illustrative of the overhead of having more systems relevant than need be. If the systems were less performant, more representative target hardware proves slower, or if there were more of them in the level, this could be a greater opportunity for optimization, especially given the tight frame resources when initializing the level.

To explore simulation optimizations, we’ll first take a look at the timings for the Gun Pad system with the Timers tab, specifically looking at the Callees tab. This will show the contribution of every timer that’s a child of the selected timer. In this case they are sorted by Inclusive timing, which is the total time spent in the timer, including its children’s timers.

[![](https://dev.epicgames.com/community/api/learning/image/8900b875-3e2a-475b-b6f6-e85a57e2c678?resizing_type=fit)](https://dev.epicgames.com/community/api/learning/image/8900b875-3e2a-475b-b6f6-e85a57e2c678?resizing_type=fit)

For reference here’s what the tracks for a couple of worker threads executing the System instance ticks. Each thread executes four instance ticks sequentially.

[![](https://dev.epicgames.com/community/api/learning/image/40f6fef9-0ae4-4198-ba0a-0b38d344c0a5?resizing_type=fit)](https://dev.epicgames.com/community/api/learning/image/40f6fef9-0ae4-4198-ba0a-0b38d344c0a5?resizing_type=fit)

Here’s a zoomed in view of just one system instance tick, so the different emitter ticks can be seen. Each emitter tick contributes about .003 to .008 ms each.

[![](https://dev.epicgames.com/community/api/learning/image/5671489e-e7b9-44a1-905e-1fc6c7bd6d31?resizing_type=fit)](https://dev.epicgames.com/community/api/learning/image/5671489e-e7b9-44a1-905e-1fc6c7bd6d31?resizing_type=fit)

For the whole frame, it looks like PA_Rings contributes about .06ms and Beam_Base, Beam_Diffuse and Beam_Core contribute .056-.057 ms. This is only looking at one frame, however, so we should look at a more representative time window, and their averages to make judgments on where to focus optimization efforts.

Here’s the timer tab from a larger time span focusing on the emitter ticks. The averages are significantly lower than the times seen before, which would make sense after scalability kicks in, and fewer system instances are running in a frame. From this data is looks like Cubes_Trails is the most costly emitter, but they all are fairly insignificant at .01ms each, or less.

[![](https://dev.epicgames.com/community/api/learning/image/59186539-c86b-46de-882c-8f5a66b04496?resizing_type=fit)](https://dev.epicgames.com/community/api/learning/image/59186539-c86b-46de-882c-8f5a66b04496?resizing_type=fit)

We can use the Niagara editor’s performance mode to dive more into the asset and look for optimizations. For instance count optimizations, we could delay or stagger the spawning of the gun pad effects that are far away from the player character, or try employing pre-culling on the effect type.

**NOTE:** The Niagara editor's performance mode does not work with the new virtual machine.

[![Capture of the Cube Trails, and their source emitter Cubes](https://dev.epicgames.com/community/api/learning/image/979b7f12-606f-4bfa-bd42-f4c6de9d82de?resizing_type=fit)](https://dev.epicgames.com/community/api/learning/image/979b7f12-606f-4bfa-bd42-f4c6de9d82de?resizing_type=fit)

Capture of the Cube Trails, and their source emitter Cubes

We'll start by looking at the Cube Trails emitter, since it was top of this list for footprint in the insights capture. The above capture is displaying the average times with relative values for module timing. The update script timing roughly matches the timings seen in the insights capture at around .01 to .02 ms. However the modules themselves don't account for much of this timing in the update script.

Still there are some quick optimizations we can make here. The Cube Trails emitter does not inherit velocity when sampling particles from their source emitter, but the dependencies system doesn't know that, so it always recommends adding the Solve Forces and Velocities module. Removing this module and dismissing the issue generated on the Sample Particles from Other Emitter module will achieve the same behavior with less overhead (saving ~5% according to the Niagara editor).

The multiple calls to scaling color could potentially be combined and simplified for further optimizations.

In the emitter update and particle spawn, spawning from and sampling from the source emitter have a high cost relative to the other modules. Eliminating the need to sample from another emitter entirely would reduce the emitter count and be another performance win. However this is non-trivial, and the current setup is likely the result of an effort to consolidate emitters already. Instead of having an emitter for each trail, consolidating to two is a good alternative.

In the future, converting over to stateless emitters for each trail would likely be the best optimization.

[![](https://dev.epicgames.com/community/api/learning/image/794ca02e-b204-4e29-97a3-0f8e165a3635?resizing_type=fit)](https://dev.epicgames.com/community/api/learning/image/794ca02e-b204-4e29-97a3-0f8e165a3635?resizing_type=fit)

Beam_Core and Beam_Base are made of all the same modules

Since there isn't much more we can do with the Cube Trail emitter without rebuilding the effect, we can look for other areas for optimization. 

If we look at Beam_Base and Beam_Core they run nearly identical logic, with only some variation of data, which makes them good candidates for merging into a single emitter. Moreover they can share the same renderer, so there no need to use visibility tags when combining the two emitters avoiding the associated overhead.

Overall there may be other emitters that could be merged, but they would be more difficult than these two. In the future migrating to lightweight emitters would likely be best suited for this use case. 

###### Documentation & Tutorials

- [Lightweight Emitters](https://dev.epicgames.com/documentation/en-us/unreal-engine/niagara-lightweight-emitters-overview)

### View Modes - Measuring Rendering Complexity

VFX often have lots of overlapping translucent sprites and meshes, so they can often be the cause of overdraw, so it's also important to validate your Niagara system's shader complexity. You can see a general overview of the complexity with the Shader Complexity View Mode. For a more detailed view at overdraw the Quad Overdraw View Mode can be used.

Reducing particle counts and spreading them further apart can reduce overdraw. The less screen space particles occupy the less of a concern this will be as well. 

###### Documentation & Tutorials

- [View Modes Documentation](https://dev.epicgames.com/documentation/en-us/unreal-engine/viewport-modes-in-unreal-engine#shadercomplexity)

[![Shader Complexity of the Gunpad Loading particle system in a Lyra game session](https://dev.epicgames.com/community/api/learning/image/6ae33324-d852-408f-ad02-ad6ff5bb5e2c?resizing_type=fit)](https://dev.epicgames.com/community/api/learning/image/6ae33324-d852-408f-ad02-ad6ff5bb5e2c?resizing_type=fit)

Shader Complexity of the Gunpad Loading Niagara system in a Lyra game session

Above is a capture of one of the gun pads in the Expanse level. There is a fair amount of overdraw in this effect, and it's common across the level. It could be optimized to have less overlapping sprites, but that would also change the visuals of the effect. Spawn count scaling could be used to reduce the number of particles spawned at different scalability settings to balance the trade-off for different platforms.

For a more detailed look at the overdraw of this particle system we can use the different view modes in the Niagara editor to see the effects of edits made to the system in real time. 

[![](https://dev.epicgames.com/community/api/learning/image/a988805d-a62c-46c5-a9d0-0951e7a6bb3e?resizing_type=fit)](https://dev.epicgames.com/community/api/learning/image/a988805d-a62c-46c5-a9d0-0951e7a6bb3e?resizing_type=fit)

The above image is a side by side comparison of the overdraw and lit views. On the left is the unedited system, and on the right is the system with the NE_RingMeshTimerInternal, Beam_Core, and Beam_Based emitters disabled. This eliminates almost all overdraw at 7 and above. Just turning on and off emitters can give a good idea of where to focus efforts on reducing overdraw.

[![](https://dev.epicgames.com/community/api/learning/image/91970a26-895e-4a9a-b13d-0ba2671c3ac2?resizing_type=fit)](https://dev.epicgames.com/community/api/learning/image/91970a26-895e-4a9a-b13d-0ba2671c3ac2?resizing_type=fit)

Niagara has built-in support for spawn count scaling based on scalability settings. Various scalability overrides and settings can be accessed in the Scalability mode of the Niagara editor. As a test I added scalability overrides to the three emitters disabled above, to halve their counts at Medium scalability and below.  

[![](https://dev.epicgames.com/community/api/learning/image/2fed7a64-57b5-4081-8a5f-b8f80deeeb0f?resizing_type=fit)](https://dev.epicgames.com/community/api/learning/image/2fed7a64-57b5-4081-8a5f-b8f80deeeb0f?resizing_type=fit)

Emitter Scalability Overrides with spawn count scaling on Low and Medium

[![](https://dev.epicgames.com/community/api/learning/image/b78639da-94b2-4c06-a947-ffdac52509ed?resizing_type=fit)](https://dev.epicgames.com/community/api/learning/image/b78639da-94b2-4c06-a947-ffdac52509ed?resizing_type=fit)

Lit View comparing the effects of spawn count scaling

In the scalability mode, you can toggle between different scalabilities quickly to preview the differences. Here is a side by side comparison of the lit views of the medium and high scalabilities. The difference in brightness is noticeable, but some material changes could reduce the discrepancy.

[![](https://dev.epicgames.com/community/api/learning/image/bfdf394f-1e09-4562-bfcb-b4b7ab3f1a24?resizing_type=fit)](https://dev.epicgames.com/community/api/learning/image/bfdf394f-1e09-4562-bfcb-b4b7ab3f1a24?resizing_type=fit)

Quad Overdraw view comparing the effects of spawn count scaling

Here is the side by side comparison of their quad overdraws. The 7+ areas from the beams is almost completely eliminated, and while the ring still has a lot of 8+ coverage it's reduce most of the 10 coverage.

This shows that spawn count scaling is effective for reducing this system's overdraw, and each scalability level could be further refined to balance fidelity and performance for their respective target hardware. 

For platforms that support variable rate shading, you can also adjust the shading rate of the materials used in the system to reduce the impact of their overdraw. This is controlled on the material details under Material > Advanced > Shading Rate. The shading rate will effectively reduce the resolution that the material is drawn at. 

[![](https://dev.epicgames.com/community/api/learning/image/e4414797-009e-4b84-a610-4b317d202d3c?resizing_type=fit)](https://dev.epicgames.com/community/api/learning/image/e4414797-009e-4b84-a610-4b317d202d3c?resizing_type=fit)

### Niagara Debugger

The Niagara debugger also includes performance profiling tools that can be used alongside PIE for more rapid performance profiling. More details can be found on the docs page.