+++
categories = ["cp-dev"]
coders = []
date = 2026-03-31
description = "VR/PC roguelite shooter developed in Unreal Engine 5.4"
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

{{< youtube "9A6OSjdRqsw" >}}


## My Contribution & Challenging

{{< LP "My contribution to this project have across multiple aspect, including custom procedural generation solution, gameplay, AI, optimization etc.">}}


### 1. Procedural Generation


#### Level Generation

![](/Portfolio/NB/LevelDesignConcept.png)

![](/Portfolio/NB/LevelDesignConcept_2.png)

{{< LP "A rule-based 3D procedural level generator that creates areas in a fixed sequence with designer-controllable seeds. Uses collision detection and dead-end validation for spawn conditions. Each door receives up to 3 spawn attempts to prevent premature dead ends. Generation restarts entirely after 3 backtracks.">}}

![](/Portfolio/NB/PCGshowcase.png)

{{< LP "Each area connection uses a connection point placed within the level instance. These points are tied together and overlapped to link rooms. Each connection point acts as a door, which the designer can assign as a start door (connects to the previous room), an end door (selected as the next entry during generation), or a special door (connects to a dedicated special room).">}}

#### Enemy Spawn Distribution

![](/Portfolio/NB/EnemyWeightDistribution.png)

{{< LP "After level generation finishes, enemies get distributed to each area based on spawn points. Designers can assign a spawn weight to each enemy per spawn point. A higher weight increases how much spawn score that enemy consumes. I applied a Gaussian distribution to the enemy assignment process.">}}

{{< LP "Each generated area has a total enemy spawn count, which increases with the area's level. Stronger enemies cost more to spawn, so they show up less often. Weaker enemies cost less and appear more frequently.">}}

### 2. Gameplay

#### Item Interactable system

{{< LP "Implemented an item interactable system for VR gameplay. Every item, including guns, supports pickup and drop. Each item class uses polymorphism to enable flexible, overridable behaviors for pickup, drop, and use.">}}

#### Shooting In VR

![](/Portfolio/NB/Shoot.png)

{{< LP "Our shooting mechanic differs from standard implementations. Each gun can toggle between line tracing and physical bullets. Physical bullets use Hierarchical Instanced Static Meshes (HISM) for pooling instancing instead of Unreal's projectile component, optimizing performance. A Bullet Pool Manager generates a fixed number of bullet instances, which weapons invoke on demand. Bullet movement, homing behavior and arc trajectories are all handled by custom logic.">}}

#### Gesture Skill

{{< youtube "IM2V8VYFgww" >}}

{{< LP "Gesture based skills are part of the core gameplay mechanics, where players cast abilities based on hand movement. I primarily contributed to the skill effects - buffs and debuffs applied to the enemies and to the player. These effects include damage over time, speed modification, damage amplification, stun, pushback, stealth and more.">}}

#### Climb

{{< youtube "8VfQVsAwmSE" >}}

{{< LP "The climb mechanic enables unique VR level design opportunities. Physical grab of special points translates to player character movement. PC version has been implemented as well.">}}

#### Dash

{{< LP "Players can dash on ground or in the air. An air dash applies a gravity trajectory effect that influences falling behavior after the dash completes. A ground dash grants a temporary speed increase buff for a few seconds.">}}

### 3. AI

#### Runner AI

![](/Portfolio/NB/RunnerEnemy.png)

{{< LP "I owned the implementation of the Runner, a melee enemy featuring lunge attack, leap attack and melee attack. The Runner has destructible spots that respond to gunfire: red spots deal critical damage, while blue spots spawn a sub-enemy upon being shot.">}}

#### Spitter AI

![](/Portfolio/NB/SpitterEnemy.png)

{{< LP "I was also in charge of the Spitter, a ranged enemy with three aggressive attacks: a homing projectile, a multidirectional scatter attack and an arc-based projectile. Each hit has a chance to apply a thorn debuff (slowdown + damage over time) to the player.">}}

{{< LP "The Spitter has also four defensive behaviors triggered when the player gets too close: spawn an explosive mine, push the player backwards before retreating, spawn an area that does damage over time to target or simply run away if all defensive skills are on cooldown. Its standing position is determined by EQS to ensure projectiles can always reach the player.">}}


#### Enemy Manager

{{< LP "Designed an Enemy Manager that controls all AI behavior, determining whether enemies are aggressive or passive. The manager dynamically swaps AI states in real time, limits how many enemies can attack the player simultaneously and prevents the same AI from attacking repeatedly from start to finish. It also dictates which enemies engage the player based on distance.">}}

### 4. PC Port

{{< youtube "5_VEJl9NQHg" >}}

While contributing most of the gameplay to VR, I was also responsible for porting the gameplay mechanic into PC. 