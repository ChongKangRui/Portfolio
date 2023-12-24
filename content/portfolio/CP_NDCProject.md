+++
categories = ["cp-dev"]
coders = []
date = 2020-06-19T23:00:00Z
description = "A third-person multiplayer shooter game created by using Unreal Engine"
image = "https://www.indiafilings.com/learn/wp-content/uploads/2018/03/Non-Disclosure-Agreement-Template.jpg"
title = "NDA Project"
type = "post"
[[tech]]
logo = "https://cdn.icon-icons.com/icons2/2389/PNG/512/unreal_engine_logo_icon_144771.png"
name = "Unreal"
url = "https://www.unrealengine.com/en-US/"
+++

## Gameplay Screenshots

{{< img2 "/Portfolio/asset/s1.png" "/Portfolio/asset/s2.png">}}

{{< img2 "/Portfolio/asset/s3.png" "/Portfolio/asset/s4.png">}}


## My Contribution & Challenging

{{< LP "My contribution to this project was mainly the AI. I created two AI and some gameplay features.">}}

### 1. AI with a simple attack style

{{< LP "The first AI was an uncomplicated AI with simple attack behaviour. However, considering the network replication system to synchronize sfx, animation and correct behaviour state, it can add some challenges to this AI creation.">}}

### 2. AI with 6 different weapon and complex behavior

{{< LP "The second AI was a complex AI with a variety of behaviours. Consider this AI to have three ranged and three melee weapons, each with its own special attack behaviour, and this AI can even summon the first AI or heal itself on its own. This increases the difficulty of producing AI behaviour while considering the replication system. ">}}


{{< LP "In terms of the behaviour tree module, I eventually made the AI start with a default behaviour tree module that contains investigate, patrolling, summon first AI and ranged weapon behaviour. However, when the AI belongs to the melee weapon behaviour, it will switch from the default behaviour tree to another behaviour tree module when It activates combat mode. Vice versa, when it is quit combat mode, the behaviour tree will switch back to default.">}}

{{< LP "Last but not least, since this AI will decide its combat type at the beginning of the game, it is important to set replication properly for the animation blueprint and spawn the correct weapon since I do encounter a lot of problems with synchronization between server and client. The final solution that I explored was to let the weapon variable be replicated but set and spawn the weapon only on the server side. This AI is one of the most challenging parts that I have encountered since there is a lot of logic between AI and replication systems to consider. ">}}

### 3. General Gameplay features
#### Synchronization score between server and client 

{{< LP "The score synchronization between the server and client will follow the same concept as the AI weapon spawn. All of the scores will be set on the server and replicated on the client side. The data synchronization has to be done in the player blueprint instead of the widget since the widget doesn't provide replication functionality. Each widget was a sole object for either the server or the client.">}}

#### Hand offset for the more precise holding gun position

{{< LP "During this project, one of the problems that we encountered was that the holding gun animation and the gun were not matched correctly. The hand itself is not natural and precise in terms of holding a gun. Therefore, to make the hand IK more precise and natural, I have created the value for each character to modify the IK value in the left hand IK by modifying the bone transform directly. This value will be changeable in the data table as part of the character property.">}}