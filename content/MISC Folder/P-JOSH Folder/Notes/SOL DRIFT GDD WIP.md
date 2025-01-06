![[image3.png]]

> Contents
> 

[**Overview**](about:blank#overview) **3**

> Working Title 3
> 
> 
> [Current status](about:blank#current-status) 3
> 
> [Concept Statement](about:blank#concept-statement) 3
> 
> [Genre](about:blank#genre) 3
> 
> [Target Audience](about:blank#target-audience) 4
> 
> [Player Experience](about:blank#player-experience) 4
> 

[**Core loops**](about:blank#core-loops) **4**

> Movement Mechanics: 5
> 
> 
> [Standard Flight:](about:blank#standard-flight) 5
> 
> [Drift Mechanic:](about:blank#drift-mechanic) 6
> 
> [Twitch Movement:](about:blank#twitch-movement) 6
> 
> [Boosting:](about:blank#boosting) 7
> 
> [Evasive Tactics:](about:blank#evasive-tactics) 7
> 
> [Combat Components](about:blank#combat-components) 7
> 
> [Primary Fire and Missile Systems:](about:blank#primary-fire-and-missile-systems) 7
> 
> [Synergy and Enemy Vulnerabilities:](about:blank#synergy-and-enemy-vulnerabilities) 7
> 
> [Enemy Movement Capabilities:](about:blank#enemy-movement-capabilities) 8
> 
> [Strategic Decision-Making:](about:blank#strategic-decision-making) 8
> 
> [Combat Alert System:](about:blank#combat-alert-system) 8
> 
> [Meritocracy System](about:blank#meritocracy-system) 8
> 
> [Performance-Based Rewards:](about:blank#performance-based-rewards) 8
> 
> [Merit Accumulation:](about:blank#merit-accumulation) 9
> 
> [Medals and Achievements:](about:blank#medals-and-achievements) 9
> 
> [Reward System:](about:blank#reward-system) 9
> 
> [Progression and Motivation:](about:blank#progression-and-motivation) 9
> 
> [Merit Table](about:blank#merit-table) 10
> 

[**Player Progression - Ship-Levelling and Prestige System**](about:blank#player-progression---ship-levelling-and-prestige-system) **11**

> Ship-Specific Progression: 11
> 
> 
> [Unlocking New Abilities:](about:blank#unlocking-new-abilities) 11
> 
> [Prestige System:](about:blank#prestige-system) 11
> 
> [Customization and Variety:](about:blank#customization-and-variety) 11
> 
> [Continuous Engagement:](about:blank#continuous-engagement) 12
> 

# **Overview**

## **Working Title**

> SOL DRIFT
> 

## **Current status**

> Prototype stage:
> 
- Player movement and core mechanics are complete and are undergoing iterative polishing based on player feedback with 3 unique ships fully functional.
- Enemy AI are fully functional but are now undergoing their second stage of prototyping, recreating their pathfinding system into custom code, built with optimisation and scalability. They are currently very heavy on performance.
- Environment and objectives are only in their beginning stages of development, however recent additions of random “World Events” and obstacles have been enough to keep up with the rapid development of mechanics and other game systems.
- Multiplier System, Merit System and Achievement Systems have frameworks and working prototypes, all built with scalability in mind, making it a much smoother and faster process to add new entries to these systems.
- Player progression systems such as ranking up and score counting have frameworks built with working prototypes. Calculations are being processed correctly and saved to the player’s file. These frameworks require a little more tweaking before rewards can be tied to player progression. Currently Score and Rank do not offer the player anything of value.
- Save System is undergoing reformatting. The game was originally built for event purposes, allowing all players to create a unique save that they could come back to whenever they wanted, all on one computer. This system is now being built to accommodate only one player with three saves on one computer, capable of communicating with online Cloud Save functions.

## **Concept Statement**

> Enter the adrenaline-fueled realm of SOL DRIFT: a heart-pounding space combat adventure. Engage in lightning-fast maneuvers and intense battles as you confront a relentless advancing threat. With each encounter escalating in intensity, you'll push your piloting skills to their absolute limits in the ultimate test of survival, learning to effortlessly dance and drift around your foes. In this galactic war, you're not just a pilot - you're a legend in the making. Strap in, soldier, and unleash the fury of your ship as you carve your name into history.
> 

## **Genre**

> Arcade Space Combat with elements of Survival and Roguelike.
> 

## **Target Audience**

> This game was created to bring back the Arcade Atmosphere, offering a Plug and Play experience with a high skill ceiling with a competitive rewards system. The audience would consist of fans of other Flight shooters like Star Wars: Rogue Squadron, Project Wingman and Ace Combat - as well as players who enjoy the challenge of roguelike mechanics such as rewarding character upgrades and permadeath. Additionally, the game would appeal to those who enjoy competitive leaderboards and mastering skill-based gameplay mechanics.
> 

## **Player Experience**

> In SOL DRIFT, players embody the role of a seasoned mercenary, tasked with defending key sectors of a war-torn galaxy against relentless waves of enemy forces in an endlessly replayable horde mode experience. As a skilled pilot, players engage in intense space combat, facing off against hordes of enemy ships and formidable bosses while striving to survive as long as possible and climb the leaderboards. The game's dynamic and reactive gameplay evokes a range of emotions, from adrenaline-fueled excitement during intense combat encounters to moments of satisfaction and accomplishment as players overcome challenges and achieve high scores. With each gameplay session, players hone their piloting skills, unlock new ships and upgrades, and earn a reputation as legendary mercenaries feared and respected throughout the galaxy.
> 

# **Core loops**

> - Engage in fast-paced space combat, combining elements of racing simulation and intense gunplay, utilising a unique movement system with unconventional mechanics to allow different approaches to combat.
> 
> - The Meritocracy. Performance in game (kills, sprees, combos, etc.) all contribute to player rewards. All Merits, Medals and Achievements reward the player in some way, be that through extra points and increases to the multiplier or receiving unique rewards.
> - Score directly translates to currency and level. Buy new components and upgrades for your ships as you unlock them, with each ship having their own short tech-tree that allows your ship to be “Prestiged”, resetting your ships equipped abilities and components but providing the ship with a new rank, increased base stats, and access to a new ability unique to each ship.

## **Movement Mechanics:**

> SOL DRIFT expands on what players are used to in a space combat game, re-engineering movement and game flow to be something more akin to a racing sim with guns. Responsive “Twitch Movement” is what drives the skill ceiling forward, allowing players of all levels to adapt and succeed while leaving plenty of room in the nuances to satisfy more advanced players in their journey to get better.
> 

### Standard Flight:

- Players control their spaceship using traditional flight controls, with the ability to pitch and yaw using a bespoke “Gyro Aim” system that allows the mouse to behave similar to a controller joystick - an unconventional choice but it allows for extremely granular control and wide range of sensitivity to accommodate the fast paced combat. The Gyro Aim system is currently clamped to a circle on screen 600px in diameter, multiplying the mouse cursor’s distance from the centre of the screen by a maximum factor of 1. A distance of 600px or more is equal to 1, with this number appropriately scaling down to 0 as the distance between cursor and centre decreases. This multiplier of 0-1 directly controls the sensitivity of pitch and yaw, which is uniquely processed by each ship making them feel very different from each other. Roll is part of the rest of the controls tied to WASD.
    
    ![SOL%20DRIFT%20GDD%20WIP%203a0bbc72d6c64bec9a8656407e87f136/image2.png](SOL%20DRIFT%20GDD%20WIP%203a0bbc72d6c64bec9a8656407e87f136/image2.png)
    
- Thrusters provide forward propulsion, allowing players to navigate through space.
- Flight is responsive and intuitive, catering to both novice and experienced players.
- The flight system is built completely from scratch using vector maths, designed to be reliable, reactive and light on performance.

### Drift Mechanic:

- The signature mechanic of SOL DRIFT, the drift allows players to execute dynamic manoeuvres at high speeds.
- When engaged, retro-thrusters positioned around the ship fire off, creating a burst of energy that enables drifting.
- While drifting, players maintain their original direction of travel but gain full control over their ship's rotation.
- Drifting increases sensitivity, allowing for quick and precise adjustments to orientation.
- Disengaging the drift causes the ship to continue in the new direction it is facing.

### Twitch Movement:

![SOL%20DRIFT%20GDD%20WIP%203a0bbc72d6c64bec9a8656407e87f136/image1.png](SOL%20DRIFT%20GDD%20WIP%203a0bbc72d6c64bec9a8656407e87f136/image1.png)

- SOL DRIFT emphasises responsive movement akin to a racing simulation, allowing for quick and precise inputs on a 3D axis.
- Players can perform rapid evasive manoeuvres, sharp turns, and precise adjustments to outmanoeuvre opponents.
- Twitch movement enhances the overall fluidity and intensity of gameplay, rewarding players for their reflexes and skill.

### Boosting:

- Players have the ability to boost for short bursts of increased speed. Boosting across all ships on average increases speed by around 50%, with some ships having unique play styles that call for speeds of nearly 80% more.
- Boosting can be used strategically to escape danger, chase down enemies, or quickly navigate through obstacles.
- Managing boost reserves is crucial, as overusing boost can leave players vulnerable to attack from faster attacks. Boost reserves automatically replenish over time.

### Evasive Tactics:

- The combination of standard flight, drifting, and boosting allows for a wide range of evasive tactics.
- Players can employ advanced manoeuvres such as barrel rolls, corkscrews, and sharp turns to evade enemy fire and outmanoeuvre adversaries. The longer the fight lasts, the more intense and dangerous the enemy’s weapons become - some trying to take down the player with unique experimental weaponry that has unique methods of countering.

## **Combat Components**

### Primary Fire and Missile Systems:

- Each ship in SOL DRIFT is equipped with a primary fire gun and a unique missile system.
- The primary fire gun serves as the main offensive weapon, delivering rapid-fire projectiles or energy fire depending on the ship's design.
- The missile system offers a more powerful but limited-use weapon, capable of delivering devastating blows to enemies.
- Players must strategically balance the use of their primary fire and missile systems, considering factors such as ammunition count, cooldown times, and enemy vulnerabilities.

### Synergy and Enemy Vulnerabilities:

- To effectively take down enemies, players must strike a synergy between their primary fire and missile systems.
- Some enemies may be more susceptible to certain weapons than others, requiring players to adapt their tactics accordingly.
- For example, fast-moving targets may be easier to hit with rapid-fire projectiles, while heavily armoured foes may require the use of missiles to inflict significant damage.
- Understanding enemy vulnerabilities and exploiting them with the right combination of weapons is key to success in combat, rewarding the player with extra points and increases to the multiplier.

### Enemy Movement Capabilities:

- Adding to the challenge, some enemies in SOL DRIFT possess the same movement capabilities as the player.
- These agile adversaries can execute swift manoeuvres, drift around obstacles, and engage in aerial acrobatics, posing a formidable threat to players.
- Facing enemies with comparable movement capabilities adds depth and complexity to combat encounters, requiring players to anticipate and react to enemy movements while maintaining their offensive stance.

### Strategic Decision-Making:

- Combat in SOL DRIFT is not just about reflexes and firepower; it also requires strategic decision-making.
- Players must assess the battlefield, identify priority targets, and choose the most effective weapons and tactics for the situation. Each ship will perform differently in each situation.
- Making split-second decisions amidst the chaos of combat is crucial for survival and victory.

### Combat Alert System:

- The player is assisted by a combat alert system, determining how close missiles are to the player, allowing for unique medals like “Bankshot” to be obtained by shooting down a missile in extremely close proximity or to simply evade.
- This system comes as an alternative to a classic radar system. The game is simply too fast and chaotic to be able to track the movements of enemies, projectiles and obstacles while focusing on the gameplay.

## **Meritocracy System**

### Performance-Based Rewards:

- Performance in-game, including kills, sprees, combos, and other notable accomplishments, contributes to the accumulation of Merits.
- Merits serve as a measure of a player's skill and achievement within the game, reflecting their prowess in combat and creativity with game systems.

### Merit Accumulation:

- Players earn Merits based on their performance in each gameplay session, with the quantity and quality of Merits varying depending on the difficulty and complexity of the tasks accomplished.
- Merits are awarded for a wide range of actions, from defeating enemies and completing objectives to executing advanced manoeuvres and achieving high scores.

### Medals and Achievements:

- In addition to Merits, players can earn Medals and Achievements for completing specific challenges, reaching milestones, or mastering certain gameplay mechanics
- Each Medal and Achievement is tied to a unique accomplishment or milestone, rewarding players for their dedication and skill.

### Reward System:

- All Merits, Medals, and Achievements contribute to player rewards, providing tangible benefits that enhance the gameplay experience
- Rewards may include
- Extra points and increases to the multiplier, allowing players to earn higher scores and climb the leaderboards
- Unlockable cosmetics, such as ship skins, allowing players to personalise their gameplay experience and wear their achievements.
- Access to special upgrades or weapons that provide an edge in combat that directly compliment the playstyle and requirements that were needed to unlock the achievement.

### Progression and Motivation:

- The Meritocracy system serves as a key component of player progression, motivating players to strive for excellence and continually improve their skills.
- By rewarding players for their achievements and accomplishments, SOL DRIFT fosters a sense of accomplishment and satisfaction, encouraging players to push their limits and overcome challenges.

## 

## **Merit Table**

| Merit | Description | Type | Score |
| --- | --- | --- | --- |
|  |  |  |  |
| Double | Two kills in quick succession. | Multikill | 50 |
| Triple | Three kills in quick succession. | Multikill | 100 |
| Quad | Four kills in quick succession. | Multikill | 200 |
| Furious Fives | Five kills in quick succession. | Multikill | 300 |
| Hexed's | Six kills in quick succession. | Multikill | 450 |
| Seven in the Grave | Seven kills in quick succession. | Multikill | 600 |
| Untouchable | 10 kills without taking any damage | Spree | 800 |
| Hard Target | 20 kills without taking any damage | Spree | 2000 |
| Phantom | 30 kills without taking any damage | Spree | 5000 |
| Ethereal Strider | 50 kills without taking any damage | Spree | 10000 |
| Gun Spree | 15 primary fire kills | Spree | 800 |
| Fire for Effect | 25 primary fire kills | Spree | 2000 |
| Shredifier | 40 primary fire kills | Spree | 4000 |
| Missile Mania | 15 missiles fire kills | Spree | 600 |
| Death Pencil | 20 missiles fire kills | Spree | 1500 |
| (Don’t Fear) The Reaper | 35 missiles fire kills | Spree | 3500 |
| Multi Lethal | Take down an enemy using both primary and missile fire. | Style Kill | 25 |
| Bank Shot | Take down an enemy missile while in extremely close proximity. | Style Kill | 100 |
| Retaliation | Take down the enemy that last hit you. | Style Kill | 75 |
| Denial | Take down an enemy missile. | Style Kill | 25 |
| Counter Battery | Take down an enemy missile with your own missile. | Style Kill | 35 |
| CurveBall | Take down an enemy while drifting and boosting. | Style Kill | 25 |
| Can't Touch This | Complete a wave without getting hit at all. | Style Kill | 1000 |

# **Player Progression - Ship-Levelling and Prestige System**

### Ship-Specific Progression:

- In addition to player progression, each ship in SOL DRIFT has its own level that can be increased through gameplay
- Ship levels are earned by using the ship in combat, completing objectives, and achieving milestones specific to that ship.

### Unlocking New Abilities:

- As a ship levels up, players unlock new abilities and enhancements unique to that ship
- These abilities may include special manoeuvres, weapon upgrades, defensive capabilities, or passive bonuses that augment the ship's performance in combat.

### Prestige System:

- Once a ship reaches its maximum level, players have the option to prestige the ship, resetting its level back to one while retaining certain benefits or bonuses.
- “Prestiging” a ship unlocks a new ability or enhancement exclusive to prestige ships, further enhancing the ship's capabilities and offering a fresh challenge for players to pursue.

### Customization and Variety:

- The ship-levelling and prestige system adds depth and variety to gameplay, allowing players to experiment with different ships and play styles as they progress through the game.
- Each ship offers a unique progression path, with its own set of abilities and enhancements that cater to different playstyles and strategies.

### Continuous Engagement:

- The progression system is designed to encourage continuous engagement with the game, providing ongoing incentives for players to explore new content, improve their skills, and strive for higher levels of achievement.

An example of what a ship’s upgrade tree will look like;

![SOL%20DRIFT%20GDD%20WIP%203a0bbc72d6c64bec9a8656407e87f136/image4.png](SOL%20DRIFT%20GDD%20WIP%203a0bbc72d6c64bec9a8656407e87f136/image4.png)