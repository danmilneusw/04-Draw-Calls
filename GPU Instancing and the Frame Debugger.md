# GPU Instancing and the Frame Debugger
1. Open the Unity project called **Unity Project - GPU Instancing** and make sure you're on the scene called **ExampleScene**.

<div align="center">
  <a href="Images\1\ExampleScene.png" target="_blank">
    <img src="Images\1\ExampleScene.png" style="height:400px;"/>
  </a>
</div>
<br><br>

2. Open the Frame Debugger at Window > Analysis > Frame Debugger. The Frame Debugger is a profiling tool that lets you analyse a frame at runtime and view all the individual draw calls used to render it. You can view the draw calls chronologically too to see all the steps in how the frame is rendered. It will be blank for now.

<div align="center">
  <a href="Images\1\FrameDebugger.png" target="_blank">
    <img src="Images\1\FrameDebugger.png" style="height:400px;"/>
  </a>
</div>
<br><br>

3. In the Editor, run the game then, while the player is still in the spawn position, click Enable in the Frame Debugger. The game will pause and you will see a list of all the draw calls for the now paused frame on the left-side of the window. If your Frame Debugger doesn't look like below (with all the previews and information on the right-side), then you may need to build your project first. I had no problems with the Frame Debugger until recently it kept showing up blank, I think it may be a bug in older Unity versions. Go to File > Build and Run. Enable Development Build. Click Build And Run. Once it's running, select Enable in the Frame Debugger. You should see this:

<div align="center">
  <a href="Images\1\Build.png" target="_blank">
    <img src="Images\1\Build.png" style="height:400px;"/>
  </a>
</div>
<br><br>

<div align="center">
  <a href="Images\1\716 Draw Calls.png" target="_blank">
    <img src="Images\1\716 Draw Calls.png" style="height:400px;"/>
  </a>
</div>
<br><br>


4. You can move the slider at the top of the Frame Debugger to move from the first to last draw call. Just a reminder: these are all the draw calls the CPU has sent to the GPU to perform to render this frame. They contain all the information the GPU needs to render, like information about textures, shaders, and buffers. All this information is called the "Render State".

5. Remember how we said that to optimise we should reduce the number of changes to the render state? Right now, I've placed loads of barrels at the spawn point to exagerate this point. Take a look at the calls. At around the 500th call you should be able to see all of these barrels being drawn individually. Luckily we can use a technique called GPU Instancing to draw them all at once!

<div align="center">
  <a href="Images\1\Material GPU Instancing Not Enabled.png" target="_blank">
    <img src="Images\1\Material GPU Instancing Not Enabled.png" style="height:400px;"/>
  </a>
</div>
<br><br>

6. So, firstly, how does GPU Instancing work? It has only come about recently thanks to the power of modern GPUs. It lightens the load on the CPU by making it send only a single draw call to the GPU with information to draw the same mesh multiple times. Essentially, modern GPUs can handle much more complex draw calls than they used to, meaning the CPU doesn't need to make multiple draw calls - we can just combine a lot of draw calls into one, which is easily done when the meshes for the object match. That's why for Unity's GPU Instancing, only multiple copies of the same mesh can be used with this technique. GPU Instancing is often a great option, it's useful for drawing things that appear multiples times in a scene like trees. However, when using this technique on integrated graphics cards GPU Instancing may come with negative performance gains.<br><br>This is a fairly high-level explanation. If you use this technique in your assignment, do some research and find some references to explain better the theory of what goes on behind-the-scenes for higher marks!<br><br>For reference, I have a total of 716 draw calls currently. You will see that if you select one of the barrels in the Frame Debugger (e.g Draw MeshBreakableBarrel (72)), it will say "The material doesn't have GPU instancing enabled" (like in the image above).<br><br>To enable GPU Instancing for all our barrels, select any one of the barrels in the inspector, then under Barrel_Special (Material) select Enable GPU Instancing.

<div align="center">
  <a href="Images\1\Enable GPU Instancing.png" target="_blank">
    <img src="Images\1\Enable GPU Instancing.png" style="height:400px;"/>
  </a>
</div>
<br><br>

7. Run the Frame Debugger again, how many draw calls do you now have? I have 429, a reduction in 487 calls (716-229).

<div align="center">
  <a href="Images\1\Reduce Draw Calls.png" target="_blank">
    <img src="Images\1\Reduce Draw Calls.png" style="height:400px;"/>
  </a>
</div>
<br><br>

8. But how does this affect performance? Open the other scene called **ManyBarrels**. This scene is a copy of the previous but just a load of barrels, so you should see performance gains more clearly.

<div align="center">
  <a href="Images\1\Many Barrels Scene.png" target="_blank">
    <img src="Images\1\Many Barrels Scene.png" style="height:400px;"/>
  </a>
</div>
<br><br>

9. You've used the Profiler plenty now so this part is down to you (but please ask if you have any questions). Profile this scene with GPU Instancing not enabled. Profile it with it enabled. What is the total time spent on the CPU and GPU in both cases? What is using the GPU when GPU Instancing is not enabled, and why is GPU usage less when GPU Instancing is enabled?


Quick screenshot of my results for reference:
- Initial Profile
<div align="center">
  <a href="Images\1\Profiler GPU I Not Enabled.png" target="_blank">
    <img src="Images\1\Profiler GPU I Not Enabled.png" style="height:400px;"/>
  </a>
</div>
<br><br>

- GPU Instancing Enabled
<div align="center">
  <a href="Images\1\Profiler.png" target="_blank">
    <img src="Images\1\Profiler.png" style="height:400px;"/>
  </a>
</div>
<br><br>

10. With this knowledge you will be able to know how many draw calls are being generated per frame, how to reduce them, how much you reduced them by, and see how this impacted performance :)