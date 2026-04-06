+++
categories = ["pp-dev"]
coders = []
date = 2025-05-04
description = "A Third Person Space Shooter Game created in Unreal Engine"
github = ["https://github.com/ChongKangRui/SpaceShooter_3D"]
image = "/Portfolio/SpaceShooter/icon.png"
title = "Personal Project: Space Shooter 3D"
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

{{< img2 "/Portfolio/SpaceShooter/s1.png" "/Portfolio/SpaceShooter/s2.png">}}
{{< img2 "/Portfolio/SpaceShooter/s3.png" "/Portfolio/SpaceShooter/s4.png">}}


## Showcase

{{< youtube "yjvAkOBcw6M" >}}


## Highlighting


### 1. PathFinding

![](/Portfolio/SpaceShooter/Pathfinding/Showcase.png)

{{< LP "The pathfinding algorithm that was applied in this project was the A* algorithm. Here is a very good educational video that helped me have a better understanding of how the A* algorithm works and also served as a reference for this project.">}}

{{< youtube "p3WcsO6pAmU" >}}

#### PathGrid

![](/Portfolio/SpaceShooter/Pathfinding/GenerateGrid.png)

{{< LP "Pathfinding grid is the core pathfinding component that acts like a NavMeshBoundsVolume. A set of node data will be generated and stored as a 3-dimensional index.">}}

![](/Portfolio/SpaceShooter/Pathfinding/AStarNodeStruct.png)
![](/Portfolio/SpaceShooter/Pathfinding/AStarNodeStruct2.png)
![](/Portfolio/SpaceShooter/Pathfinding/AStarGrid_SpawnNode.png)

{{< LP "Node data is a struct that stores the world location, its own coordinate (the index representation in 3-dimensional array), the node status, the neighbor nodes index and tracking moving player. When a node was spawning, a collision check would happen in order to know if anything was blocking the node location, avoid the unavailable node bring into consideration of path finding algorithm.">}}

#### AStarAgentComponent

{{< LP "After the foundation of the path finding was build, it is time to make AI move which is where I implemented the A* Algorithm. Before I start showcase about the core logic of algorihtm, let me introduce another struct that will be used in this algorithm">}}

![](/Portfolio/SpaceShooter/Pathfinding/RealTimeNodeData.png)

{{< LP "FAstarNodeData is a struct that is used to construct the path from the start location to the end location. It stores the GCost (represent the cost from last node to this node), FCost (represent the cost from start node to this node), camefrom node index, the current node pointer and also time to reach.">}}

![](/Portfolio/SpaceShooter/Pathfinding/AgentComponent_MoveTo.png)

{{< LP "MoveTo is the core logic function that make the AI move. Before A* algorithm start, system will define the start node and end node based on current AI location. GetClosestNode() convert the world location into node coordinate to so the program will know the node explicitly without looping through the node dimension array.">}}

![](/Portfolio/SpaceShooter/Pathfinding/MoveToCore.png)

{{< LP "Once start node and end node was defined, A* algorithm will start. OpenList will be the list that used to store all the potential node to travel while ClosedList will be final list that gonna used to construct the path. A local variable CurrentNodeData will be used to define the current start node location and store inside the ClosedList . ">}}


![](/Portfolio/SpaceShooter/Pathfinding/MoveToCore2.png)

{{< LP "Next, start a while loop, keep looping until either there is no potential node or the program finds the Goal Node. The first OpenList element will be decided as the current node. Note that the first element of OpenList will always be the lowest cost node to travel. ">}}

![](/Portfolio/SpaceShooter/Pathfinding/MoveToCore3.png)

{{< LP "If the current node is valid, start finding the next node with the neighbor node. If the neighbor node is valid and passes every false check, the program will continue to the next process of calculating navigation cost.">}}


![](/Portfolio/SpaceShooter/Pathfinding/MoveToCore4.png)

{{< LP "Here, the program starts calculating the navigation cost. The navigation cost will be affected by DirectionChangePenalty and Distance. Both of the values will decide the GCost value and eventually affect the navigation since navigation construction will always require choosing the shortest and lowest cost path.">}}

{{< LP "It is worth mentioning the effect of DirectionChangePenalty is to prevent and eliminate the chance of navigation that is against the current path direction. It will try to provide a smooth and natural path.">}}

{{< LP "After Neighbour Data finish setup, if neighbour not been passed through by the previous iteration, this node should be stored into OpenList and ClosedList. Then Heaptify function will put the lower cost node as first element in the OpenList. ">}}


![](/Portfolio/SpaceShooter/Pathfinding/MoveToCore5.png)

{{< LP "Finally, the program starts a new iteration. If the current node is goal node, path will reconstruct and pass into the GameThread for AI to move.">}}


#### Reconstruct

![](/Portfolio/SpaceShooter/Pathfinding/ReconstructPath.png)

{{< LP "In the ReconstructPath function, the path will construct by starting with the goal node and tracking back the came from node until it meets the begin node. Over the ReconstructPath function, it will notice the path grid that each node will be occupied by the agent and also their arrival time. ">}}

![](/Portfolio/SpaceShooter/Pathfinding/BezierPath.png)

{{< LP "In order to have a smooth path, bezier curve will be applied to agent vector output.">}}


#### Optimization

{{< LP "Optimization is very crucial and one of the very first problems I encounter after finishing the pathfinding algorithm. The navigation iteration will increase along with the detail of pathfinding and the number of node in the path grid. The heavy iteration can even block the game thread during early development. Therefore, in order to increase the iteration speed and make sure the heavy iteration won't block the game thread, heapify and multithreading were applied to the navigation system.">}}

##### 1. MultiThreading

{{< LP "This is the very first time that I actually applied multithreading in Unreal Engine. My past experience was mostly related to gameplay, AI and feature development, multithreading wasn't a necessary tool. However, to implement such a heavy looping algorithm, moving this process to the background thread seems to be a logical approach to increase speed and efficiency.">}}

##### 2. Heapify

![](/Portfolio/SpaceShooter/Pathfinding/Heapify.png)

{{< LP "Other than multithreading, the second tool that I used was Heapify. The purpose of this function was to find the lowest cost node and put it on top of the list. Initially, FindByPredicate function was used to find the lowest cost but it was too slow. So in the end, it was being replaced by the Heapify function which is much faster than the FindByPredicate.">}}

### 2. Spaceship Character

![](/Portfolio/SpaceShooter/Character/CharacterBase.png)

{{< LP "Spaceship Character, the base class of both player and enemy class. It contain the general function of character such as: ">}}
###### Weapon Shooting

###### Health and Damage Taken Feature

###### Mesh setup


#### Player

![](/Portfolio/SpaceShooter/Character/PlayerClass.png)

{{< LP "The notable part of player class is the smooth rotation of character and smooth FOV of the camera. The FOV of the camera will fit with the speed of the character. The rotation of player spaceship will ignore gimbal lock, so players are allowed to rotate pitch and roll 360 degrees.">}}

#### Enemy

![](/Portfolio/SpaceShooter/Character/ShootDirection.png)

{{< LP "The only part different for enemy will be the different output of shoot direction. Enemy also possess the AStarAgentComponent so enemy was allowed to move freely in 3D space pathfinding. ">}}


#### Data Management

![](/Portfolio/SpaceShooter/Character/AIAndPlayerData.png)

The character stat, weapon variable and mesh will be managed in Data Table.
