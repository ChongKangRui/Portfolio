+++
categories = ["cp-dev"]
coders = []
date = 2020-06-19T23:00:00Z
description = "A first-person escape room horror game set in Japan's Edo era."
steam = "https://store.steampowered.com/app/2220660/Chiyo/"
image = "https://cdn.akamai.steamstatic.com/steam/apps/2220660/capsule_616x353.jpg?t=1700451759"
title = "Chiyo"
type = "post"
[[tech]]
logo = "https://cdn.icon-icons.com/icons2/2389/PNG/512/unreal_engine_logo_icon_144771.png"
name = "Unreal"
url = "https://www.unrealengine.com/en-US/"
+++
## Gameplay Screenshots

{{< img2 "https://cdn.cloudflare.steamstatic.com/steam/apps/2220660/ss_de583b18f60b219f0655d39ba1f5c7baade31827.600x338.jpg?t=1701851250" "https://cdn.cloudflare.steamstatic.com/steam/apps/2220660/ss_ce5b7df240c93e8756fecbe0aa9469ac045bf324.116x65.jpg?t=1701851250">}}
{{< img2 "https://cdn.cloudflare.steamstatic.com/steam/apps/2220660/ss_88c8f3e23bd7f96bbc42dd47de14e0ae896a27b9.600x338.jpg?t=1701851250" "https://cdn.cloudflare.steamstatic.com/steam/apps/2220660/ss_57de579dac5797f19e097a53add22fd42fea66d8.600x338.jpg?t=1701851250">}}


## Gameplay Trailer

{{< youtube "2KGlswJclmg" >}}


## My Contribution & Challenging

### 1. Interaction system
{{< LP "I am one of the people who contributed to designing the basic interaction system when we create it from scratch. The interaction system that I contributed included how players interact with the interactable object, zoom in on the interactable object and even place items on those interactable objects. The purpose of this system is to simplify everything and make the system easy to use and understand by other programmers." >}} 

### 2. Inventory system and pickable

#### Pickable
{{< LP "Before I start with the inventory system, let me introduce the pickable. Pickable is a branch of interactable. Pickable was responsible for being able to be picked up by the player, used/interacted with other interactable objects, and stored their own data such as name, description, variable property, and so on. I was in charge of developing both the pickable base and the inventory system. To manage such a large scale of multiple pickable instances, a datatable will be used to allow the designer to easily adjust pickable property. " >}}

### Inventory system

{{< LP "The inventory system is a system that is responsible for storing item references, showing item information, providing item inspection and providing an interface for players to use for the interactable objects.During the inspection, the player will be allowed to zoom in and rotate or interact with the item as well. Inspection was basically using a component called SceneRender2DComponent to allow the item to be shown as an image in the widget blueprint. This will prevent items from clipping into a wall or object while the player is inspecting them." >}}

### 3. Save system

{{< LP "The save system is one of the most challenging parts that I handled in this project. The save system is responsible for saving and restoring the puzzle. For the saving part, it should save the door attribute (is open/unlock, cursed?), the pickable item that is stored inside the inventory, the journal that is already recorded, the puzzle state and so on. For the restore, it either has to restore everything including pickables and door attribute or it only restores the puzzle state and spawns the player on the correct spawn point. During restoration for specific puzzles, it may also need to restore presave pickable items or trigger specific sequences." >}}

{{< LP "The main logic behind the save system to restore and save multiple puzzles and player progress was to use interfaces and integers. A preset array for puzzle manager will be saved accordingly following the sequence of the puzzle. Integers will eventually be used to store the progress of the player. Once the integer meets the requirement of the puzzle (equal to or beyond the puzzle array index), it will call the interface to restore the puzzle." >}}

{{< LP "Because the save system has been involved in a lot of things in this project, it must be careful and clear what can be triggered or what must be prevented from triggering at the start of the game. As a result, many factors must be considered during the creation of the save system, making it one of the more challenging parts of this project for me." >}}

### 4. Puzzle Time Travel

{{< LP "Puzzle time travel is one of the puzzles in the game. Time travel will allow players to go to different seasons and collect different items by changing the clock's time. Therefore, a system will be responsible for changing seasons (like VFX), creating a seasonal event for related items, and deciding which time belongs to which season. An unordered map will be used to store the season and time, and a delegate will be used for related items to bind their season changing event." >}}

{{< LP "To transform clock time based on angle, some calculations will need to be done. I am basically using the dot product and ACOS to get the angle of the clockhand. The dot product vector will be taken in the direction from the center point to the default point (which is 0) and from the center point to the end of the clockhand. To transform time based on angle, it need to use time divided by angle and use this value to multiply by the angle that we got previously." >}}

{{< LP "Since the clock will also be responsible for controlling the skylight, directional light, and other related VFX. Thus, for optimization purposes, all of the VFX will only be activated when the player begins to solve the time travel puzzle." >}}

### 5. Puzzle Onsen
{{< LP "Puzzle onsen is one of the puzzles as well in the game. The player has to get the orb that is stuck inside the onsen pipe to pass this puzzle. Therefore, this puzzle was basically built around an orb, pipes and pumps. The pumps will be responsible for controlling the force of the pipes." >}}

{{< LP "To simulate the water force slowly increasing and decreasing when the player activates the pump, the force of the orb will be modified by using the timeline. The pipes were built by the spline mesh component, so the orb can get the precise vector when it moves along the spline. Another problem to solve is that when the player tries to transfer the orb from pipe to pipe, how can the pipe detect it? It also needs to be clear which pipe contains the orb and controls it." >}}

{{< LP "The solution is that two collision detections will be put at the begin and end of the pipe. These collisions will have a fixed distance for designer to adjust and set their detection range when the orb is near the edge of the pipe. These collisions will be responsible for removing and assigning the pipe reference to the control orb" >}}


### 6. Part of the AI
{{< LP "I was also in charge of part of the AI in this game. One of the main AI that chases the player was maintained and improved by me during the middle of the development. This AI is responsible for chasing players, patrolling, teleporting, sense player by hearing and sight perception, and even detecting or passing through the door that is sealed by the player." >}}
