+++
categories = ["cp-dev"]
coders = []
date = 2023-05-04
description = "A third-person multiplayer shooter game created by using Unreal Engine"
image = "/Portfolio/MouthzipIcon.png"
title = "Commercial Project: NDA Project"
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

{{< LP "My contribution to this project focused primarily on the AI systems. I implemented two AI agents, each with their own behaviors and decision-making logic. I also developed several supporting gameplay features that integrated directly with these AI systems to create a cohesive player experience.">}}

### 1. AI with a simple attack style

{{< LP " The first AI was straightforward, with simple attack behavior. However, due to the network replication system used to synchronize SFX, animations, and behavior states, even this simple AI presented unique challenges during development.">}}

### 2. AI with 6 different weapon and complex behavior

{{< LP "The second AI was far more complex, featuring a wide range of behaviors. It had access to three ranged weapons and three melee weapons, each with its own unique special attack. On top of that, this AI could summon the first AI or heal itself independently. Balancing all these behaviors while ensuring everything worked properly with the replication system significantly increased the difficulty of development. ">}}


{{< LP "In terms of the behaviour tree module, I eventually made the AI start with a default behaviour tree module that contains investigate, patrolling, summon first AI and ranged weapon behaviour. However, when the AI belongs to the melee weapon behaviour, it will switch from the default behaviour tree to another behaviour tree module when It activates combat mode. Vice versa, when it is quit combat mode, the behaviour tree will switch back to default.">}}

{{< LP "Last but not least, since this AI will decide its combat type at the beginning of the game, it is important to set replication properly for the animation blueprint and spawn the correct weapon since I do encounter a lot of problems with synchronization between server and client. The final solution that I explored was to let the weapon variable be replicated but set and spawn the weapon only on the server side. This AI is one of the most challenging parts that I have encountered since there is a lot of logic between AI and replication systems to consider. ">}}

### 3. General Gameplay features
#### Synchronization score between server and client 

{{< LP "For score synchronization, I used the same approach as the AI weapon spawn. All scores are set on the server and then replicated to the client side. The tricky part was that I had to handle the data sync inside the player blueprint instead of the widget, since widgets don't support replication. Each widget exists only for the server or the client, never both.">}}

#### Hand offset for the more precise holding gun position

{{< LP "During the project, we ran into an issue where the holding gun animation didn't match the gun model properly. The hand position looked unnatural and off. To fix this, I created adjustable values for each character to tweak the left hand IK by modifying the bone transform directly. These values are stored in a data table as part of each character's properties, making them easy to adjust per character.">}}