---
title: Tinting a Sprite
description: Demonstrates how to tint a sprite using a Color value.
---

# Tinting a Sprite

Demonstrates how to tint a sprite using a [Color](xref:Microsoft.Xna.Framework.Color) value.

## Drawing a Tinted Sprite

1. Follow the procedures of [Drawing a Sprite](HowTo_Draw_A_Sprite.md).
2. In the [Update](xref:Microsoft.Xna.Framework.Game.Update) method, determine how to tint the sprite.

   In this example, the value of the game pad thumbsticks determine the Red, Green, Blue, and Alpha values to apply to the sprite.

    ```csharp
    protected Color tint;
    protected override void Update(GameTime gameTime)
    {
        ...
        GamePadState input = GamePad.GetState(PlayerIndex.One);
        tint = new Color(GetColor(input.ThumbSticks.Left.X),
            GetColor(input.ThumbSticks.Left.Y),
            GetColor(input.ThumbSticks.Right.X),
            GetColor(input.ThumbSticks.Right.Y));
    
        base.Update(gameTime);
    }
    ```

3. In the [Draw](xref:Microsoft.Xna.Framework.Game.Draw) method, pass the color value created in [Update](xref:Microsoft.Xna.Framework.Game.Update) to [SpriteBatch.Draw](xref:Microsoft.Xna.Framework.Graphics.SpriteBatch.Draw).

    ```csharp
    protected override void Draw(GameTime gameTime)
    {
        GraphicsDevice.Clear(Color.CornflowerBlue);
    
        spriteBatch.Begin();
        spriteBatch.Draw(SpriteTexture, position, tint);
        spriteBatch.End();
    
        base.Draw(gameTime);
    }
    ```

4. When all of the sprites have been drawn, call [End](xref:Microsoft.Xna.Framework.Graphics.SpriteBatch.End) on your [SpriteBatch](xref:Microsoft.Xna.Framework.Graphics.SpriteBatch) object.

## See Also

### Tasks

[Drawing a Sprite](HowTo_Draw_A_Sprite.md)

#### Concepts

[What Is a Sprite?](./../../whatis/WhatIs_Sprite.md)

#### Reference

[SpriteBatch](xref:Microsoft.Xna.Framework.Graphics.SpriteBatch)  
[Draw](xref:Microsoft.Xna.Framework.Graphics.SpriteBatch.Draw)  
[Texture2D](xref:Microsoft.Xna.Framework.Graphics.Texture2D)  
[Color](xref:Microsoft.Xna.Framework.Color)  

© 2012 Microsoft Corporation. All rights reserved.  

© 2023 The MonoGame Foundation.
