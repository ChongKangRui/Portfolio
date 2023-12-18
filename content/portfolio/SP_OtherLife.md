+++
categories = ["sp-dev"]
coders = []
date = 2020-06-19T23:00:00Z
description = "A final-year project that we completed over a six-month period."
description2 = "8 Persons Group Project"
itch = "https://uowmgames.itch.io/other-life"
image = "https://img.itch.zone/aW1nLzEwNjY0MDgwLnBuZw==/315x250%23c/ag3Ydf.png"
title = "Student Project: OtherLife"
type = "post"
[[tech]]
logo = "https://cdn.icon-icons.com/icons2/2389/PNG/512/unreal_engine_logo_icon_144771.png"
name = "Unreal"
url = "https://www.unrealengine.com/en-US/"
+++


## Gameplay Screenshots

{{< img2 "https://img.itch.zone/aW1hZ2UvMTY2NjY5Ni8xMDY2MjM5OS5wbmc=/347x500/koE76a.png" "https://img.itch.zone/aW1hZ2UvMTY2NjY5Ni8xMDY2MjQwMC5wbmc=/347x500/jJje%2Bc.png">}}
{{< img2 "https://img.itch.zone/aW1hZ2UvMTY2NjY5Ni8xMDY2MjQwNi5wbmc=/347x500/hZ4gDq.png" "https://img.itch.zone/aW1hZ2UvMTY2NjY5Ni8xMDY2MjQwMi5wbmc=/347x500/kEwxAP.png">}}


## Trailer

{{< youtube "G3N2SD9Dokc" >}}

## Game Description

{{<LP "Developed by Infinity Studios, Other Life is a first-person exploration game where you play as an alien explorer, sent out to scour the stars in search of new life.  After detecting a significant energy signature on a nearby planet, you and your trusty AI companion happen upon the remnants of an alien civilization, brought to ruin by an unknown catastrophe. Armed with unique light-based technology, explore and discover the truth behind this interstellar mystery.">}}


{{<LP "Explore the serenely derelict alien city and the lives of its lost people. Discover the workings behind the unique crystal technology of the Lumenites, and how it can relate to your own. Solve and overcome the many challenges left behind by a cataclysmic event. Venture into the core of the city and uncover the consequences of a great secret.">}}

## My Contribution 

### 1. Ai Companion
![](/FYP/AI.png)
{{< img2 "/FYP/AICompanionCollect.gif" "/FYP/DropBattery.gif">}}

collect and put in battery

{{< img2 "/FYP/AIPickingUp.gif" "/FYP/AICompanionPut.gif">}}

Picking Up and Dropping Down

### 2. Highlight and Scanning 
{{< img2 "/FYP/highlighting.png" "/FYP/highlighting2.png">}}

Highligting

![](/FYP/AIScaning.gif)

Scanning

### 3. Dialogue and Cinematic Text Transformation

{{< img2 "/FYP/AIDialogue.gif" "/FYP/CinematicTransformText.gif">}}

Gif and content

## The Challenges and Solutions
### 1. Ai Companion

#### AI Behavior Tree
![](/FYP/Aibehaviortree.png)

Except the behavior that used for final level, the behaviour enum will determine the ai behaviour. Based on the enum state, Ai companion will switch to different behaviour in order to help the player.

![](/FYP/AIEnumState.png)

Based on the player command, ai will switch the state according to the condition.

{{< img2 "/FYP/EQS.png" "/FYP/teleport.png">}}

Environment Query System was applied to not only the pathfinding but also the teleport system in order to get the most precise location and avoid getting stuck.

#### Pick up and Drop down Item

![](/FYP/pickupSolution.png)

In order to really pick up the object without having any problem, collision, gravity and pathfinding need to be handled properly.

![](/FYP/DropDown.png)

When dropped, the item should enable nav mesh, collision and physic instead. 


#### Collect and Put in battery

![](/FYP/Spawnbattery.png)

For the battery and generator, basically it will be determined by whether the target had the interface or not. Of course before spawning the battery, it will check whether the inventory have enough number of battery or not

### 2. Highlight and Scanning 

#### Highlight outline

![](/FYP/AngleFormula.png)

The angle calculation will basically involve the dot product and acos2 to get the radians, then transform it to degrees. By getting the degrees, we will be able to know whether the object or which object is interactive or not based on the player angle.

![](/FYP/HightilightingMaterial.png)

Highlighting can be one of the most tricky parts of this project. In order to properly highlight the mesh, the coordinate of the shape of the mesh will be needed and calculated. Fortunately, a tutorial resource from ParallelCube allowed us to handle the heavy calculation. 

![](/FYP/stencil.png)

The object that gonna to be highlighted will be determine by their stencil integer.

#### Scanning

![](/FYP/Scannermaterial.png)

The scanning effect could be slightly less tricky compared with highlighting outlines. Basically, we just need to get the centre of the scanner and multiply the texture with a sphere mask. By increasing the radians dynamically in material blueprint, a scan effect will be created from the centre of scanner to the maximum amount of scan distance. 

### 3. Dialogue and Cinematic Text Transformation

#### Dialogue

![](/FYP/DialogueAnimated.png)

The dialogue system basically uses an append to collect each character from the array inside a string and then display it one by one. 

#### Cinematic Text Transformation

![](/FYP/CTTA.png)

Cinematic Text Transformation will use a different approach to achieve the effect compared with the dialogue system. In order to transform from one font to another, each character will be an individual widget. All widgets will be assigned as a child of a horizontal box. Inside each of the char widgets, the font will be changed after a specific delay.



