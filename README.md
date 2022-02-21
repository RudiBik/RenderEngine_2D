# RenderEngine_2D

This repo contains a 2D render engine that is API independent and abstracts away the low level rendering details from the user. The following projects are contained in this repo:
- RI: The abstract low level render interface (mainly [IRenderSystem](Engine_and_PixelPop/Include/IRenderSystem.h) (Renderer interface + texture manager) and the [TextureHandle](Engine_and_PixelPop/Include/HandleMgr.h) class) and user friendly utility classes for rendering (e.g. a [Sprite](Engine_and_PixelPop/Include/Drawable/Sprite.h) class and text rendering class [Label](Engine_and_PixelPop/Include/Drawable/Label.h)). These utility classes use the main render interface themselves under the hood.
- RSD9: Dynamic library implementing the above interface using DirectX9 (mainly [D9RenderSystem](Engine_and_PixelPop/RI/RID9/D9RenderSystem.h) for the main interface and [D92DRenderer](Engine_and_PixelPop/RI/RID9/D92DRenderer.h) for low level rendering and managing vertex-/ and index-buffers.
- Pixelpop: A simple demo game to test the functionality of the render engine (Implementing the flashgame pixelpop from nitrome myself http://www.nitrome.com/games/pixelpop/) 


A video of the demo game using the engine with the DirectX9 implementation.

https://user-images.githubusercontent.com/16277721/154807967-a27a0de0-198a-455f-846a-034d8974c0f4.mov


The RI project is fully independent of any rendering API containing it's own classes for rendering configurations, vertices, rendering primitives, managing loaded images through handles, a texture manager and other details. This enables the implementation of the interface using different API's like DirectX or OpenGL and making it possible to decide at runtime which API to use for rendering (e.g. OpenGL on linux and DirectX on windows). In this repo only one implementation is provided using DirectX9.


## Running it
In the 'Engine_and_PixelPop\PixelPop' directory is a binary file 'PixelPop.exe' that represents the game. It can be configured using the Options.txt file in the same folder, e.g. changing resolution. 

This is a very old project (2015) from my bachelor time and sadly I couldn't get it to build again since I didn't document the versions of the used dependencies at that time. Luckily I kept the binary that I had build at that time :)


## Design
<table>
  <tr>
    <td><strong>Classes defining the low-level interface for rendering</strong></td>
    <td><strong>Utility classes for rendering that use the low-level interface themselves</strong></td>
  </tr>
  <tr>
    <td><img src="https://user-images.githubusercontent.com/16277721/154995749-8a6f4204-3567-40bd-ab1e-5a77a63926b7.png"></td>
    <td><img src="https://user-images.githubusercontent.com/16277721/154996276-84ddcbc5-a396-4c18-8588-a29419db6b51.png"></td>
  </tr>
</table>

<strong>Whole class diagram</strong>
- Left of the red bar: Rendering interface static library defining the interface and utility classes on top for rendering sprites, fonts, ...
- Right of the red bar: DirectX9 implementation of the interfaces in it's own dynamic library 
![whole](https://user-images.githubusercontent.com/16277721/154996572-4cb2aecd-f7a0-4fc0-bca5-81ca42c6cc01.png)


## References
This whole project is mainly about abstracting away details from the user making a system flexible and simple. One of the advantages is allowing the user to not having to think about managing resources (e.g. images, vertex buffers, ..., reloading on context switches, ...) at all and being able to focus fully on what is important (in this case game design).

I got inspired by multiple books for this project with the main idea for abstracting away the rendering interface from the API coming from the following one:

![3D-Spiele-Programmierung](https://images-na.ssl-images-amazon.com/images/I/51wM8CIGjjL._SX363_BO1,204,203,200_.jpg)

<table>
  <tr>
    <td><img src="https://images-na.ssl-images-amazon.com/images/I/51mQl0y9NGL._SX382_BO1,204,203,200_.jpg" width="300"></td>
    <td><img src="https://images-na.ssl-images-amazon.com/images/I/51V1DUCnkQL._SX352_BO1,204,203,200_.jpg" width="300"></td>
    <td><img src="https://images-na.ssl-images-amazon.com/images/I/61T+7acdSSL.jpg" width="300"></td>
  </tr>
  <tr>
    <td><img src="https://images-na.ssl-images-amazon.com/images/I/71Kfg2zTisL.jpg" width="300"></td>
    <td><img src="https://images-na.ssl-images-amazon.com/images/I/41zo5mj1VAL.jpg" width="300"></td>
    <td><img src="https://images-na.ssl-images-amazon.com/images/I/51OWUuHWYFL.jpg" width="300"></td>
  </tr>
</table>
