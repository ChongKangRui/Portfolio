+++
categories = ["cp-dev"]
coders = []
date = 2026-03-31
description = "A VR and PC shooter project that created by Unreal Engine"
image = "/Portfolio/NB/Logo.png"
title = "Commercial VR Project: NetherBloom"
type = "post"
[[tech]]
logo = "/Portfolio/asset/UnrealLogo.png"
name = "Unreal"
url = "https://www.unrealengine.com/en-US/"
[[tech]]
logo = "/Portfolio/asset/c++Logo.png"
name = "C++"
url = "https://learn.microsoft.com/en-us/cpp/cpp/?view=msvc-170"
+++

## VR Gameplay Demonstration

{{< youtube "rQdojWyPCv0" >}}


## My Contribution & Challenging

{{< LP "My contribution to this project have across multiple aspect, including custom procedural generation solution, gameplay, AI, optimization etc.">}}


### 1. Procedural Generation


#### Level Generation

![](/Portfolio/NB/LevelDesignConcept.png)

![](/Portfolio/NB/LevelDesignConcept_2.png)



{{< LP "Here is the concept of the generation. Level design defines a set of rules that will apply to the level generation. The generation will create areas following a fixed sequence. All generation will use seed, giving the designer a way to control the outcome. The generation algorithm will detect spawn conditions based on collision detection. To prevent dead ends before level generation is complete, each door within an area will have 3 chances to spawn, allowing the generation to step back. If stepping back happens 3 times, the entire generation will restart. ">}}

![](/Portfolio/NB/PCGshowcase.png)

{{< LP " Each connection between areas is defined by a connection point placed in the level instance. These points are tied together and overlapped to connect rooms. Each connection point acts as a 'door' and the designer can assign it as a start door (connects to the previous room), an end door (selected as the next entry during generation), or a special door (connects to a dedicated special room).">}}

#### Enemy Spawn Distribution

![](/Portfolio/NB/EnemyWeightDistribution.png)

{{< LP "After generation is complete, enemies are distributed to each area according to the enemy spawn points in that area. The designer can assign a spawn weight to each enemy at each spawn point. This weight directly affects enemy distribution—the higher the weight, the more spawn score that enemy consumes.">}}

{{< LP "Spawn score directly affects how many enemies spawn in the level. Stronger enemies have a higher spawn score, so they appear less often, while weaker enemies have a lower spawn score and appear more frequently.">}}



### 2. Gameplay

#### Gun Shooting On VR

![](/Portfolio/NB/Shoot.png)

{{< LP "Our shooting mechanic works slightly differently in terms of logic. First, each gun can toggle between line trace and physical bullets. However, our physical bullets all use hierarchical instanced static meshes (HISM) to optimize performance instead of using the projectile component. A Bullet Pool Manager generates a fixed number of bullet instances and weapons can invoke an instance of a bullet. The bullet's movement, homing and arc-curve behavior are all handled by our custom logic.">}}

#### Gesture Skill

![](/Portfolio/NB/SkillRadialTrace.png)

{{< LP "Gesture skills are part of the game mechanic. The player can cast skills based on different hand gesture motions. I primarily contributed the skill effects (buffs and debuffs) that apply to each enemy and the player. These skill effects can include damage over time, speed deduction/increase, damage increase, stun, pushback, stealth and more.">}}

#### Climb

{{< youtube "8VfQVsAwmSE" >}}

{{< LP "The climb mechanic is one of the most interesting mechanics for level design, particularly in VR. The player must use the controller to grab a grab point and move their physical hand in order to move the character's body in the game.">}}


### 3. AI

#### Runner AI

![](/Portfolio/NB/RunnerEnemy.png)

{{< LP "I was in charge of one of the melee enemies in the game, called the Runner. The Runner has a lunge attack and a jump launch attack. Spots attached to the enemy can be shot by the gun. A red spot results in critical damage to the enemy, while a blue dot spawns a sub-enemy from the Runner.">}}

#### Spitter AI

![](/Portfolio/NB/SpitterEnemy.png)

{{< LP "I was also in charge of one of the ranged enemies, called the Spitter. The Spitter has 3 aggressive attacks. It can shoot a projectile that tracks the target, shoot a split projectile, or shoot an arc-curve based projectile. Each projectile have a chance applies a thorn debuff(slowdown, damage over time etc) to the player when hit.">}}

{{< LP "The Spitter also has 3 defensive behaviors when the player gets too close. When the player gets too close, the Spitter will either spawn an explosive miner or push the player backward before running away. If all defensive skills are on cooldown, it will simply run away from the player without doing anything. The standing location of the Spitter is determined by the EQS to ensure its projectiles are always reachable toward the player.">}}


### 4. Porting Of PC

{{< youtube "5_VEJl9NQHg" >}}

While contributing most of the gameplay to VR, I was also responsible for porting the gameplay mechanic into PC. 