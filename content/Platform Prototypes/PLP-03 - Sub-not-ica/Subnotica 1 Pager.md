---
tags:
  - platformprototypes
  - production
  - documentation
cssclasses:
  - img-grid
aliases:
  - 11/11/24 World Building Chat
---
# Overview 

**Third Person Submarine Shooter**, Specifically testing ==Underwater Movement== with an emphasis on **speed**, all controlled by a ==Gyro Aim System==, allowing the mouse to **control all rotations**, while combating a ==Complex AI== built to respond to a any space and environment.

**GIT REPO**
https://github.com/BEANM00N/IsoRogueProto.git

**PURPOSE**
 - Experiment with correct configuration for Underwater Movement;
	 - Speed Control
	 - Movement Tactility
	 - Water Drag - (Maybe experiment with Pressure)
 - Learn the best practices for equippables and upgrade systems
 - Test integration of an Armour System and how that affects fast paced gameplay

---
# Systems 

## Underwater Movement
 - Similar to games like **Subnautica** the player will take control of a Submarine.
 - Similar to the effect Zero Gravity affects Spacecraft, we want to explore and experiment with how *Water Drag* affects submarines;
	 - Submarine Hull Shape
	 - Hull Structure
	 - Speed
	 - Density
	 - Temperature
 - The most interesting part while exploring this affect on movement is ensuring *Tactility* and *responsiveness* are key feelings the player notices.
 - **DRIFT BABY**
```image-layout-a
![[Underwater 1.png]]
![[Underwater 2.png]]
```


---
## Gyro Aim System
 - To accompany the **Movement System** a Mouse Gyro System will control a lot of the Submarine's inputs. This is quite an unconventional approach to character control in general but offers some of the most input granularity. 
 
```image-layout-a
![[Gyro.png]]
![[Gyro 2.png]]
```

---

## COMPLEX AI 
 - To fill out the Gameplay we want to experiment with a new *Pathfinding* Method for enemy AI, releasing them from the shackles of traditional navigation constraints.
 - This new method would allow the AI to move in any space it's placed in, moving freely along all *3D Axis*.
 - We want them to be affected by the same *Underwater* Constraints that affect the player's Movement.
 
```image-layout-a
![[Enemy 1.png]]
![[Enemy 2.png]]
```


