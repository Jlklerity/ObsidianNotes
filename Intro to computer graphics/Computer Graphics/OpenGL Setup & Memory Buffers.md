![[Pasted image 20260722112559.png|543]]![[Pasted image 20260722112643.png|543]]

## VBO

Storage allocated for OpenGL vertex, color, texture data etc....

## VAO

Vertex Array Objects are basically settings to configure the data (VBO)

## EBO

Stores vertex indices to tell the GPU which indices to use when making primitives. Useful for referencing vertex data rather than having to repeat the vertexes again.

`unsigned int EBO;
`glGenBuffers(1, &EBO);`
`glBindBuffer(GL_ELEMENT_ARRAY_BUFFER, EBO);`
`glBufferData(GL_ELEMENT_ARRAY_BUFFER, sizeof(indices), indices, GL_STATIC_DRAW);`

## SSBO (Since OpenGL 4.3)

A general-purpose, large, **read-write** buffer accessible directly _inside shader code_ (vertex, fragment, compute, etc.)

`layout(std430, binding = 0) buffer ParticleBuffer {`
    `vec4 positions[];`
`};`

## PBO (Pixel Buffer Objects)

Unlike VBOs that store vertex data to input in the vertex shader, PBOs store raw pixel data to input in textures


| Feature        | VBO                                         | PBO                                                 |
| -------------- | ------------------------------------------- | --------------------------------------------------- |
| Primary Target | `GL_ARRAY_BUFFER`                           | `GL_PIXEL_UNPACK_BUFFER`/<br>`GL_PIXEL_PACK_BUFFER` |
| Data Type      | Vertex data (positions, normals, UVs).      | Raw pixel data (images, textures, framebuffers).    |
| Pipeline Stage | Input to the Vertex Shader.                 | Input to Textures or output from Framebuffers.      |
| Direction      | One-way: CPU → GPU.                         | Two-way: CPU → GPU OR GPU → CPU.                    |
| Main Benefit   | Avoids sending vertex data every draw call. | Enables asynchronous DMA pixel transfers.           |

> [!important] Which To Use? For Efficiency
> • Use a VBO when you need to draw 3D geometry. Using a PBO for vertex data is invalid.
> • Use a PBO when you need to stream video frames, upload textures dynamically, or save screenshots. Using a VBO for raw image data transfers is invalid.


## Framebuffer

#### Depth Buffer (Z buffer)

stores the Z-axis (depth) values of each pixel

#### Stencil Buffer

mask pixels in an image, to produce special effects

#### Color Buffer

Holds colored pixels to display

#### Double Buffering

technique used in computer graphics and data processing to prevent screen flickering and improve performance by using two memory buffers

#### Stride Padding

![[Pasted image 20260722115032.png]]

> [!attention] Note
> OpenGL runs with only one thread at a time. 
> 
> OpenGL cannot choose what GPU hardware to use. (Only takes what is selected in the Control Panel of the selected GPU in use)
