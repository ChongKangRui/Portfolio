+++
categories = ["pp-dev"]
coders = []
date = 2023-12-05
description = "A Third Person Space Shooter Game created in Unreal Engine"
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

The core logic was referenced from the Lyra project.

#### Gameplay Ability Binding

The setup requires two structs.

![](/Portfolio/SEO/GAS/GAS_AbilityStructBinding.png)

The first struct determines which abilities are granted to the Gameplay Ability System. Each weapon grants or removes its abilities when the player swaps weapons. The same ability can also have different levels depending on the weapon.

![](/Portfolio/SEO/GAS/GAS_AbilityInputBinding.png)

The second struct binds Gameplay Tags to input actions.

![](/Portfolio/SEO/GAS/GAS_BindAbility.png)

{{< LP "These two functions are the core for binding abilities to the Enhanced Input Component.">}}
{{< LP "BindNativeAction handles functionality outside the Gameplay Ability System, like character and camera movement.">}} 
{{< LP "BindAbilityActions handles the actual Gameplay Abilities that will be granted to the system.">}}

#### Gameplay Ability Input

![](/Portfolio/SEO/GAS/GAS_AbilityInput.png)

{{< LP "These two functions get bound to input actions using BindAbilityActions. ">}}

{{< LP "When the player presses an input button bound to a Gameplay Tag, AbilityInputTagPressed searches for the granted ability and adds it to InputPressedSpecHandle and InputHeldSpecHandle.">}}

{{< LP "When the player releases the button, AbilityInputTagReleased searches for the ability, adds it to InputReleasedSpecHandle, and removes it from InputHeldSpecHandle. The AbilitySpecHandle also gets removed from InputPressedSpecHandle when the ability executes.">}}


#### Gameplay Ability Execute

![](/Portfolio/SEO/GAS/GAS_ProcessAbility_1.png)

{{< LP "Now for how the ability activates. Abilities held in InputPressedSpecHandle and InputHeldSpecHandle get looped through and added to an AbilityToActivate array.">}}

![](/Portfolio/SEO/GAS/GAS_ProcessAbility_2.png)

{{< LP "A for loop then activates all the abilities. InputReleasedSpecHandle only triggers after all valid abilities have been activated.">}}

#### Gameplay Ability Base

![](/Portfolio/SEO/GAS/GAS_BaseAbility.png)

{{< LP "The Gameplay Ability Base is the parent class for all gameplay abilities. It contains common functions for derived ability classes to grab necessary references.">}}

![](/Portfolio/SEO/GAS/GAS_ListAbility.png)

Here is a list of the Gameplay Abilities I created for this project. Critical gameplay functionality and replication were handled inside these abilities. For more details, feel free to check the GitHub link.

### 2. Weapon

![](/Portfolio/SEO/Weapon/WeaponInventory.png)

{{< LP "A WeaponInventoryComponent manages all weapon-related data. Each weapon is represented as a UObject called Weapon Instance. This component also handles switching between weapons.">}}

![](/Portfolio/SEO/Weapon/WeaponInventory_WeaponStruct.png)

{{< LP "A struct represents each weapon slot. There are four slots: Main Weapon, Secondary Weapon, Melee Weapon, and Throwable Weapon.">}}

#### Weapon Instance
![](/Portfolio/SEO/Weapon/WeaponInstance.png)

{{< LP "WWeapon Instance is a UObject that stores weapon data like max ammo and current ammo. Ammo is stored in a Gameplay Tag-based container. The Weapon Instance also tells the Gameplay Ability System which abilities should be granted for that weapon.">}}

![](/Portfolio/SEO/Weapon/WeaponInventory_ReplicateUOBject.png)

{{< LP "Inside the weapon inventory, Weapon Instance gets replicated so each client knows the weapon data.">}}

![](/Portfolio/SEO/Weapon/ExampleUI01.png)
![](/Portfolio/SEO/Weapon/ExampleUI02.png)

Here are the example of how the Interface will be look like over the data table.

### 3. Match Rule System

Now for the match system and how it works.

![](/Portfolio/SEO/GameMode/GameMode_AssignPlayerToTeam.png)

{{< LP "Whenever a new player joins the host, the Game Mode assigns them to the team with fewer players. Players can also switch teams and add new AI to their team.">}}

![](/Portfolio/SEO/GameState/MatchSystem_AssignplayerTo.png)

{{< LP "The Game State stores all team information and handles the actual logic for assigning players to teams.">}}

![](/Portfolio/SEO/PlayerState_Attribute.png)

{{< LP "It's also worth mentioning the Player State, which stores important player data like player name, current money, and player ID.">}}