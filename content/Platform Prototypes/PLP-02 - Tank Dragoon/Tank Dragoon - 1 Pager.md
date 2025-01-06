---
tags:
  - platformprototypes
  - production
  - documentation
cssclasses:
  - img-grid
---
# Overview 

**Tank Dragoon** is an ==Isometric Roguelike Shooter==, Comprising of a ==Dead Ops Arcade== gameplay loop, combined with ==Deep Rock Survivor's Card== System and Armoured Core's Modular Equipment. Face a never ending horde of escalating difficulty while Leveling up.  

**GIT REPO**
https://github.com/BEANM00N/IsoRogueProto.git

**PURPOSE**
 - Test viability of scalable roguelike systems
	 - Randomized Cards System
	 - Modular Equipment System
	 - *==Bonus==* Armour System
	 - ==Bonus== Dynamic Horde Difficulty
 - Learn the best practices for equippables and upgrade systems
 - Test integration of an Armour System and how that affects fast paced gameplay

---
# Systems 

## CARD DRAW
 - Similar to Cult of the Lamb and Deep rock Survivor, the **Card Draw** will allow the player to choose a card from a random selection of cards.
 - These cards each influence the player in different ways, affecting either, Weapons, Player Stats or World (Enemies, Environment, etc)
 - Cards will be assigned specific *Classes* that define when they can be chosen by the player, completely dependent on the kind of equipment they chose. Their purpose is to reinforce and add variance to the player's *Build*. (Subject to change. May be completely random)

```image-layout-a
![[Pasted image 20240918121858.png]]
![[Pasted image 20240918122233.png]]
```


---
## MODULAR EQUIPMENT
 - The **Card System** must be complemented by an underlying system, one that lets the player have *Some* control over the kind of build they want to pursue within the game, that has a specific playstyle that isn't muddled or forcefully altered at it's core by progression with the card system.
 
 i.e. A **Gunner** will always be a **Gunner**.

 - Similar to *Armored Core 6* Players will have the opportunity to outfit their tanks with different weapons, Engines, and **ARMOURS**

```image-layout-a
![[Pasted image 20240918123759.png]]
![[ftl parts.jpg]]
```

---

## ARMOUR SYSTEM
The **ARMOUR SYSTEM** in *Tank Dragoon* is a rudimentary version of the armour system present in *World of Tanks* and *War Thunder* - where positioning and plating make up a huge part of the skill ceiling. 

An Armour system of this level obviously affects the flow of gameplay dramatically, slowing it down substantially, which is why it must be implemented with upmost care. 

The **ARMOUR SYSTEM** will *only* come into effect for "Higher Tier" enemies, allowing the low armour dispensable units to contribute to the "Horde" element. The player should be in a juggling game, keeping both eyes on not only general crowd control but also on Armoured enemies that require more thoughtful positioning and a touch of strategy.

![[Pasted image 20240920131223.png]]
	🟧 - Critical
	🟩 - Low Armour
	🟨 - Medium Armour
	🟥 - High Armour

---

## DYNAMIC HORDE SYSTEM

Paired with the **Armour** System would be a dynamic horde system, creating a playing field similar to *Dead Ops Arcade* and *Vampire Survivor* with immense enemy density for the adrenaline and ease of chaining card abilities with weapon abilities with an added *Medium Tier* Enemy that adopts the Armour system that forces strategy and careful positioning while fending off the fodder.

---

## ART INSPIRATIONS
**Gothic Militarism**; A blend of Warhammer's absurd yet utilitarian designs and Wolfenstein's gritty "perfectionist" approach, creating a ridiculous yet sound rendition of a future soaked in war, dripping with *Hyperreality*. 
```image-layout-masonry-3
![[Wolfenstein.png]]
![[Wolfenstein 2.png]]
![[Warhammer.jpg]]
![[Warhammer 2.jpg]]
![[Warhammer 3.jpg]]
```

---
## THE WORLD

"War calls for evolution, but to what extent? Prehistoric giants now roam the barren battlefields, hopelessly searching for their *Prey* - But what *Prey*? What's even left out there? **Kriegsmaschine** they called them. Ancient Vessels of Destruction from a time long ago, created in an attempt to put a stop to the **42nd War**. It seems after 41 wars humanities evil and creativity still knew no bounds, no limits - although at that point I'm not even sure if you could still be human after so much trauma...

"If only the "humans" of that time could see their *Magnum Opus* now, still lumbering along *over a thousand years later*, dedicated to a long forgotten cause. I suppose it's a testament to their genius, engineering a will that would *surpass even it's creator*. The Earth is now theirs. We simply live *around* them, not with them. If they learnt of our existence the planet would be enveloped in *flame* for another few hundred years! Goodness! The flames from the last war can still be seen around!

Rumors from the last war say that an entire arsenal of *Super Nuclear Warheads* wasn't even enough to take **One** of those bastards down, with further accounts speaking of the Demon wading through the super hot fires as if it were a pond of water, completely unscathed. 
"I hear other parts of the world worship these machines as "Gods". I suppose I can't blame them. What can you possibly do when faced with *Divine Power* as unfathomable as theirs...

"But - It is our righteous cause to stand up against these behemoths - It is our sacred right to reclaim what was once ours - To lay the path forward for humanity to rebuild, to prosper, to live freely... Join us... Prove to the rest of the world what the indominable "human" spirit is capable of. I have a plan...

---
## MARKET VIABLITY

### COMPETITORS

```image-layout-masonry-3
![[Hades.jpg]]
![[Dead_Ops_Arcade.webp]]
![[Vampire Survivors.jpg]]
![[Cult of the Lamb.jpg]]
![[Enter the Gungeon.webp]]
![[ftl.jpg]]
```
---
**STEAM DB COMPARISONS**
![[SteamDbComparison.png]]

### VIABILITY

- **North American market for Roguelike Game was valued at $ 264.42 million in 2023** and will **reach $ 375.57  million by 2030**, at a **CAGR of 5.54%** during the forecast period of 2024 through 2030.

- **Asia-Pacific market for Roguelike Game was valued at $ 461.66 million in 2023** and will **reach $ 688.91 million by 2030**, at a **CAGR of 6.77%** during the forecast period of 2024 through 2030.

- **Europe market for Roguelike Game was valued at $ 225.99 million in 2023** and will **reach $ 306.87 million by 2030**, at a **CAGR of 5.05%** during the forecast period of 2024 through 2030.



