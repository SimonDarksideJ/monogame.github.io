
# Testing for Collisions

Demonstrates how to use the [BoundingSphere](bb195173.md) class to check whether two models are colliding.


> [!TIP]
> This technique is implemented in the FuelCell game, a game developed by following a series of focused articles that discuss basic 3D game development. For more information, see <A href="dd254739.md">FuelCell: "Ships" Passing in the Night</A>.


# The Complete Sample

The code in the topic shows you the technique. You can download a complete code sample for this topic, including full source code and any additional supporting files required by the sample.

[Download CollisionBetweenSpheres](http://go.microsoft.com/fwlink/?linkid=198839).

# Detecting Whether Two Models Collide

### To check whether two objects are colliding

1.  Track the position of a model as it moves about the game world.
    
    ``` csharp
    struct WorldObject
    {
        public Vector3 position;
        public Vector3 velocity;
        public Model model;
        public Texture2D texture2D;
        public Vector3 lastPosition;
        public void MoveForward()
        {
            lastPosition = position;
            position += velocity;
        }
        public void Backup()
        {
            position -= velocity;
        }
        public void ReverseVelocity()
        {
            velocity.X = -velocity.X;
        }
    }
    ```

2.  Make a nested loop with the first model's meshes as the outer loop and the second model's meshes as the inner loop.

3.  Inside the loop, follow these steps.
    
    1.  Get the bounding sphere for the current mesh of the first model and the current mesh of the second model.
    
    2.  Offset the bounding spheres by the current positions of the models.
    
    3.  Call the [BoundingSphere.Intersects](bb197631.md) method to check the pairs of bounding spheres for collision.
        
        If the method returns **true**, the objects are colliding.
    
    4.  If the models are colliding, break out of the loop.
        
        ``` csharp
        static void CheckForCollisions(ref WorldObject c1, ref WorldObject c2)
        {
            for (int i = 0; i < c1.model.Meshes.Count; i++)
            {
                // Check whether the bounding boxes of the two cubes intersect.
                BoundingSphere c1BoundingSphere = c1.model.Meshes[i].BoundingSphere;
                c1BoundingSphere.Center += c1.position;
        
                for (int j = 0; j < c2.model.Meshes.Count; j++)
                {
                    BoundingSphere c2BoundingSphere = c2.model.Meshes[j].BoundingSphere;
                    c2BoundingSphere.Center += c2.position;
        
                    if (c1BoundingSphere.Intersects(c2BoundingSphere))
                    {
                        c2.ReverseVelocity();
                        c1.Backup();
                        c1.ReverseVelocity();
                        return;
                    }
                }
            }
        }
        ```


> [!NOTE]
> For an example of determining a particle's path after it hits a surface, see <A href="bb198638.md">Vector3.Reflect</A>.


## See Also

#### Tasks

[Rotating and Moving the Camera](bb197901.md)  

#### Concepts

[Bounding Volumes and Collisions](bb313876.md)  
[Collision Content Catalog at App Hub Online](http://go.microsoft.com/fwlink/?linkid=128869)

