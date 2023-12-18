+++
categories = ["pp-dev"]
coders = []
date = 2020-06-19T23:00:00Z
description = "An RPG Souls-Like Game created by Unreal Engine"
image = "https://res.cloudinary.com/samrobbins/image/upload/q_auto/v1591793276/logos/logos_hugo_h2xbne.svg"
title = "GodArena"
type = "post"
[[tech]]
logo = "https://cdn.icon-icons.com/icons2/2389/PNG/512/unreal_engine_logo_icon_144771.png"
name = "Unreal"
url = "https://www.unrealengine.com/en-US/"
[[tech]]
logo = "https://upload.wikimedia.org/wikipedia/commons/thumb/1/18/ISO_C%2B%2B_Logo.svg/1822px-ISO_C%2B%2B_Logo.svg.png"
name = "C++"
url = "https://learn.microsoft.com/en-us/cpp/cpp/?view=msvc-170"
+++

## Gameplay Screenshots

{{< img2 "/GPS2/mindwar01.png" "/GPS2/mindwar02.png">}}
{{< img2 "/GPS2/mindwar03.png" "/GPS2/mindwar04.png">}}


## Showcase

{{< youtube "_4FArgOX1I4" >}}


## Highlighting


### 1. Action Combat System

{{< img2 "/GPS2/mindwar03.png" "/GPS2/mindwar04.png">}}

The whole action combat system can basically be split into three components: Action Component, Attribute Component and Targeting Component. The purpose of this system is to make it simple to use, easier to construct build-in C++ functions in the blueprint and fit the design purpose of this game.

-Action component: Manage all action behaviour that applies to both AI and Player. Involve execute, terminate or abandon the action.
-Attribute component: Manage all attributes for a character such as health, stamina, hit reaction, blood spawn etc.
-Targeting component: Do all the calculations for smooth camera targeting move, switch target angle calculation, etc.

### 2. Action Component

#### Action

Action.png

Action is the core of the action component which represents action behavior. All of the interactions will be done in Action class.  Two functions in the base Action class are called OnActionBegin and OnActionEnd will be the implementation of action behavior. These two functions will called whenever the action begin and end trigger.

ActionTimer.png

In the action base class, I also create a custom SetTimer event to serve as simplification of the function.

#### Component

characterDataTable.png  Character_DatatableInitialization.png

All of the actions will be initialized at the BeginPlay based on our character type (player type and enemy type). The action initialization will be based on the map that we set in the datatable with the specific character type enum. 

ExecuteAction.png  TerminateAction.png

The action can be used to execute which begin the action and terminate at the end of the action. Those execute and terminate triggers will be set in the blueprint for the player. For AI, it will trigger as a task in the behaviour tree based on the AI state.

ActionComponentDelegate.png

In the action component, the dynamic multicast delegate will also be provided for the flexibility of constructing functions quickly in the blueprint. Therefore, whenever an action is triggered or ends, it can always provide active action referencing for better flexibility. 

### 3. Attribute Component

AttributeGetter.png

The attribute component will basically be responsible for some of the most important properties of a character like health, stamina and so on. First of all, it provides variable access for both blueprints and C++.

ApplyDamage.png

Since the attribute component is managed health and stamina, it will also have a common function that applies the damage to the character that will be deducted to either health or stamina. This function will also be responsible for spawning blood vfx, applying an impulse to the character when they are being attacked. The actual function of applying damage was created in a functional library blueprint as a static function. Therefore, we don't need to take into account casting or getting component references whenever we try to apply damage to certain characters.

AttributeDelegate.png

The same thing with the action component, the attribute component also provides some dynamic multicast delegate for a flexible and convenient development environment.

### 4. Targeting Component

TargetingComponentStruct.png

For the Targeting component, a struct will be provided to manage the mesh rotation since the player was allowed to dodge or roll.

BeginTargetLogic.png

When the player is trying to target an enemy, a calculation will be done before the actual targeting logic happens in order to choose the enemy that is most eligible to be targeted.

TargetingTickLogic2.png

For the core logic of targeting camera rotation, I choose to calculate it step by step so that I can have more control over the whole calculation. 

TargetingTickLogic.png

Eventually, this whole calculation will go into a loop timer. This loop timer will only be active when the player start locking the target.

### 5. AI

AIExample.png

For the AI, is basically using an enum character state to determine what behaviour they would do. The debuff will be prioritised to abort the other behaviour whenever they get stunned or laid on the ground. Other than that, most of the AI behaviour will just be handled by the action component.

AIExecuteAction.png

One of the examples of how I tie the system with the AI. It will just execute a random action from the array.

