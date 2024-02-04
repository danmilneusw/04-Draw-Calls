# 04-Draw-Calls
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

## Introduction
When drawing geometry to the screen, draw calls are generated. Draw calls tell the graphics API what needs to be drawn and how it should be drawn. Draw calls contain information like textures, shaders, and buffers. They can be resource instensive, especially the preparation required to generate the draw call.

In preparing for a draw call, the CPU alters settings on the GPU. These settings are collectively called the render state. Changes to the render state, such as switching to a different material, are the most resource-intensive operations Unity's graphics API performs...

...so we must optimise! Here's the ways Unity suggests to do this (taken from [here](https://docs.unity3d.com/Manual/optimizing-draw-calls.html#:~:text=A%20draw%20call%20tells%20the,as%20information%20about%20textures%2C%20shaders)):

- Reduce the total number of draw calls. When you decrease the number of draw calls, you also decrease the number of render-state changes between them.
- Organize draw calls in a way that reduces the number of changes to the render state. If the graphics API can use the same render state to perform multiple draw calls, it can group draw calls together and not need to perform as many render-state changes.

Optimizing draw calls and render-state changes has a number of benefits for your application. Mainly, it improves frame times, but it also:
- Reduces the amount of electricity your application requires. For battery-powered devices, this reduces the rate at which batteries run out. It also reduces the amount of heat a device produces when running your application.
- Improves maintainability of future development on your application. When you optimize draw calls and render-state changes earlier and maintain them at an optimized level, you can add more GameObjects to your scene without producing large performance overheads.

There's a few methods for optimising draw calls, some may be better for certain use-cases than others, so it's worth testing multiple methods. Today we'll focus on GPU Instancing, Static Batching, and Dynamic Batching. You can learn more about these techniques and about the other techniques [here](https://docs.unity3d.com/Manual/optimizing-draw-calls.html#:~:text=A%20draw%20call%20tells%20the,as%20information%20about%20textures%2C%20shaders).

In Unity, we can use the Frame Debugger to see exactly how the engine goes about rendering the scene to the player, you'll learn more about this profiling tool in tutorial 1.

## Summary
- Understand draw calls
- Learn how to use the Frame Debugger
- Learn about GPU Instancing
- Learn about Overdraw and Occlusion Culling

## Tutorials
You need to go to this directory and unzip the zip before opening Unity Project - GPU Instancing:<br>
"...\04-Draw-Calls\Unity Project - GPU Instancing\Assets\UnityTechnologies\Creator Kit - Beginner Code\Art\Texture\Buildings\Buildings_Albedo.zip"<br>
Sorry I had to do this to meet GitHub's file size limits. 

1. **GPU Instancing and the Frame Debugger.md**
2. **Overdraw and Occlusion Culling.md**

## Extra Resources
- [Catlike Coding Tutorial on Draw Calls](https://catlikecoding.com/unity/tutorials/custom-srp/draw-calls/) ⭐
- [Unleashing the Power of Unity Draw Calls Blog Post](https://bleedingedge.studio/blog/unleashing-the-power-of-unity-draw-calls/)
### Frame Debugger
- [Unity Docs - Frame Debugger](https://docs.unity.cn/Manual/frame-debugger-window-event-information.html) ⭐
### GPU Instancing
- [Unity Docs - GPU Instancing](https://docs.unity3d.com/560/Documentation/Manual/GPUInstancing.html) ⭐
- [Catlike Coding Tutorial](https://catlikecoding.com/unity/tutorials/rendering/part-19/Rendering-19.pdf) ⭐

Aside from GPU Instancing, there is also [Static Batching](https://docs.unity3d.com/Manual/static-batching.html) and [Dynamic Batching](https://docs.unity3d.com/Manual/dynamic-batching.html), but GPU Instancing, generally speaking, is the most powerful of the three.
