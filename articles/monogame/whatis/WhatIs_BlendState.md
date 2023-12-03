---
_title: What Is Blend State?
_description: The definition for the Blend State for MonoGame!
---

# What Is Blend State?

Blend state controls how color and alpha values are blended when combining rendered data with existing render target data.

The blend state class, [BlendState](/api/Microsoft.Xna.Framework.Graphics.BlendState.html), contains state that controls how colors are blended. Each time you render, the pixel data you generate (call it source data) is stored in a render target. The render target might be empty or it might already contain data (call it destination data). Blending occurs each time you combine source and destination data.

You have a lot of control over how you blend the source and the destination data. For example, you can choose to overwrite the destination with the source data by setting [BlendState.Opaque](/api/Microsoft.Xna.Framework.Graphics.BlendState.html#Microsoft_Xna_Framework_Graphics_BlendState_Opaque) or combine the data by adding them together using [BlendState.Additive](/api/Microsoft.Xna.Framework.Graphics.BlendState.html#Microsoft_Xna_Framework_Graphics_BlendState_Additive). You can blend only the color data or the alpha data, or both, by setting up the blending functions [ColorBlendFunction](/api/Microsoft.Xna.Framework.Graphics.BlendState.html#Microsoft_Xna_Framework_Graphics_BlendState_ColorBlendFunction) and [AlphaBlendFunction](/api/Microsoft.Xna.Framework.Graphics.BlendState.html#Microsoft_Xna_Framework_Graphics_BlendState_AlphaBlendFunction). You can even limit your blending operation to one or more colors (or channels) using [ColorWriteChannels](/api/Microsoft.Xna.Framework.Graphics.BlendState.html#Microsoft_Xna_Framework_Graphics_BlendState_ColorWriteChannels).

For an example that creates and uses a state object, see [Creating a State Object](StateObject1.md).

© 2012 Microsoft Corporation. All rights reserved.  

© 2023 The MonoGame Foundation.