# Basics

```kcl
myVariable = value  
```
*Assign values to variables*

```kcl
myVariable = if cond {
  value_if_true
} else {
  value_if_false
}
```
*if expression*

```kcl
x |> f()
```
*Equivalent to f(x) [book](https://zoo.dev/docs/kcl-book/pipelines.html)*

```kcl
x |> f() |> g()
```
*Equivalent to g(f(x))*

# Operators

```kcl
n + m
n - m
-n
n * m
n / m
```
*Basic arithmetic operators*

```kcl
n < m
n <= m
n == m
n != m
n >= m
n > m
```
*Basic relational operators*

```kcl
b & c
b | c
!b
```
*Basic logical operators*

# 2D

```kcl
startSketchOn(XY)
```
*Start sketch on a standard plane [docs](https://zoo.dev/docs/kcl-std/functions/std-sketch-startSketchOn)*

```kcl
startSketchOn(cube, face = myFace)
```
*Start sketch on a tagged face of a solid*

```kcl
startSketchOn(XY)
|> startProfile(at = [0, 0])
```
*Start a profile in a sketch [docs](https://zoo.dev/docs/kcl-std/functions/std-sketch-startProfile)*

```kcl
|> line(end = [3, 3])
|> line(endAbsolute = [3, 3])
```
*Add a line to a profile (relative distances, or end at an absolute point) [docs](https://zoo.dev/docs/kcl-std/functions/std-sketch-line)*

```kcl
|> line(end = [3, 3], tag = $myEdge)
```
*Adds a line, tags it with the given name for referring to later. Almost every sort of line supports `tag =`.*

```kcl
|> close()
```
*Straight line return to start of sketch, closing it [docs](https://zoo.dev/docs/kcl-std/functions/std-sketch-close)*

```kcl
|> xLine(length = 3)
|> xLine(endAbsolute = 3)
```
*Add a horizontal line (relative distance, or end at an absolute point) [docs](https://zoo.dev/docs/kcl-std/functions/std-sketch-xLine)*

```kcl
|> yLine(length = 3)
|> yLine(endAbsolute = 3)
```
*Add a vertical line (relative distance, or end at an absolute point) [docs](https://zoo.dev/docs/kcl-std/functions/std-sketch-yLine)*

```kcl
|> tangentialArc(end = [4, 3])
|> tangentialArc(endAbsolute = [4, 3])
```
*Circular arc that smoothly bends the given X and Y distances away,
or smoothly bends to the given point [docs](https://zoo.dev/docs/kcl-std/functions/std-sketch-tangentialArc)*

```kcl
|> circle(center = [4, 3], diameter = 4)
|> circle(center = [4, 3], radius = 2)
```
*Circle (automatically closes) [docs](https://zoo.dev/docs/kcl-std/functions/std-sketch-circle)*

# Extrudes

```kcl
mySketch |> extrude(length = 4)
```
*Extrudes a 2D sketch into a 3D solid, with the given 3rd dimension length. [book](https://zoo.dev/docs/kcl-book/sketch3d.html#extrude), [docs](https://zoo.dev/docs/kcl-std/functions/std-sketch-extrude)*

```kcl
|> extrude(length = 4, twistAngle = 120deg)
```
*Extrude, twisting the solid around its center too*

```kcl
|> extrude(length = 4, twistAngle = 120deg, twistCenter = [2, 2])
```
*Extrude, twisting the solid around a point 2 units away from its center in each direction*

```kcl
|> extrude(length = 4, symmetric = true)
```
*Extrude 4 units up and 4 units down*

```kcl
|> extrude(length = 4, bidirectionalLength = 1)
```
*Extrude 4 units up and 1 unit*

```kcl
|> extrude(length = 4, bidirectionalLength = 1)
```
*Extrude 4 units up and 1 unit*

```kcl
|> extrude(to = [1, 0, 1])
```
*Extrude until the face reaches the given point*

```kcl
|> extrude(to = Y)
```
*Extrude until the face reaches the given axis*

```kcl
|> extrude(to = YZ)
```
*Extrude until the face reaches the given plane*

```kcl
|> extrude(to = myCube)
```
*Extrude until the face reaches the given solid*

```kcl
|> extrude(to = myEdge)
|> extrude(to = getCommonEdge(faces = [faceTag0, faceTag1]))
```
*Extrude until the face reaches the given tagged edge*

```kcl
|> extrude(length = 4, method = MERGE)
```
*If extruding out of an existing solid, modifies that solid. This is the default.*

```kcl
|> extrude(length = 4, method = NEW)
```
*If extruding out of an existing solid, creates a new solid and leaves the old unchanged*

```kcl
|> extrude(length = 4, tagStart = $myTag)
```
*Tag the face created from the original sketch before extrusion*

```kcl
|> extrude(length = 4, tagEnd = $myTag)
```
*Apply a tag to the face of the sketch created from the extrusion*

# Other 2D-to-3D

```kcl
sweep(mySketch, path = myPath)
```
*Extrude but along the given path instead of a straight line. [book](https://zoo.dev/docs/kcl-book/sketch3d.html#sweep), [docs](https://zoo.dev/docs/kcl-std/functions/std-sketch-sweep)*

```kcl
mySketch |> revolve(axis = Y)
```
*Revolves a sketch 360 degrees around the given axis. [book](https://zoo.dev/docs/kcl-book/sketch3d.html#revolve), [docs](https://zoo.dev/docs/kcl-std/functions/std-sketch-revolve)*

```kcl
mySketch |> revolve(axis = Y, angle = 90deg)
```
*Revolves a sketch partway around the given axis*

```kcl
loft([sketch1, sketch2, sketch3])
```
*Lifts sketches up into each other, interpolating the volume in between. [book](https://zoo.dev/docs/kcl-book/sketch3d.html#lofts), [docs](https://zoo.dev/docs/kcl-std/functions/std-sketch-loft)*

```kcl
loft([sketch1, sketch2, sketch3], vDegree = 1)
```
*Setting vDegree affects how smooth the interpolation is. 1 is jagged straight lines, higher numbers are smoother.*

# Transforming 3Ds

```kcl
|> appearance(color = "#00ff00")
```
*Color a solid*

```kcl
|> appearance(color = "#00ff00", metalness = 90, roughness = 10)
```
*Other visuals are between 0 (low) and 100 (high)*

```kcl
|> translate(x = 10.0, y = 10.0, z = 2.5)
|> translate(xyz = [10, 10, 2.5])
|> translate(x = 10.0)
```
*Translate the object in space, along 1-3 axes. [book](https://zoo.dev/docs/kcl-book/transform_3d.html#translation), [docs](https://zoo.dev/docs/kcl-std/functions/std-transform-translate)*

```kcl
|> scale(x = 0.5, y = 0.5, z = 2)
|> scale(x = 0.5)
```
*Scale the solid's size. 0.5 is half size, 2 is double size. [book](https://zoo.dev/docs/kcl-book/transform_3d.html#scale), [docs](https://zoo.dev/docs/kcl-std/functions/std-transform-scale)*

```kcl
|> rotate(roll = 45deg, pitch = 10deg, yaw = 5deg)
|> rotate(roll = 45deg)
|> rotate(axis = Z, angle = 90deg)
|> rotate(axis = [1, 1, 0], angle = 90deg)
```
*Rotate the solid, giving 1-3 of roll/pitch/yaw, or an axis and angle. [book](https://zoo.dev/docs/kcl-book/transform_3d.html#rotation), [docs](https://zoo.dev/docs/kcl-std/functions/std-transform-rotate)*

```kcl
other = clone(cube) |> translate(x = 10)
```
*Clone and modify other solids (or sketches). [Docs](https://zoo.dev/docs/kcl-std/functions/std-clone)*

# Fillets and chamfers

```kcl
solid |> fillet(radius = 5, tags = [myEdge])
```
*Rounded cut on the edge tagged $myEdge in the original sketch. [book](https://zoo.dev/docs/kcl-book/tags.html#tagging-edges), [docs](https://zoo.dev/docs/kcl-std/functions/std-solid-fillet)*

```kcl
chamfer(length = 5, tags = [myEdge])
```
*Straight cut on the edge tagged $myEdge in the original sketch. [book](https://zoo.dev/docs/kcl-book/tags.html#chamfers), [docs](https://zoo.dev/docs/kcl-std/functions/std-solid-chamfer)*

```kcl
chamfer(length = 5, angle = 30deg, tags = [myEdge])
```
*Specify a custom angle on the chamfer. Angle defaults to 45 degrees if not given.*

```kcl
chamfer(length = 5, secondLength = 1, tags = [myEdge])
```
*Specify the amount to cut away from both faces of this edge. Incompatible with `angle`. Defaults to `length` if not given*

# Traversing edges

```kcl
|> getPreviousAdjacentEdge(myEdge)
```
*Get the side edge just before $myEdge in the solid. Useful for filleting/chamfering sides. [docs](https://zoo.dev/docs/kcl-std/functions/std-sketch-getOppositeEdge)*

```kcl
|> getNextAdjacentEdge(myEdge)
```
*Get the side edge just after $myEdge in the solid [docs](https://zoo.dev/docs/kcl-std/functions/std-sketch-getOppositeEdge)*

```kcl
|> getOppositeEdge(myEdge)
```
*Get the edge on the opposite extruded face of the solid [docs](https://zoo.dev/docs/kcl-std/functions/std-sketch-getOppositeEdge)*

# Planes

```kcl
myPlane = offsetPlane(XY, offset = 20)
```
*Define a new plane, offset from an existing one [book](https://zoo.dev/docs/kcl-book/sketch_on_face.html#offset-planes), [docs](https://zoo.dev/docs/kcl-std/functions/std-offsetPlane)*

```kcl
myPlane = {
  origin = { x = 0, y = 1, z = 0},
  xAxis = { x = 1, y = 0, z = 0 },
  yAxis = { x = 0, y = 0, z = 1 },
}
```
*Manually define a new plane.*

