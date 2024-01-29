# Overdraw and Occlusion Culling
Another way to reduce the number of draw calls is to have less to display. You are probably familiar with Frustrum Culling, typically just referred to as "culling", where only what is in the field-of-view of the camera is rendered whereas everything else is not, but occlusion culling takes this idea further. Rather than just what is in the FOV being rendered, the occlusion is assessed to see if their is an object blocking another object. In this case, we don't need to render the object that is behind an object if we can't see it, even if it is in the FOV.

1. Open the project. Let's assess how bad our 'overdraw' is. This is the amount of objects being rendered behind other objects. Perhaps from the image below you can already see how it works.

<div align="center">
  <a href="Images\2\Unity Overdraw Example.png" target="_blank">
    <img src="Images\2\Unity Overdraw Example.png" style="height:200px;"/>
  </a>
</div>
<div align="center">
  <a href="https://unity.com/resources/ultimate-guide-to-profiling-unity-games">
  source
  </a>
</div>

2. Position your Scene camera (the one you use, not the in-game camera) and select the Overdraw option in the dropdown on the right. You will see that brighter areas indicate where overdraw is more prevalent, as this is where objects are being drawn on top of one another.

<div align="center">
  <a href="Images\2\Applying Overdraw.png" target="_blank">
    <img src="Images\2\Applying Overdraw.png" style="height:400px;"/>
  </a>
</div>
<br><br>

3. We're going to apply occlusion culling to fix this. Go to Window > Rendering > Occlusion Culling. Then select all of the cubes in the hierarchy and in the inspector make them static by ticking the box and make sure Occluder Static and Occludee Static are active via the dropdown.

<div align="center">
  <a href="Images\2\Defining Ocludees and Ocluders.png" target="_blank">
    <img src="Images\2\Defining Ocludees and Ocluders.png" style="height:400px;"/>
  </a>
</div>
<br><br>

4. Go back to the Occlusion window (next to the Inspector). If you click the Visualization tab, you'll see no occlusion data is baked yet and our scene has no occlusion. 

<div align="center">
  <a href="Images\2\No Occlusion Yet.png" target="_blank">
    <img src="Images\2\No Occlusion Yet.png" style="height:400px;"/>
  </a>
</div>
<br><br>

5. Select the Bake tab and, using the default values, click the Bake button at the bottom of the window.

<div align="center">
  <a href="Images\2\Bake.png" target="_blank">
    <img src="Images\2\Bake.png" style="height:400px;"/>
  </a>
</div>
<br><br>

6. Go to the Visualization tab and you'll see some occlusion culling in action...

<div align="center">
  <a href="Images\2\Occlusion in Action.png" target="_blank">
    <img src="Images\2\Occlusion in Action.png" style="height:400px;"/>
  </a>
</div>
<br><br>

7. But this appears to be doing standard culling. We expect the cubes to the left to be culled out also as the Main Camera can't see them. In the Bake tab, if you set the values to:
- 0.1
- 0.1
- 5

You'll get some occlusion culling (very left cubes are gone).

<div align="center">
  <a href="Images\2\Improved Occlusion Culling.png" target="_blank">
    <img src="Images\2\Improved Occlusion Culling.png" style="height:400px;"/>
  </a>
</div>
<br><br>

8. For this scene, you should be able to improve occlusion culling drastically by changing these values (I know because I've tested it). I'll leave it up to you to research what might be the best values. You can learn some more about them here, which might be a good reference if you plan to include Occlusion Culling in your report for the assignment: https://docs.unity3d.com/Manual/occlusion-culling-window.html#:~:text=When%20you%20select%20a%20Camera,view%20to%20configure%20the%20visualization.

9. Finally, test if occlusion culling improves the number of draw calls using the Frame Debugger.