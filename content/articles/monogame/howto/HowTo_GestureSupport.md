---
title: How to detect Gestures on a Multi-touch Screen.
description: This topic demonstrates how to detect and use multi-touch gestures in a MonoGame game.
---

# Detecting Gestures on a Multi-touch Screen

This topic demonstrates how to detect and use multi-touch gestures in a MonoGame game.

MonoGame supports multi-touch gesture-based input on Mobile. The primary class that provides this support is [TouchPanel](xref:Microsoft.Xna.Framework.Input.Touch.TouchPanel), which provides the ability to:

* Designate which gestures should be detected.
* Query to see if any gestures are available for processing.

> Gesture support is provided as a convenient subset of the features possible on a multi-touch input device. For more information about general multi-touch programming, see [Working with Touch Input](HowTo_UsemultitouchInput.md).

## To enable gesture support and detect gestures in a Windows Phone game

1. Set the gestures to enable with [TouchPanel.EnabledGestures](xref:Microsoft.Xna.Framework.Input.Touch.TouchPanel.EnabledGestures). This can be one value, or a combination of values, in the [GestureType](xref:Microsoft.Xna.Framework.Input.Touch.GestureType) enumeration. Performance can be decreased by enabling all gestures, so it is a good practice to enable only the gestures you'll be using in your game.

2. During your game loop, check to see if any gestures are available with [TouchPanel.IsGestureAvailable](xref:Microsoft.Xna.Framework.Input.Touch.TouchPanel.IsGestureAvailable). When [IsGestureAvailable](xref:Microsoft.Xna.Framework.Input.Touch.TouchPanel.IsGestureAvailable) is **false**, there are no more gestures in the queue.

3. If gestures are available, call [TouchPanel.ReadGesture](xref:Microsoft.Xna.Framework.Input.Touch.TouchPanel.ReadGesture) to get a [GestureSample](xref:Microsoft.Xna.Framework.Input.Touch.GestureSample) that contains the data for the gesture.

> Some gestures will be preceded by another gesture that begins the gesture. For instance, a **DoubleTap** gesture is always preceded by a **Tap** gesture. For more information about the various gesture types supported, see [GestureType](xref:Microsoft.Xna.Framework.Input.Touch.GestureType).

## Example

The following code illustrates the procedure for detecting gestures on a multi-touch screen.

* Enabling gestures in the game's constructor:

    ```csharp
    // set up touch gesture support: make vertical drag and flick the
    // gestures that we're interested in.
    TouchPanel.EnabledGestures = GestureType.VerticalDrag | GestureType.Flick;
    ```

* Detecting gestures in the game's Update method:

    ```csharp
    // get any gestures that are ready.
    while (TouchPanel.IsGestureAvailable)
    {
        GestureSample gs = TouchPanel.ReadGesture();
        switch (gs.GestureType)
        {
            case GestureType.VerticalDrag:
                // move the poem screen vertically by the drag delta
                // amount.
                poem.offset.Y -= gs.Delta.Y;
                break;

            case GestureType.Flick:
                // add velocity to the poem screen (only interested in
                // changes to Y velocity).
                poem.velocity.Y += gs.Delta.Y;
                break;
        }
    }
    ```

## See Also

### Reference

[Microsoft.Xna.Framework.Input.Touch](xref:Microsoft.Xna.Framework.Input.Touch)  
[TouchPanel](xref:Microsoft.Xna.Framework.Input.Touch.TouchPanel)  
[GestureType](xref:Microsoft.Xna.Framework.Input.Touch.GestureType)  
[GestureSample](xref:Microsoft.Xna.Framework.Input.Touch.GestureSample)  

© 2012 Microsoft Corporation. All rights reserved.  

© 2023 The MonoGame Foundation.