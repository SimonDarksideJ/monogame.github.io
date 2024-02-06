
# Positioning the Camera

Demonstrates how to position the camera so that all objects in a scene are within the view frustum while maintaining the camera's original orientation. 

# The Complete Sample

The code in the topic shows you the technique. You can download a complete code sample for this topic, including full source code and any additional supporting files required by the sample..

[Download FitCameraToScene\_Sample.zip](http://go.microsoft.com/fwlink/?linkid=198850).

# Positioning the Camera to View All Objects in a Scene

### To position the camera to view all objects in a scene

1.  Create a [BoundingSphere](bb195173.md) class that contains all of the objects in the scene. To create the sphere, loop through all of the objects in the scene, merging the [BoundingSphere](bb195173.md) classes that contain them with [BoundingSphere.CreateMerged](bb195657.md).

2.  If you are not already tracking the [BoundingSphere](bb195173.md) classes for collision detection, use [CreateFromBoundingBox](bb195614.md) or [CreateFromPoints](https://msdn.microsoft.com/en-us/library/m:microsoft.xna.framework.boundingsphere.createfrompoints\(system.collections.generic.ienumerable%7bmicrosoft.xna.framework.vector3%7d\)) to create them from [BoundingBox](bb195161.md) classes or points.
    
    In this example, the [BoundingSphere](bb195173.md) classes are created from [BoundingBox](bb195161.md) classes.
    
    ``` csharp
    BoundingSphere GetSceneSphere()
    {
        BoundingSphere sceneSphere =
            new BoundingSphere(new Vector3(.5f, 1, .5f), 1.5f);
        for (int z = 0; z < 5; z++)
        {
            for (int x = 0; x < 5; x++)
            {
                BoundingSphere boundingSphere =
                    sphere.Meshes[0].BoundingSphere;
                boundingSphere.Center = new Vector3(x * 3, 0, z * 3);
    
                sceneSphere = BoundingSphere.CreateMerged(
                    sceneSphere, boundingSphere);
            }
        }
    
        return sceneSphere;
    }
    ```

3.  Set the position of the camera to the center of the [BoundingSphere](bb195173.md) that contains the scene.
    
    ``` csharp
    cameraPosition = sceneSphere.Center;
    ```

4.  Determine the distance from the center of the [BoundingSphere](bb195173.md) that the camera needs to be to view the entire scene.
    
    This distance is equal to the hypotenuse of the triangle formed by the center of the sphere, the desired camera position, and the point where the sphere touches the view frustum. One angle of the triangle is known to be the field of view of the camera divided by two. One leg of the triangle is known to be the radius of the sphere. Given these two measurements, you can calculate the hypotenuse as the radius of the sphere divided by the sine of half the field of view.
    
    ``` csharp
    float distanceToCenter =
        sceneSphere.Radius / (float)Math.Sin(FOV / 2);
    ```

5.  Get the [Backward](bb195064.md) vector of the view [Matrix](bb197911.md) and flip its X component.
    
    ``` csharp
    Vector3 back = view.Backward;
    back.X = -back.X; //flip x's sign
    ```

6.  To move the camera backward with respect to its orientation, multiply the desired distance by the adjusted back vector from the previous step.
    
    The camera is now facing the center of the sphere containing the scene and is far enough back that the sphere fits in the camera's view frustum.
    
    ``` csharp
    cameraPosition += (back * distanceToCenter);
    ```

## See Also

[Rotating and Moving the Camera](bb197901.md)

© 2012 Microsoft Corporation. All rights reserved.  

© The MonoGame Team.