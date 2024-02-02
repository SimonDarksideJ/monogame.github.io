---
title: How to create a Render Target
description: Demonstrates how to create a render target using a RenderTarget2D.
---

# Creating a Render Target

Demonstrates how to create a render target using the [RenderTarget2D](xref:Microsoft.Xna.Framework.Graphics.RenderTarget2D) class.

## Creating a RenderTarget

### To create a render target

1. Declare variables for a render target using the [RenderTarget2D](xref:Microsoft.Xna.Framework.Graphics.RenderTarget2D) class and the render target texture using a [Texture2D](xref:Microsoft.Xna.Framework.Graphics.Texture2D) class.

    ```csharp
    SpriteBatch spriteBatch;
    Texture2D grid;
    RenderTarget2D renderTarget;
    ```

2. Create a render target, giving it the same size as the back buffer.

    ```csharp
    renderTarget = new RenderTarget2D(
        GraphicsDevice,
        GraphicsDevice.PresentationParameters.BackBufferWidth,
        GraphicsDevice.PresentationParameters.BackBufferHeight);
    ```

3. Load a grid for a texture, which contains two vertical and two horizontal lines.

    ```csharp
    protected override void LoadContent()
    {
        // Create a new SpriteBatch, which can be used to draw textures.
        spriteBatch = new SpriteBatch(GraphicsDevice);
    
        grid = Content.Load<Texture2D>("grid");
    }
    ```

4. Render the texture to the render target.

    This function sets the render target on the device, draws the texture (to the render target) using a [SpriteBatch](xref:Microsoft.Xna.Framework.Graphics.SpriteBatch), and sets the device render target to null (which resets the device to the back buffer).

    ```csharp
    private void DrawRenderTarget()
    {
        // Set the device to the render target
        graphicsDeviceManager.GraphicsDevice.SetRenderTarget(renderTarget);
    
        graphicsDeviceManager.GraphicsDevice.Clear(Color.Black);
    
        spriteBatch.Begin();
        Vector2 pos = Vector2.Zero;
        spriteBatch.Draw(grid, pos, Color.White);
        spriteBatch.End();
    
        // Reset the device to the back buffer
        graphicsDeviceManager.GraphicsDevice.SetRenderTarget(null);
    }
    ```

5. Draw the render target texture to the back buffer.

    ```csharp
    graphicsDeviceManager.GraphicsDevice.Clear(Color.CornflowerBlue);
    
    spriteBatch.Begin();
    spriteBatch.Draw((Texture2D)renderTarget,
        new Vector2(200, 50),          // x,y position
        new Rectangle(0, 0, 32, 32),   // just one grid
        Color.White                    // no color scaling
        );
    spriteBatch.End();
    ```

---

© 2012 Microsoft Corporation. All rights reserved.  

© 2023 The MonoGame Foundation.
