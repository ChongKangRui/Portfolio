+++
categories = ["sp-dev"]
coders = []
date = 2020-06-19T23:00:00Z
description = "A second-year project that we completed over a three-month period."
description2 = "9 Persons Group Project"
itch = "https://uowmgames.itch.io/mind-wars"
image = "https://img.itch.zone/aW1nLzc2NjE1NzMucG5n/315x250%23c/2s4q95.png"
title = "Student Project: MindWar"
type = "post"

[[tech]]
logo = "https://1000logos.net/wp-content/uploads/2021/10/Unity-logo.png"
name = "Hugo"
url = "https://unity.com/"
[[tech]]
logo = "https://www.cdnlogo.com/logos/c/27/c.svg"
url = "https://unity.com/how-to/learning-c-sharp-unity-beginners"
+++

## Gameplay Screenshots

{{< img2 "/Portfolio/GPS2/mindwar01.png" "/Portfolio/GPS2/mindwar02.png">}}
{{< img2 "/Portfolio/GPS2/mindwar03.png" "/Portfolio/GPS2/mindwar04.png" >}}


## Trailer

{{< youtube "q6HVDigSZ48" >}}

## Game Description

{{<LP "Developed by StopFeeding Studios, Mind Wars is a strategy/auto-battler mobile game that takes major inspirations from auto-chess titles such as Teamfight Tactics and Dota Underlords.Set in the near-future, Players assume the role of the eponymous profession, healing illnesses both mental and physical by vanquishing evil viruses with their army of nanobots.">}}

## My Contribution 

### 1. Hexagon Generator
![](/Portfolio/GPS2/HexGenerator.png)

### 2. Spell Cards and Shop System
![](/Portfolio/GPS2/T_S_SC.gif)
### 3. Main Menu Camera System(Draggable Camera)
![](/Portfolio/GPS2/CameraSystem.gif)
### 4. Perks and Upgrades. 
![](/Portfolio/GPS2/PerkSystem.gif)

### 5. Instruction Page
![](/Portfolio/GPS2/Instruction.gif)

## The Challenges and Solutions
### 1. Hexagon Generator

![](/Portfolio/GPS2/HexagonGeneratorScript.png)

Platform procedure generator can be the most tricky parts that I handle in this project. Our level concept is proposed to be a procedure generator platform with a random enemy tower. Creating a procedure platform is not that hard. However, the tricky part is that in order to create a "good shape" of the platform like the above image, a complex formula will be needed to add inside the for loop function in order to determine the shape of the spawn location. 

Fortunately, a good YouTube reference of custom shape hex tile platform helped me a lot. Other than that, each of the hex tile positions will be needed to add into a List in order to achieve random tower and damage tile spawn.

{{< youtube "rjBD-4gNcfA" >}}
Credit:  Hexagon Calculation Formula Reference from Aeonic Softworks

### 2. Spell Cards and Shop System

#### Shop System

![](/Portfolio/GPS2/shop1.png)
The shop system is the second challenge I faced in this project. To ensure the item is randomized in a limited way(which means the player can get at least one robot unit and upgrade), a list of variables will be needed to determine the different types of shop items to spawn. 
![](/Portfolio/GPS2/shop2.png)
The most tricky part of the shop system would be buyCard function. Shop system contains a lot of different type of item such as spell card, robot unit and upgrade. An epic perks buff could even increase the item amount to 2 each time the player bought it. Therefore, a lot of conditions will need to check in order to actually achieve the function of each type of item.

#### Spell Card

![](/Portfolio/GPS2/Spellcard1.png)

In order to make the spell card function work(such as transforming the card from 2D screen to world space), ray tracing would be used to determine the object that collided.


![](/Portfolio/GPS2/Spellcard2.png)
Except for the fireball function was spawned and moved to the target, the other spell cards such as poison, heal and increase atk speed will spawn a sphere of collision to damage or increase the specific target's hp

### 3. Main Menu Camera System
![](/Portfolio/GPS2/CameraDragSolution.png)

A boolean was used to determine whether the camera rotation should auto-play or not. Other than that, the camera angle was clamped between two values when it is auto rotate. A coroutine was also used to determine the cooldown after the player stopped dragging the camera.

### 4. Perks and Upgrades. 
![](/Portfolio/GPS2/PerkandUpgradeScript.png)

A scripting API that Unity provides called PlayerPrefs is the key function that helps me get most of the upgrade and perks value to work easily.

![](/Portfolio/GPS2/PerkandUpgradeScript2.png)
The mana instance cool down, hp regenerate and robot shield perks could stand as individual functions but they still use PlayerPrefs to determine whether those functions can activate or not.

### 5. Instruction Page
![](/Portfolio/GPS2/Instruction2.png)

Instruction pages use the boolean to control the left and right swiping. The content array will be used to store the page UI reference and determine which page the player is located on and for smooth movement when swiping left and right. Another boolean CanMove was used to prevent players from spamming the swiping movement.

