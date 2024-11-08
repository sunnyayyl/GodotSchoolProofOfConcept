# Installation
Godot 4 can be downloaded from the [Godot website](https://godotengine.org/download).

> [!INFO] C# support
> In order to use C# alongside Godot, the *.NET* version is required

> [!WARNING] Other distribution method
> Despite Godot is available on [Steam](https://store.steampowered.com/app/404790), [Epic Game Store](https://store.epicgames.com/p/godot-engine) and system package manager. But they do not have the C# version, so the official download is recommended.
# Getting started
If you haven't used Godot before, you'll see the screen below:
![[Screenshot From 2024-11-08 20-34-13.png]]
Press the `+ Create` button on the toolbar to create a new project. A pop-up will appears as follow:
![[Screenshot From 2024-11-08 20-35-37.png]]
Set the desired project name and project path, then press `Create & Edit`.
![[Pasted image 20241108203719.png]]
# Godot Basics
> Check out the [offical documentation on the key concepts](https://docs.godotengine.org/en/stable/getting_started/introduction/key_concepts_overview.html)
# An Example
## The beginning
First, create a 2D scene
![[Pasted image 20241108204418.png]]
Your screen should looks like this
![[Pasted image 20241108204726.png]]
Clicking on the `Node2D` will populate your `Inspector` menu
![[Pasted image 20241108204921.png]]
These are property of the node that can be changed in the editor. By clicking on the `Node` tab, the content will change to the following: 
![[Pasted image 20241108205025.png]]
These are signal, they are used to do event-driven programming. Which will be used later.
We can rename the node by double clicking on the `Node2D` on the Scene list.
![[Pasted image 20241108205356.png]]
I've renamed it to World
Press `Ctrl-s` to save the scene.
![[Pasted image 20241108205513.png]]
## The player
### Nodes
We can add new node by clicking on the `+` button on the `Scene` tab
![[Pasted image 20241108205803.png]]
![[Pasted image 20241108205816.png]]
A collection of node is available here, for the player, we'll use the `CharaterBody2D`
![[Pasted image 20241108205905.png]]
![[Pasted image 20241108210119.png]]
A new node will pop up in the scene tree, and the editor nicely warned us about the lack of `CollisionShape`.
![[Pasted image 20241108210211.png]]
We can fix this warning by click on the `CharaterBody2D` and press the `+` button to add a new child node. 
![[Pasted image 20241108210338.png]]
Add a new `CollisionShape2D`, and then, add a `Sprite2D` too while we're at it.
![[Pasted image 20241108210441.png]]
The scene tree should now looks as follow:
![[Pasted image 20241108210535.png]]
_And another warning_
![[Pasted image 20241108210643.png]]This time, we have to create a shape for the `CollisionShape2D` node. But before fixing it, we should give the sprite a image.
We'll used the Godot icon for the player, and to use it as a sprite texture, we can drag the `icon.svg` in `FileSystem` tab 
![[Pasted image 20241108211047.png]]
into the `Texture` property in the `Inspector` tab
![[Pasted image 20241108211159.png]]
Your screen should now looks like this. We can now give our player its collision shape. Click on the `Collision2D` node and go to the shape property in the `Inspector` tab
![[Pasted image 20241108211319.png]]
Select the `RectangleShape2D`
![[Pasted image 20241108211402.png]]
A blue collision box should now appear in the editor, resize it to fit the size of the icon.

> [!hint] Snapping
> Enable `Grid Snapping` ![[Screenshot From 2024-11-08 21-16-48.png]] to help with fitting the box onto the icon

![[Pasted image 20241108211734.png]]
### Code
Now, we can actually start programming. To attach a script onto the player **click on the `CharaterBody2D` node**, then, press the attach script button on the `Scene` tab![[Pasted image 20241108211912.png]]
![[Pasted image 20241108211856.png]]
![[Pasted image 20241108212119.png]]
A pop-up will now appears, change the language to `C#` as follow:
![[Pasted image 20241108212132.png]]