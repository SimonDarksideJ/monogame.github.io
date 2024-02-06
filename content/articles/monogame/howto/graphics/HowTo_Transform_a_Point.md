
# Transforming a Point

This example demonstrates how to use the [Vector3](bb199670.md) and [Matrix](bb197911.md) classes to transform a point. A matrix transform can include scaling, rotating, and translating information. 

# The Complete Sample

The code in the topic shows you the technique. You can download a complete code sample for this topic, including full source code and any additional supporting files required by the sample.

[Download TransformPoint\_Sample.zip](http://go.microsoft.com/fwlink/?linkid=198920).

# Transforming a Point with a Matrix

### To transform a point

1.  Create a [Matrix](bb197911.md) by using [CreateRotationY](bb195683.md) or one of the other **Create** methods.
2.  Pass the point and the [Matrix](bb197911.md) to the [Vector3.Transform](bb199541.md) method.

<!-- end list -->

``` csharp
static Vector3 RotatePointOnYAxis(Vector3 point, float angle)
{
    // Create a rotation matrix that represents a rotation of angle radians.
    Matrix rotationMatrix = Matrix.CreateRotationY(angle);

    // Apply the rotation matrix to the point.
    Vector3 rotatedPoint = Vector3.Transform(point, rotationMatrix);

    return rotatedPoint;
}
```

## See Also

#### Matrix Creation Methods

[CreateRotationX](bb195680.md)  
[CreateRotationY](bb195683.md)  
[CreateRotationZ](bb195686.md)  
[CreateScale](bb195693.md)  
[CreateTranslation](bb195698.md)

