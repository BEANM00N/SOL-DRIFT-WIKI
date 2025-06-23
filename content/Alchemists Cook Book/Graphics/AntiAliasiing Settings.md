# Best UE4/5 Anti-Aliasing Values
Unreal Engine 4/5
# Universal/Variable Tweaks

r.MipMapLODBias= (If using blurry/strong TAA use a value of -2 or -1, if using a weak/light TAA or no TAA use a value of 1 or 2, negative values increase texture detail which mitigates blurring & higher values decrease it which mitigates aliasing. Negative values also reduce performance, default is 0)
r.Tonemapper.Sharpen= (0.0 - 3, the less TAA you're using the lower you might want it to be and the more TAA the higher. Default is 0.5)

# Method: TAA

[/Script/Engine.RendererSettings]
r.TemporalAA.HistoryScreenpercentage=200
r.BasePassForceOutputsVelocity=1
r.DefaultFeature.AntiAliasing=2
r.TemporalAAPauseCorrect=1
r.TemporalAA.Upsampling=1
r.TemporalAACatmullRom=1
r.TemporalAA.Algorithm=0
r.PostProcessAAQuality=6
r.AntialiasingMethod=2
r.TemporalAA.Quality=2
r.VelocityOutputPass=1
foliage.DitheredLOD=1

[/Script/UnrealEd.CookerSettings]
+VersionedIntRValues=r.VelocityOutputPass

### Presets: TAA (Optional)

### No AA TAA

r.TemporalAACurrentFrameWeight=0.40
r.TemporalAAFilterSize=0.1
r.TemporalAASamples=1

### Very Light TAA

r.TemporalAACurrentFrameWeight=0.35
r.TemporalAAFilterSize=0.2
r.TemporalAASamples=1

### Light TAA

r.TemporalAACurrentFrameWeight=0.25
r.TemporalAAFilterSize=0.4
r.TemporalAASamples=8 (1 if theirs too much jitter in said game)

### Mild TAA

r.TemporalAACurrentFrameWeight=0.2
r.TemporalAAFilterSize=0.4
r.TemporalAASamples=8 (1 if theirs too much jitter in said game)

### Moderate TAA

r.TemporalAACurrentFrameWeight=0.15
r.TemporalAAFilterSize=0.4
r.TemporalAASamples=4 (1 if theirs too much jitter in said game)

### High TAA

r.TemporalAACurrentFrameWeight=0.1
r.TemporalAAFilterSize=0.4
r.TemporalAASamples=4 (1 if theirs too much jitter in said game)

–––––––––––––

# Method: TSR

[/Script/Engine.RendererSettings]
r.TSR.ShadingRejection.ExposureOffset=3.0
r.TSR.ShadingRejection.TileOverscan=3
r.TSR.ShadingRejection.SampleCount=0
r.TSR.RejectionAntiAliasingQuality=2
r.TSR.ShadingRejection.Flickering=1
r.TSR.History.ScreenPercentage=200
r.TSR.History.GrandReprojection=1
r.BasePassForceOutputsVelocity=1
r.TSR.Velocity.Extrapolation=1
r.TSR.History.UpdateQuality=3
r.TemporalAA.Upsampling=0
r.TemporalAA.Quality=2
r.AntialiasingMethod=4
r.VelocityOutputPass=1
foliage.DitheredLOD=1
r.TSR.Resurrection=1
fort.TSR.Enable=1
r.TSR.16BitVALU=0

[/Script/UnrealEd.CookerSettings]
+VersionedIntRValues=r.VelocityOutputPass

### Presets: TSR (Optional)

### Clearest TSR

r.TSR.Velocity.WeightClampingSampleCount=0
r.TSR.ShadingRejection.Flickering.Period=0
r.TSR.History.SampleCount=8

### Balanced TSR

r.TSR.Velocity.WeightClampingSampleCount=2
r.TSR.ShadingRejection.Flickering.Period=2
r.TSR.History.SampleCount=8

### Stable TSR

r.TSR.Velocity.WeightClampingSampleCount=3
r.TSR.ShadingRejection.Flickering.Period=3
r.TSR.History.SampleCount=16

_UE5 Only_

–––––––––––––

# Method: FXAA

[/Script/Engine.RendererSettings]
r.DefaultFeature.AntiAliasing=1
r.TemporalAA.Upsampling=0
r.PostProcessAAQuality=6
r.AntialiasingMethod=1
foliage.DitheredLOD=0
r.FXAA.Quality=5

–––––––––––––

# Additional

# Blur

These commands simply deblur the image and since that's probably one reasons you're here, might as well add these to your list as well

r.SceneColorFringeQuality=0
r.MotionBlur.Amount=0
r.MotionBlurQuality=0

# Denoise

These are commands you can use to reduce or remove noise, artifacts, fireflies, etc in your game, which can occur if you disable or lower TAA's strength _(Even when using a games stock settings these artifacts can still occur)_

r.Lumen.ScreenProbeGather.Temporal.MaxFramesAccumulated= (Higher values reduce flicker & noise but increase ghosting, so pick your poison, 8 - 64)
r.Lumen.ScreenProbeGather.TemporalFilterProbes=1
r.Lumen.ScreenProbeGather.MaxRayIntensity=0.3 (0.1 if too noisy)
r.Lumen.Reflections.MaxRoughnessToTrace=0
r.Lumen.ScreenProbeGather.ShortRangeAO=0
r.Lumen.Reflections.MaxRayIntensity=0.2 (0.07 or 0 if too noisy)
r.Lumen.Reflections.DownsampleFactor=1
r.Lumen.Reflections.BilateralFilter=1
r.Shadow.EnableModulatedSelfShadow=1
r.AmbientOcclusion.Compute.Smooth=1
r.Lumen.Reflections.Temporal=1
r.AmbientOcclusion.Denoiser=2
r.DiffuseIndirect.Denoiser=2
r.AmbientOcclusion.Compute=1
r.Reflections.Denoiser=2
r.MinRoughnessOverride=1 (0.2 if too strong)
r.ContactShadows=0
r.CapsuleShadow=0
r.BloomQuality=2 (0 if you dislike bloom. Higher than 2 makes bloom flicker)
r.SSR.Quality=0
r.VRS.Enable=0

–––––––––––––

# Notes

Multiple presets are for a few reasons; 1) each game is different thus will require different values and 2) people have different preferences for the ratio of aliasing to clarity they desire. With that said the part that says "Method" should always be included & the presets can either be ignored or can go after it

# Injected AA

If you're experiencing a lot of aliasing then you can also install ReShade and [download my preset](https://www.mediafire.com/file/mf856le21kp0fzk/ReShadeAntiAliasing.zip/file) that will help anti-alias the image further

# Upscaling

If you can't play the game at native then please [refer to this guide](https://www.reddit.com/r/OptimizedGaming/s/tj5cFKuTXh)
