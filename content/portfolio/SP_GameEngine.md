+++
categories = ["sp-dev"]
coders = []
description = "A Simple Game Engine that created during my college time."
github = ["https://github.com/ChongKangRui/Simple-Game-Engine"]
image = "https://st4.depositphotos.com/27269280/29686/v/450/depositphotos_296865646-stock-illustration-game-engine-logo-game-logo.jpg"
title = "Student Project: Game Engine"
type = "post"
[[tech]]
logo = "https://upload.wikimedia.org/wikipedia/commons/thumb/1/18/ISO_C%2B%2B_Logo.svg/1822px-ISO_C%2B%2B_Logo.svg.png"
name = "C++"
url = "https://learn.microsoft.com/en-us/cpp/cpp/?view=msvc-170"
[[tech]]
logo = "https://miro.medium.com/v2/resize:fit:1024/1*9ACZQhVgQfbpX0aJ9PO7gQ.png"
name = "OpenGL"
url = "https://www.glfw.org/"
+++

## Engine Showcase

{{< youtube "mMfNs28PuOM" >}}

## Highlighting

In this project, I learned about the most basic concept of game engine structure and I also require to use it to create a simple game.

### 1. Entity Component System

{{< img2 "/Portfolio/SGE/ECSSystem.png" "/Portfolio/SGE/GameObjectComponent.png" >}}

This project have a simple Entity Component System where a gameobject class that was able to attach the component to it.

### 2. Input System

![](/Portfolio/SGE/InputSystem.png)
![](/Portfolio/SGE/InputSystemEnum.png)

This project also have it own input system where it will convert all of the opengl keycode into input system own enum.

### 3. Level System

![](/Portfolio/SGE/LevelSystem.png)

A level system will be required as well. SceneManager will be responsible to manage all of the level and scene is responsible to manage all of the game object.

### 4. Transform and Sprite Renderer Component

{{< img2 "/Portfolio/SGE/TransformC.png" "/Portfolio/SGE/SimpleSpriteRenderer.png" >}}

Lastly, a transform and sprite renderer component will be used to manage the object transform and render the sprite texture.
