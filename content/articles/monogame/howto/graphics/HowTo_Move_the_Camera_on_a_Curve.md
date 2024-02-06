
# Moving the Camera on a Curve

Demonstrates how to use the [Curve](bb196070.md) and [CurveKey](bb196065.md) classes to move a camera along the shape of a curve.

Using [Curve](bb196070.md)s allows a path to be defined by a small number of control points with the [Curve](bb196070.md)s calculating the points on the path between the control points.

# The Complete Sample

The code in the topic shows you the technique. You can download a complete code sample for this topic, including full source code and any additional supporting files required by the sample.

[Download ScriptedCamera\_Sample.zip](http://go.microsoft.com/fwlink/?linkid=198895).

# Scripting the Camera to Follow a Curve

### To script camera movement

1.  Create an instance of the [Curve](bb196070.md) class for each component being scripted.
    
    In this case, you need two sets of three curves. One is for each of the x, y, and z components of the camera's position, and the other is for the position at which the camera is looking (the "look-at" position).
    
    ``` csharp
    class Curve3D
    {
    
        public Curve curveX = new Curve();
        public Curve curveY = new Curve();
        public Curve curveZ = new Curve();
        ...
    }
    ```
    
        Curve3D cameraCurvePosition = new Curve3D();
        Curve3D cameraCurveLookat = new Curve3D();

2.  Set the [PreLoop](bb198493.md) and [PostLoop](bb198486.md) type of each [Curve](bb196070.md).
    
    The [PreLoop](bb198493.md) and [PostLoop](bb198486.md) types determine how the curve will interpret positions before the first key or after the last key. In this case, the values will be set to [CurveLoopType.Oscillate](bb196069.md). Values past the ends of the curve will change direction and head toward the opposite side of the curve.
    
    ``` csharp
    curveX.PostLoop = CurveLoopType.Oscillate;
    curveY.PostLoop = CurveLoopType.Oscillate;
    curveZ.PostLoop = CurveLoopType.Oscillate;
    
    curveX.PreLoop = CurveLoopType.Oscillate;
    curveY.PreLoop = CurveLoopType.Oscillate;
    curveZ.PreLoop = CurveLoopType.Oscillate;
    ```

3.  Add [CurveKey](bb196065.md)s to the [Curve](bb196070.md)s.

4.  Specify the time each [CurveKey](bb196065.md) should be reached and the camera position when the [CurveKey](bb196065.md) is reached.
    
    In this case, each point in time will have three [CurveKey](bb196065.md)s associated with it – one for each of the x, y, and z coordinates of the point on the [Curve](bb196070.md).
    
    ``` csharp
    public void AddPoint(Vector3 point, float time)
    {
        curveX.Keys.Add(new CurveKey(time, point.X));
        curveY.Keys.Add(new CurveKey(time, point.Y));
        curveZ.Keys.Add(new CurveKey(time, point.Z));
    }
    ```
    
        void InitCurve()
        {
            float time = 0;
            cameraCurvePosition.AddPoint(new Vector3(7.5f, 0, -45), time);
            cameraCurveLookat.AddPoint(new Vector3(9, 0, 9), time);
            time += 2000;
            cameraCurvePosition.AddPoint(new Vector3(3f, 0, -36), time);
            time += 2000;
            cameraCurvePosition.AddPoint(new Vector3(12f, 0, -30), time);
            time += 2000;
            cameraCurvePosition.AddPoint(new Vector3(3f, 0, -24), time);
            time += 2000;
            cameraCurvePosition.AddPoint(new Vector3(12f, 0, -18), time);
            time += 2000;
            ...
            cameraCurvePosition.SetTangents();
            cameraCurveLookat.SetTangents();
        }

5.  Loop through each [Curve](bb196070.md) setting the [TangentIn](bb199296.md) and [TangentOut](bb199297.md) of each [CurveKey](bb196065.md).
    
    The tangents of the [CurveKey](bb196065.md)s control the shape of the [Curve](bb196070.md). Setting the tangents of the [CurveKey](bb196065.md)s to the slope between the previous and next [CurveKey](bb196065.md) will give a curve that moves smoothly through each point on the curve.
    
    ``` csharp
    public void SetTangents()
    {
        CurveKey prev;
        CurveKey current;
        CurveKey next;
        int prevIndex;
        int nextIndex;
        for (int i = 0; i < curveX.Keys.Count; i++)
        {
            prevIndex = i - 1;
            if (prevIndex < 0) prevIndex = i;
    
            nextIndex = i + 1;
            if (nextIndex == curveX.Keys.Count) nextIndex = i;
    
            prev = curveX.Keys[prevIndex];
            next = curveX.Keys[nextIndex];
            current = curveX.Keys[i];
            SetCurveKeyTangent(ref prev, ref current, ref next);
            curveX.Keys[i] = current;
            prev = curveY.Keys[prevIndex];
            next = curveY.Keys[nextIndex];
            current = curveY.Keys[i];
            SetCurveKeyTangent(ref prev, ref current, ref next);
            curveY.Keys[i] = current;
    
            prev = curveZ.Keys[prevIndex];
            next = curveZ.Keys[nextIndex];
            current = curveZ.Keys[i];
            SetCurveKeyTangent(ref prev, ref current, ref next);
            curveZ.Keys[i] = current;
        }
    }
    ```
    
        static void SetCurveKeyTangent(ref CurveKey prev, ref CurveKey cur, 
            ref CurveKey next)
        {
            float dt = next.Position - prev.Position;
            float dv = next.Value - prev.Value;
            if (Math.Abs(dv) < float.Epsilon)
            {
                cur.TangentIn = 0;
                cur.TangentOut = 0;
            }
            else
            {
                // The in and out tangents should be equal to the 
                // slope between the adjacent keys.
                cur.TangentIn = dv * (cur.Position - prev.Position) / dt;
                cur.TangentOut = dv * (next.Position - cur.Position) / dt;
            }
        }

6.  Add code to evaluate the x, y, and z coordinates of the [Curve](bb196070.md)s at any given time by passing the elapsed time to the [Evaluate](https://msdn.microsoft.com/en-us/library/m:microsoft.xna.framework.curve.evaluate\(system.single\)) method of each of the [Curve](bb196070.md)s.
    
    ``` csharp
    public Vector3 GetPointOnCurve(float time)
    {
        Vector3 point = new Vector3();
        point.X = curveX.Evaluate(time);
        point.Y = curveY.Evaluate(time);
        point.Z = curveZ.Evaluate(time);
        return point;
    }
    ```

7.  Create a variable to track the amount of time that has passed since the camera started moving.
    
    ``` csharp
    double time;
    ```

8.  In [Game.Update](https://msdn.microsoft.com/en-us/library/m:microsoft.xna.framework.game.update\(microsoft.xna.framework.gametime\)), set the camera's position and look-at position based on the elapsed time since the camera started moving, and then set the camera's view and projection matrices as in [Rotating and Moving the Camera](bb197901.md).
    
    ``` csharp
    // Calculate the camera's current position.
    Vector3 cameraPosition =
        cameraCurvePosition.GetPointOnCurve((float)time);
    Vector3 cameraLookat =
        cameraCurveLookat.GetPointOnCurve((float)time);
    ```

9.  In [Game.Update](https://msdn.microsoft.com/en-us/library/m:microsoft.xna.framework.game.update\(microsoft.xna.framework.gametime\)), use [gameTime.ElapsedGameTime.TotalMilliseconds](bb196533.md) to increment the time since the camera started moving.
    
    ``` csharp
    time += gameTime.ElapsedGameTime.TotalMilliseconds;
    ```

## See Also

[Rotating and Moving the Camera](bb197901.md)

© 2012 Microsoft Corporation. All rights reserved.  

© The MonoGame Team.