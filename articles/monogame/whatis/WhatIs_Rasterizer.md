---
_title: What Is Rasterizer State?
_description: The definition for a Rasterizer for MonoGame!
---

# What Is Rasterizer State?

Rasterizer state determines how to render 3D data such as position, color, and texture onto a 2D surface.

Rasterization takes a 3D scene containing polygons (which are represented by triangles and vertices) and renders the scene onto a 2D surface. This requires mapping or transforming the 3D vertices into 2D vertices using the world, view, and projection transforms to calculate the final vertex positions in the viewing frustum. To reduce the amount of geometry that needs to be rasterized, the rasterizer clips geometry so that only the parts of a polygon that are visible get processed. The resulting list of transformed vertices is then scan-converted to determine how to fill pixel positions between vertices. Scissor testing takes a list of user-supplied rectangles to further limit the areas you may want rasterized.

Create a rasterizer state object using the [RasterizerState](/api/Microsoft.Xna.Framework.Graphics.RasterizerState.html) class. Set the rasterizer state to the graphics device using the [RasterizerState](/api/Microsoft.Xna.Framework.Graphics.GraphicsDevice.RasterizerState.html) property.

This is the default state for rasterization:

*   Render triangles with clockwise winding order.    
*   Fill primitives so they are solid.    
*   Turn off scissor testing.    
*   Enable multisampling.    
*   Avoid using either depth bias or sloped scaled depth bias.    

These are the corresponding API states:

*   Set [CullMode](/api/Microsoft.Xna.Framework.Graphics.RasterizerState.CullMode.html) to **CullMode.CullCounterClockwiseFace**.    
*   Set [FillMode](/api/Microsoft.Xna.Framework.Graphics.RasterizerState.FillMode.html) to **FillMode.Solid**.    
*   Set [ScissorTestEnable](/api/Microsoft.Xna.Framework.Graphics.RasterizerState.ScissorTestEnable.html) to **false**.    
*   Set [MultiSampleAntiAlias](/api/Microsoft.Xna.Framework.Graphics.RasterizerState.MultiSampleAntiAlias.html) to **true**.    
*   Set [DepthBias](/api/Microsoft.Xna.Framework.Graphics.RasterizerState.DepthBias.html) and [SlopeScaleDepthBias](/api/Microsoft.Xna.Framework.Graphics.RasterizerState.SlopeScaleDepthBias.html) to 0.    

Built-in state objects make it easy to create objects with the most common rasterizer state settings. **CullNone**, **CullClockwise**, and **CullCounterClockwise** are the most common settings. For an example of creating a state object, see [Creating a State Object](StateObject1.md).

© 2012 Microsoft Corporation. All rights reserved.  

© 2023 The MonoGame Foundation.