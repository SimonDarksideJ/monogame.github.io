---
title: How to load content within a Game?
description: Loading content is simple using the Content Pipeline within MonoGame projects.
---

# Loading Content in a Game

You need a content project in your game compile and build your project.

1. [Add a game content project](HowTo_GameContent_Add.md) to the solution.
2. Derive a class from [Game](xref:Microsoft.Xna.Framework.Game).
3. Override the [LoadContent](xref:Microsoft.Xna.Framework.Game) method of [Game](xref:Microsoft.Xna.Framework.Game).
4. In the [LoadContent](xref:Microsoft.Xna.Framework.Game) method, load your content using the [ContentManager](xref:Microsoft.Xna.Framework.Content.ContentManager).

    ```csharp
    SpriteBatch spriteBatch;
    // This is a texture we can render.
    Texture2D myTexture;
    
    protected override void LoadContent()
    {
        // Create a new SpriteBatch, which can be used to draw textures.
        spriteBatch = new SpriteBatch(GraphicsDevice);
        myTexture = Content.Load<Texture2D>("mytexture");
    }
    ```

5. Override the [UnloadContent](xref:Microsoft.Xna.Framework.Game) method of [Game](xref:Microsoft.Xna.Framework.Game).
6. In the [UnloadContent](xref:Microsoft.Xna.Framework.Game) method, unload resources that are not managed by the [ContentManager](xref:Microsoft.Xna.Framework.Content.ContentManager).

    ```csharp
    protected override void UnloadContent()
    {
        // TODO: Unload any non ContentManager content here
    }
    ```

## See Also

### Reference

- [Game Class](xref:Microsoft.Xna.Framework.Game)  
- [LoadContent](xref:Microsoft.Xna.Framework.Game.LoadContent)  
- [UnloadContent](xref:Microsoft.Xna.Framework.Game.UnloadContent)  
- [Game Members](xref:Microsoft.Xna.Framework.Game)  
- [Microsoft.Xna.Framework Namespace](xref:Microsoft.Xna.Framework)  

---

© 2012 Microsoft Corporation. All rights reserved.  

© 2023 The MonoGame Foundation.
