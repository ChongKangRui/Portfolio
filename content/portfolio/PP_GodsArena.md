+++
categories = ["pp-dev"]
coders = []
date = 2023-05-03
description = "An RPG Souls-Like Game created in Unreal Engine"
github = ["https://github.com/ChongKangRui/GodArena"]
image = "/Portfolio/GA/GATitle2.png"
title = "Personal Project: GodArena"
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

{{< img2 "/Portfolio/GA/s1.png" "/Portfolio/GA/s2.png">}}
{{< img2 "/Portfolio/GA/s3.png" "/Portfolio/GA/s4.png">}}


## Showcase

{{< youtube "wlK3sBi3Fzg" >}}


## Highlighting


### 1. Action Combat System

![](/Portfolio/GA/SystemDiagram.png)

The whole action combat system breaks down into three components: Action, Attribute, and Targeting. I built this system to be simple to use, easy to call C++ functions from blueprints, and aligned with the game's design goals.

-Action component: The Action Component manages all action behaviors for both AI and players. It handles executing, terminating, or canceling actions.
-Attribute component: The Attribute Component manages character stats like health, stamina, hit reactions, and blood spawn effects.
-Targeting component: The Targeting Component handles all the camera calculations, including smooth target following and angle calculations for switching between targets.

### 2. Action Component

#### Action

![](/Portfolio/GA/Action.png)

Action is the core of the Action Component and represents the actual behavior. All interactions happen inside the Action class. Two key functions in the base Action class are OnActionBegin and OnActionEnd, which handle the implementation of the action behavior. These get called whenever an action starts or ends.

![](/Portfolio/GA/ActionTimer.png)

I also added a custom SetTimer event in the action base class to simplify the timer function from Unreal's API.

#### Component

{{< img2 "/Portfolio/GA/characterDataTable.png" "/Portfolio/GA/Character_DatatableInitialization.png">}}

All actions are initialized at BeginPlay based on character type (player or enemy). The initialization reads from a data table where the user assigns actions to each character type enum.

{{< img2 "/Portfolio/GA/ExecuteAction.png" "/Portfolio/GA/TerminateAction.png">}}

Actions can be executed and terminated. For the player, these triggers are set up in blueprints. For AI, they fire as tasks inside the behavior tree based on the AI's current state.

![](/Portfolio/GA/ActionComponentDelegate.png)

I also added dynamic multicast delegates to the Action Component. This makes it easier to hook up functions quickly in blueprints. Whenever an action starts or ends, the system provides a reference to the active action, which gives more flexibility for other systems to respond. 

### 3. Attribute Component

![](/Portfolio/GA/AttributeGetter.png)

The attribute component will basically be responsible for some of the most important properties of a character like health, stamina and so on. First of all, it provides variable access for both blueprints and C++.

![](/Portfolio/GA/ApplyDamage.png)

Since the attribute component is managed health and stamina, it will also have a common function that applies the damage to the character that will be deducted to either health or stamina. This function will also be responsible for spawning blood vfx, applying an impulse to the character when they are being attacked. The actual function of applying damage was created in a functional library blueprint as a static function. Therefore, program don't need to take into account casting or getting component references whenever program try to apply damage to certain characters.

![](/Portfolio/GA/AttributeDelegate.png)

Like the Action Component, the Attribute Component also provides dynamic multicast delegates for a more flexible and convenient development environment.

### 4. Targeting Component

![](/Portfolio/GA/TargetingComponentStruct.png)

The Targeting Component uses a struct to manage mesh rotation, which was needed because the player can dodge or roll.

![](/Portfolio/GA/BeginTargetLogic.png)

When the player tries to target an enemy, the system runs a calculation first to pick the most eligible enemy before the actual targeting logic kicks in.

![](/Portfolio/GA/TargetingTickLogic2.png)

For the core camera rotation logic, I chose to calculate it step by step. This gave me more control over the entire process.

![](/Portfolio/GA/TargetingTickLogic.png)

This entire calculation runs inside a loop timer. The timer only activates when the player starts locking onto a target.

### 5. AI

![](/Portfolio/GA/AIExample.png)

The AI uses an enum character state to determine behavior. Debuffs like stuns or getting knocked to the ground get priority and will abort other behaviors. Aside from that, most AI behavior is handled by the Action Component.

![](/Portfolio/GA/AIExecuteActionTask.png)
![](/Portfolio/GA/AIExecuteAction.png)

Here's an example of how I tied the system to the AI. The AI simply executes an action from the action map. Once the action finishes, the task ends.

