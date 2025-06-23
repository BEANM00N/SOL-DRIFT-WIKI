---
color: var(--mk-color-orange)
---


## Master Behaviors

Every enemy behavior shall fall into one of a few **Master Behaviors** - these are general roles that the subsequent specific *Behavior Tasks* are delineated by

### OFFENSE

Offensive Decisions force the AI to try it's best to deal damage to a selected target in various forms and is typically achieved by the AI being given an advantageous set of parameter's around movement and target acquisition 

`as it stands this is accomplished via increasing their pitch lerp speed to speed their rotation values

Offensive decisions will be granted if the AI is either in an advantageous position (Eg "Preferred" distance to player) or the AI's personal state allows for it - *If they're not "scared of the player" based on a randomly assigned flee state granted on damage taken past a certain point*

### Defense/Self Preservation

When an enemy comes under too much threat such as their shields being broken or too much damage it will attempt to self preserve itself and perform actions that either make itself a harder target for the player via evasive flying or dropping countermeasures intended to specifically counter-act **whatever the player has attacked that enemy with the most consistently**

Defensive measures are going to be split into **PRE-EMPTIVE** & **REACTIVE** 

**PRE-EMPTIVE:** Are actions taken by the enemy to save itself from something *before* it is actually fired, thus nulling or reducing the effectiveness of it if committed to or encouraging the player to be more **proactive** in their choice of "weapons solution" by either swapping to a different means of attack during that enemies cooldown - essentially giving the player the chance to **bluff** an enemy by targeting with Missiles then swapping to Railgun if he decides to try and *Chaff-Smoke*.

In essence, given our *Time-To-Kill* being short for many targets and our offensive options for the player being so devastating, we can't rely on our enemies only reacting to specific gameplay events only *after* they happen since typically the player will be un-deterred and finish that target off swiftly, rendering it's attempts at self preservation null and gimmicky feeling. 

**REACTIVE:** Naturally, if they only reacted *before* they are hit and that is countered by the player it shouldn't be then a case that they suddenly "given up" 