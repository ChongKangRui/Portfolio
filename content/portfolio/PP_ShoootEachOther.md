+++
categories = ["pp-dev"]
coders = []
date = 2023-12-05
description = "A Third Person Space Shooter Game created by Unreal Engine"
github = ["https://github.com/ChongKangRui/ShootEachOther"]
image = "/Portfolio/SEO/GSS/Icon.png"
title = "Personal Project: ShootEachOther"
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

## Gameplay Screenshots

{{< img2 "/Portfolio/SEO/GSS/s1.png" "/Portfolio/SEO/GSS/s2.png">}}
{{< img2 "/Portfolio/SEO/GSS/s3.png" "/Portfolio/SEO/GSS/s4.png">}}


## Showcase

### Singleplayer Showcase

{{< youtube "5LIx0SD7U9o" >}}

### Multiplayer Showcase

{{< youtube "0tDU1JKGjUg" >}}

## Highlighting


### 1. Gameplay Ability System


The core logic of Gameplay Ability System was reference from Lyra project.

#### Gameplay Ability Binding

The core setup will require two struct. 

![](/Portfolio/SEO/GAS/GAS_AbilityStructBinding.png)

The first struct will be used to determine the ability granted to the Gameplay Ability System. Each weapon will grant or remove their ability when player swapping weapon. Same ability may contain different of ability level for different weapon as well.

![](/Portfolio/SEO/GAS/GAS_AbilityInputBinding.png)

The second struct will be used to bind Gameplay Tag into input action.

![](/Portfolio/SEO/GAS/GAS_BindAbility.png)

{{< LP "These two function will be the core function to bind the ability with Enhanced Input Component.">}}
{{< LP "BindNativeAction will be used to bind the functionality that not belong to Gameplay Ability System such as Character and Camera Movement.">}} 
{{< LP "BindAbilityActions will be used to bind the functionality(Gameplay Ability) that will grant to Gameplay Ability System. More detail will be explained in the next two session. ">}}

#### Gameplay Ability Input

![](/Portfolio/SEO/GAS/GAS_AbilityInput.png)

{{< LP "These two function will be bound to the input action by using BindAbilityActions function. ">}}

{{< LP "Whenever player press any input button that was bound with GameplayTag, AbilityInputTagPressed will search the granted ability, add it into InputPressedSpecHandle and InputHeldSpecHandle. ">}}

{{< LP "Whenever player release any input button that was bound with GameplayTag, AbilityInputTagReleased will search the granted ability, add it into InputReleasedSpecHandle and remove from InputHeldSpecHandle. AbilitySpecHandle will be removed from InputPressedSpecHandle during the gameplay ability execution as well.">}}


#### Gameplay Ability Execute

![](/Portfolio/SEO/GAS/GAS_ProcessAbility_1.png)

{{< LP "It is time to talk about the process of how the ability activate. The ability that held in InputPressedSpecHandle and InputHeldSpecHandle will being loop and added into the AbilityToActivate array.">}}

![](/Portfolio/SEO/GAS/GAS_ProcessAbility_2.png)

{{< LP "A forloop will be used to activate all the ability. InputReleasedSpecHandle will only be triggered after all the valid ability activate.">}}

#### Gameplay Ability Base

![](/Portfolio/SEO/GAS/GAS_BaseAbility.png)

{{< LP "Gameplay Ability Base is the basic class of the Gameplay Ability. It contain the general function for derived ability classes to get the necessary reference.">}}

![](/Portfolio/SEO/GAS/GAS_ListAbility.png)

Here is a list of Gameplay Ability that I created and applied in this project. Critical gameplay functionality was done and replicated inside these Gameplay Ability as well. For more detail functionality, feel free to check the Github link.

### 2. Weapon

![](/Portfolio/SEO/Weapon/WeaponInventory.png)

{{< LP "A WeaponInventoryComponent will be used to manage all the weapon related data. Each weapon will represent as an UObject called Weapon Instance. WeaponInventoryComponent will be responsible for switching between weapon as well. ">}}

![](/Portfolio/SEO/Weapon/WeaponInventory_WeaponStruct.png)

{{< LP "A struct that used to represent each weapon slot. There will be 4 weapon slots: ">}}

{{<LP " Slot 1 - Main Weapon ">}}
{{<LP " Slot 2 - Secondary Weapon ">}}
{{<LP " Slot 3 - Melee Weapon ">}}
{{<LP " Slot 4 - Throwable Weapon ">}} 

#### Weapon Instance
![](/Portfolio/SEO/Weapon/WeaponInstance.png)

{{< LP "Weapon Instance is an UObject that used to store the weapon data, such as Max Ammo and Current Ammo. Ammo will store inside gameplay tag base container. Weapon Instance is also responsible to tell the Gameplay Ability system which weapon ability should granted. ">}}

![](/Portfolio/SEO/Weapon/WeaponInventory_ReplicateUOBject.png)

{{< LP "In the weapon inventory, Weapon Instance will be replicated as well so each client can know the weapon data. ">}}

![](/Portfolio/SEO/Weapon/ExampleUI01.png)
![](/Portfolio/SEO/Weapon/ExampleUI02.png)

Here are the example of how the Interface will be look like over the data table.

### 3. Match Rule System

Now let talk about the match system and how it work.

![](/Portfolio/SEO/GameMode/GameMode_AssignPlayerToTeam.png)

{{< LP "Whenever a new player joins the host, Game Mode will assigne them to one of the teams based on whichever team has fewer players. They are also allow to switch between team and add new AI to their team.">}}

![](/Portfolio/SEO/GameState/MatchSystem_AssignplayerTo.png)

{{< LP "Game State will store all the team information and also responsible for the actual functionality of assign player into team.  ">}}

![](/Portfolio/SEO/PlayerState_Attribute.png)

{{< LP " It is worth to mention the Player State as well since it also storing important data of the player such as player name, their current money and player ID. ">}}