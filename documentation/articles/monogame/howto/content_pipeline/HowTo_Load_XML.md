---
title: How to load XML Content at Runtime?
description: Describes how to load custom game data at game runtime through the Content Pipeline.
---

# Loading XML Content at Runtime

This example concludes the procedure begun in the tutorial [Adding an XML Content File to a Visual Studio Project](HowTo_Add_XML.md).

Once custom game data is integrated as game content from an XML file through the Content Pipeline, it exists within your game runtime package in binary format. The data can be [loaded at runtime](HowTo_LoadContent.md) through the [ContentManager](xref:Microsoft.Xna.Framework.Content.ContentManager).

## To load the custom data in the game

Add the "MyDataTypes" library as a reference in the game project.

1. In **Solution Explorer**, right-click the game project, click **Add Reference**, click the **Projects** tab, select **MyDataTypes**, and then click **OK**.

2. In **Solution Explorer**, double-click Game1.cs to edit it.

3. Add the `using` declaration for the MyDataTypes namespace.

    ```csharp
    using MyDataTypes;
    ```

4. Add a data declaration for an array of type PetData, the class defined in the "MyDataTypes" library.

    ```csharp
    PetData[] pets;
    ```

5. In the [Game.LoadContent](xref:Microsoft.Xna.Framework.Game#Microsoft_Xna_Framework_Game_LoadContent) override function, load the custom content.

    ```csharp
    protected override void LoadContent()
    {
        // Load the pet data table
        pets = Content.Load<PetData[]>("pets");
    }
    ```

    The custom game data now resides in the array of `PetData` objects.

## See Also

- [Using an XML File to Specify Content](HowTo_UseCustomXML.md)  
- [Adding Content to a Game](HowTo_GameContent_Add.md)  

---

© 2012 Microsoft Corporation. All rights reserved.  

© 2023 The MonoGame Foundation.