# Installation
## Godot
Godot 4 can be downloaded from the [Godot website](https://godotengine.org/download).

> [!INFO] C# support
> In order to use C# alongside Godot, the *.NET* version is required

> [!WARNING] Other distribution method
> Despite Godot is available on [Steam](https://store.steampowered.com/app/404790), [Epic Game Store](https://store.epicgames.com/p/godot-engine) and system package manager. But they do not have the C# version, so the official download is recommended.
## Rider
You can use any IDE that support C#, including Visual Studio Code, but I personally prefer Rider. It is recommended to download [Jetbrains Toolbox](https://www.jetbrains.com/toolbox-app/) to manage all your Jetbrains IDE.

> [!important] Free Educational Licenses
> Student and teacher can obtain [free licence](https://www.jetbrains.com/community/education/#students/) to use Jetbrains IDE, but Rider is now free for non-commercial use.

# Getting started
If you haven't used Godot before, you'll see the screen below:
![[Screenshot From 2024-11-08 20-34-13.png]]
Press the `+ Create` button on the toolbar to create a new project. A pop-up will appears as follow:
![[Screenshot From 2024-11-08 20-35-37.png]]
Set the desired project name and project path, then press `Create & Edit`.
![[images/EditorWindow.png]]
# Godot Basics
> Check out the [offical documentation on the key concepts](https://docs.godotengine.org/en/stable/getting_started/introduction/key_concepts_overview.html)
# An Example
## The beginning
First, create a 2D scene
![[images/SceneTab.png]]
Your screen should looks like this
![[images/SceneTreeWithSingleNode2D.png]]
Clicking on the `Node2D` will populate your `Inspector` menu
![[images/InspectorTabForNode2D.png]]
These are property of the node that can be changed in the editor. By clicking on the `Node` tab, the content will change to the following: 
![[images/Node2DSignal.png]]
These are signal, they are used to do event-driven programming. Which will be used later.
We can rename the node by double clicking on the `Node2D` on the Scene list.
![[images/RenamedNode2DAsWorld.png]]
I've renamed it to World
Press `Ctrl-s` to save the scene.
![[images/SaveScene.png]]
## The player
### Nodes
We can add new node by clicking on the `+` button on the `Scene` tab
![[images/SceneTabSmall.png]]
![[images/NewNode.png]]
A collection of node is available here, for the player, we'll use the `CharaterBody2D`
![[images/CharaterBody2D.png]]
![[images/SceneTreeWithCharaterBody2D.png]]
A new node will pop up in the scene tree, and the editor nicely warned us about the lack of `CollisionShape`.
![[images/MissingCollisionShape.png]]
We can fix this warning by click on the `CharaterBody2D` and press the `+` button to add a new child node. 
![[images/CollisionShape2D.png]]
Add a new `CollisionShape2D`, and then, add a `Sprite2D` too while we're at it.
![[images/Sprite2D.png]]
The scene tree should now looks as follow:
![[images/NewSceneTreeWIthSpriteAndCollsionShape.png]]
_And another warning_
![[images/MissingShape.png]]This time, we have to create a shape for the `CollisionShape2D` node. But before fixing it, we should give the sprite a image.
We'll used the Godot icon for the player, and to use it as a sprite texture, we can drag the `icon.svg` in `FileSystem` tab 
![[images/FileSystemTab.png]]
into the `Texture` property in the `Inspector` tab
![[images/NewWindowWithSprite.png]]
Your screen should now looks like this. We can now give our player its collision shape. Click on the `Collision2D` node and go to the shape property in the `Inspector` tab
![[images/CollisionShapeShapeInspetor.png]]
Select the `RectangleShape2D`
![[images/CompletedPlayerEditorWindow.png]]
A blue collision box should now appear in the editor, resize it to fit the size of the icon.

> [!hint] Snapping
> Enable `Grid Snapping` ![[Screenshot From 2024-11-08 21-16-48.png]] to help with fitting the box onto the icon

![[images/ChangingCollisionShapeShape.png]]
### Code
Now, we can actually start programming. To attach a script onto the player **click on the `CharaterBody2D` node**, then, press the attach script button on the `Scene` tab![[images/AttatchScript.png]]
![[Pasted image 20241108211856.png]]
![[images/AttatchGDScript.png]]
A pop-up will now appears, change the language to `C#` as follow:
![[images/AttatchCSharp.png]]
![[images/GodotCSharpIDE.png]]
#### IDE
Godot have minimal C# support, so we'll do the C# programming on an external IDE, and in my case, Rider.
![[images/RiderWelcomeWindow.png]]
Your screen should looks similar to this, I've applied some plugin, for cosmetic purposes, so free free to play around with the setting. 
But more importantly, we now need to open the solution where the Godot project is located.

> [!tip] Forgot where your Godot project is?
> Go back to Godot and look for thr `FileSystem` tab and right click
> ![[images/ContextMenu.png]]
> Choose `Open in File Manager`
> You can now see where the Godot project is located in

After opening the project you will see the following screen
![[images/RiderWIndow.png]]
![[images/SolutionTab.png]]
Select the `CharaterBody2d.cs` 
![[images/RiderAndCode.png]]
#### The actual code
This is the built in template code for a `CharacterBody2D`
```c#
using Godot;  
using System;  
  
public partial class CharacterBody2d : CharacterBody2D  
{  
    public const float Speed = 300.0f;  
    public const float JumpVelocity = -400.0f;  
  
    public override void _PhysicsProcess(double delta)  
    {       Vector2 velocity = Velocity;  
  
       // Add the gravity.  
       if (!IsOnFloor())  
       {          velocity += GetGravity() * (float)delta;  
       }  
       // Handle Jump.  
       if (Input.IsActionJustPressed("ui_accept") && IsOnFloor())  
       {          velocity.Y = JumpVelocity;  
       }  
       // Get the input direction and handle the movement/deceleration.  
       // As good practice, you should replace UI actions with custom gameplay actions.       Vector2 direction = Input.GetVector("ui_left", "ui_right", "ui_up", "ui_down");  
       if (direction != Vector2.Zero)  
       {          velocity.X = direction.X * Speed;  
       }       else  
       {  
          velocity.X = Mathf.MoveToward(Velocity.X, 0, Speed);  
       }  
       Velocity = velocity;  
       MoveAndSlide();  
    }}
```

> [!NOTE] Type of process
> There are 2 type of process `_PhysicsProcess` and `_Process`:
> `_Process` is called _every frame_
> `_PhysicsProcess` is called _every physics frame_ which is by default 60 frame per second
> 
> The rules of thumb would to do everything that involve collision or physics, to make sure physics is consistent even when frame rate differ in `_PhysicsProcess`
> 
> And thing that need to be done smoothly _visually_ can be put in the `_Process`
> There's a lot of conversation on the internet about their difference, so feel free to do more research!
