---
_title: What Is a Back Buffer?
_description: The definition of a Back Buffer for MonoGame!
---

# What Is a Back Buffer?

A back buffer is a render target whose contents will be sent to the device when [GraphicsDevice.Present](/api/Microsoft.Xna.Framework.Graphics.GraphicsDevice.html#Microsoft_Xna_Framework_Graphics_GraphicsDevice_Present) is called.

The graphics pipeline renders to a render target. The particular render target that the device presents to the display is called the back buffer. Use the [BackBufferWidth](/api/Microsoft.Xna.Framework.Graphics.PresentationParameters.html#Microsoft_Xna_Framework_Graphics_PresentationParameters_BackBufferWidth) and [BackBufferHeight](/api/Microsoft.Xna.Framework.Graphics.PresentationParameters.html#Microsoft_Xna_Framework_Graphics_PresentationParameters_BackBufferHeight) properties to get the back buffer dimensions. Render directly to the back buffer or to a render target by configuring the device using [GraphicsDevice.SetRenderTarget](/api/Microsoft.Xna.Framework.Graphics.GraphicsDevice.html#Microsoft_Xna_Framework_Graphics_GraphicsDevice_SetRenderTarget_Microsoft_Xna_Framework_Graphics_RenderTarget2D_) and [GraphicsDevice.SetRenderTargets](/api/Microsoft.Xna.Framework.Graphics.GraphicsDevice.html#Microsoft_Xna_Framework_Graphics_GraphicsDevice_SetRenderTargets_Microsoft_Xna_Framework_Graphics_RenderTargetBinding___).

For Windows, the back buffer is created to match the dimensions of the [ClientBounds](/api/Microsoft.Xna.Framework.GameWindow.html#Microsoft_Xna_Framework_GameWindow_ClientBounds) by default. For consoles and mobile, the back buffer is created with the dimensions that have been specified by the user. When going into full-screen mode on Windows, it is often desirable to set the back buffer dimensions to match the [DisplayMode](/api/Microsoft.Xna.Framework.Graphics.GraphicsDevice.html#Microsoft_Xna_Framework_Graphics_GraphicsDevice_DisplayMode) dimensions so that the game ("display") resolution does not change when it goes into the full-screen mode.

When the back buffer is created it is not necessarily the same size as the final resolution on a television connected for display. The display automatically scales output to the television resolution selected by the user for the System. If the aspect ratio of the back buffer is different from the aspect ratio of the television display mode, the display will automatically add black bars (also called letterboxing) if the user's display is not widescreen.

In addition, if you request a back-buffer resolution that is not supported by the output device, the MonoGame framework automatically selects the highest resolution supported by the output device. For example, if you create a back-buffer with a resolution of 1920x1080 (for example, 1080p or 1080i) and display it on a device with 480i resolution, the back-buffer is resized to 480i automatically.

# See Also

[Viewport](WhatIs_Viewport.md)  

© 2012 Microsoft Corporation. All rights reserved.  

© 2023 The MonoGame Foundation.