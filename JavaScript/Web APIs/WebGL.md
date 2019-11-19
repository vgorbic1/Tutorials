## WebGL
WebGL (Web Graphics Library) is a JavaScript API for rendering high-performance interactive 3D and 
2D graphics within any compatible web browser without the use of plug-ins. WebGL can be used in HTML5 <canvas> elements. 
It takes advantage of hardware graphics acceleration provided by the user's device.

WebGL programs consist of control code written in JavaScript and special effects code (shader code) that is executed 
on a computer's Graphics Processing Unit (GPU). WebGL elements can be mixed with other HTML elements and composited
with other parts of the page or page background.

WebGL 2 is a major update to WebGL which is provided through the WebGL2RenderingContext interface with new rich features.

In order to draw graphics on the canvas we use a JavaScript context object, which creates graphics on the fly.

### Shader 
A shader (a set of vertex and fragment shaders) is a program, written using the OpenGL ES Shading Language (GLSL), that takes information about the vertices that make up a shape and generates the data needed to render the pixels onto the screen: namely, the positions of the pixels and their colors.

### Lighting
WebGL doesn't have much built-in knowledge. It just runs two functions you supply — a vertex shader and a fragment shader — and expects you to write creative functions to get the results you want. In other words, if you want lighting you have to calculate it yourself.
