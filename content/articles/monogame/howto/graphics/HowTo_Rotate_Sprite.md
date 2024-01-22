# Rotating a Sprite

Demonstrates how to rotate a sprite around its center.

## Drawing a Rotated Sprite

### To draw a rotated sprite on screen

1. Follow the procedures of [Drawing a Sprite](HowTo_Draw_A_Sprite.md).

2. Determine the screen location of the sprite, and the point within the texture that will serve as the origin.
   By default, the origin of a texture is (0,0), the upper-left corner. When you draw a sprite, the origin point in the texture is placed on the screen coordinate specified by the _at_ parameter. In this example, the origin is the center of the texture, and the screen position is the center of the screen.

    ```csharp
    private Texture2D SpriteTexture;
    private Vector2 origin;
    private Vector2 screenpos;
    protected override void LoadContent()
    {
        // Create a new SpriteBatch, which can be used to draw textures.
        spriteBatch = new SpriteBatch(GraphicsDevice);
        SpriteTexture = Content.Load<Texture2D>("ship");
        Viewport viewport = graphics.GraphicsDevice.Viewport;
        origin.X = SpriteTexture.Width / 2;
        origin.Y = SpriteTexture.Height / 2;
        screenpos.X = viewport.Width / 2;
        screenpos.Y = viewport.Height / 2;
    }
    ```

3. In your [Update](xref:Microsoft.Xna.Framework.Game.Update) method, determine the rotation angle to use for the sprite.

   The angle is specified in radians, and it can be greater than two times π, but does not need to be.

    ```csharp
    private float RotationAngle;
    protected override void Update(GameTime gameTime)
    {
        // Allows the game to exit
        if (GamePad.GetState(PlayerIndex.One).Buttons.Back == ButtonState.Pressed)
            this.Exit();
    
        if (Keyboard.GetState().IsKeyDown(Keys.Escape))
            this.Exit();
    
        // The time since Update was called last.
        float elapsed = (float)gameTime.ElapsedGameTime.TotalSeconds;
    
        // TODO: Add your game logic here.
        RotationAngle += elapsed;
        float circle = MathHelper.Pi * 2;
        RotationAngle = RotationAngle % circle;
    
        base.Update(gameTime);
    }
    ```

4. In your [Draw](xref:Microsoft.Xna.Framework.Game.Draw) method, call [SpriteBatch.Draw](xref:Microsoft.Xna.Framework.Graphics.SpriteBatch.Draw) with the texture, angle, screen position, and origin of the texture.

    ```csharp
    protected override void Draw(GameTime gameTime)
    {
        graphics.GraphicsDevice.Clear(Color.CornflowerBlue);
    
        // TODO: Add your drawing code here
        spriteBatch.Begin();
        spriteBatch.Draw(SpriteTexture, screenpos, null, Color.White, RotationAngle,
            origin, 1.0f, SpriteEffects.None, 0f);
        spriteBatch.End();
    
        base.Draw(gameTime);
    }
    ```

5. When all the sprites have been drawn, call [End](xref:Microsoft.Xna.Framework.Graphics.SpriteBatch.End) on your [SpriteBatch](xref:Microsoft.Xna.Framework.Graphics.SpriteBatch) object.

## See Also

### Tasks

[Drawing a Sprite](HowTo_Draw_A_Sprite.md)  

#### Concepts

[What Is a Sprite?](Sprite_Overview.md)  

#### Reference

[SpriteBatch](xref:Microsoft.Xna.Framework.Graphics.SpriteBatch)  
[Draw](xref:Microsoft.Xna.Framework.Graphics.SpriteBatch.Draw)  
[Texture2D](xref:Microsoft.Xna.Framework.Graphics.Texture2D)  

© 2012 Microsoft Corporation. All rights reserved.  

© 2023 The MonoGame Foundation.