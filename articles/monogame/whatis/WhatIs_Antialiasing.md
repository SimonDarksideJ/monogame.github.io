---
_title: What is Antialiasing?
_description: The definition of Antialsing for MonoGame!
---

# What Is Antialiasing?

Antialiasing is a technique for softening or blurring sharp edges so they appear less jagged when rendered.

Antialiasing is accomplished by multisampling each pixel at multiple pixel locations and combining the samples to generate a final pixel color. Increasing the number of samples per pixel increases the amount of antialiasing which generates a smoother edge. 4x multisampling requires four samples per pixel and 2x multisampling requires two sampler per pixel. Use the [MultiSampleCount](/api/Microsoft.Xna.Framework.Graphics.PresentationParameters.html#Microsoft_Xna_Framework_Graphics_PresentationParameters_MultiSampleCount) property of the [PresentationParameters](/api/Microsoft.Xna.Framework.Graphics.PresentationParameters.html) class to set the number of samples for the back buffer.

Set the [PreferMultiSampling](/api/Microsoft.Xna.Framework.GraphicsDeviceManager.html#Microsoft_Xna_Framework_GraphicsDeviceManager_PreferMultiSampling) property on the [GraphicsDeviceManager](/api/Microsoft.Xna.Framework.GraphicsDeviceManager.html) class to **true** to enable multisampling for the back buffer. This will be ignored if the hardware does not support multisampling.

# See Also

[Enabling Antialiasing (Multisampling)](Enable_Anti_Aliasing.md)  

© 2012 Microsoft Corporation. All rights reserved.  

© 2023 The MonoGame Foundation.