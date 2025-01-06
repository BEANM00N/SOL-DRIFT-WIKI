### C++ VS Blueprints (CPU):

 - C++ scripts are immediately translated into machine code, compiling all of the data they need into only a few lines that gets sent to the CPU in ONE go.
 - Blueprint Scripts follow the flow of their nodes, often sending each node in the sequence as a separate function that gets broken down into machine code and then each function gets pieced together in the correct order. On paper, depending on the kind of mathematics, functions and macros that are being broken down, Machine code derived from Blueprints can contain substantially more lines. 
 - HOWEVER, the difference in the performance between Machine Code derived from C++ and Blueprints is so miniscule you would have to run each script on tick for THOUSANDS of Actors to see a difference.


### DEPENDENCIES:

Try your best to make dependencies **ONE WAY**.

E.g. Spawning a projectile that casts to its owner. IF it is absolutely necessary to send data back, use Event Dispatchers to execute events in the owner's BP. This keeps the Dependencies separate. So when the Projectile Spawns it has absolutely nothing to do with it's owner.

Blueprints work slightly different from C++, in the sense that is it is much easier to form dependencies through variables and senseless casting. C++ is tighter when it comes to Design Logic, so it naturally encourages a "Top to Bottom" approach to the flow of logic by splitting a lot of it's functions and classes into "Modules"

#### Example:

**Module: SOLDRIFT - Core**
**Contains:**
 - **Character Movement**
 - **Character Class**
 - **Gamemode**

**Module: SOLDRIFT - Intermediate**
**Contains:**
 - **Instance**
 - **Interfaces**

**Module: SOLDRIFT - Weapons**
 - **Projectiles**
 - **Weapon Classes**
 - **Damage Types**

This is a very rudimentary breakdown of how C++ Modules can be split up. If you need to call a function in another Class it has to be accessed via it's Module API

E.g. Referencing class without Module API
```
UCLASS()
class ENEMYMISSILE
	: public AActor
{
	GENERATED_BODY()
}
```

E.g. Referencing class with Module API
```
UCLASS()
class Weapons_API ENEMYMISSILE
	: public AActor
{
	GENERATED_BODY()
}
```

 - Module Dependencies should always be strictly one way as it FORCES the programmer to think out their systems in a top down approach. 
 - Because C++ Modules aren't dependent on each other, it is much "safer" to delegate these modules to different team members with a much lower concern of overlap until it's ready to link their one way dependencies. 
 - The way this differs to using Blueprints is that Blueprints are kind of treated as one BIG Module so your not actually forced to adopt a top down approach to designing logic because of how easily everything can be linked which I mentioned before. Therefore you REALLY have to think about how you want things to communicate with each other within blueprints. 
---

 **The Programmer has to be much more *Vigilant* when working with Blueprints as they don't have a "Physical Boundary" like modules for C++, and you have to be *especially vigilant* if you're creating a lot of CORE SYSTEMS within Blueprints (E.g. Save Systems, etc.).**

---


> [!NOTE]
> I would say over the past few months we've been really honing in on "keeping things separate" like storing certain functions and events within the instance and gamemode, but I just want to emphasize for us that this should be a REQUIREMENT going forward. Once we get back into the swing of things with development, I strongly believe our project needs a PURGE in some sense. Eradicating old assets that bloat memory and force needless dependencies is a must, as well as re-evaluating a lot of our code and really breaking down how we want that logic to flow. Of course some Two-way Dependencies will be inevitable, and that's okay, and realistically our CPU isn't really suffering from the way we've been doing it, but it's more about reinforcing good design practices and essentially creating "Rules" for ourselves. We have an innately strong sense of how logic flows anyway so I really don't see us getting into any dangerous Processing debt, However, Graphical Optimization is a different story and that is really the only thing holding us and every other game dev from running their games on a toaster, but sadly graphics are unavoidable.

