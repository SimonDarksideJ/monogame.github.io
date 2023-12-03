---
_title: What Is a Model Bone?
_description: The definition for a Model Bone for MonoGame!
---

# What Is a Model Bone?

A model bone is a matrix that represents the position of a mesh as it relates to other meshes in a 3D model.

![](Model-ModelMesh.png)

A complex computer-generated object, often called a model, is made up of many vertices and materials organized into a set of meshes. In the MonoGame Framework, a model is represented by the [Model](/api/Microsoft.Xna.Framework.Graphics.Model.html) class. A model contains one or more meshes, each of which is represented by a [ModelMesh](/api/Microsoft.Xna.Framework.Graphics.ModelMesh.html) class. Each mesh is associated with one bone represented by the [ModelBone](/api/Microsoft.Xna.Framework.Graphics.ModelBone.html) class.

The bone structure is set up to be hierarchical to make controlling each mesh (and therefore the entire model) easier. At the top of the hierarchy, the model has a [Root](/api/Microsoft.Xna.Framework.Graphics.Model.Root.html) bone to specify the overall position and orientation of the model. Each [ModelMesh](/api/Microsoft.Xna.Framework.Graphics.ModelMesh.html) object contains a [ParentBone](/api/Microsoft.Xna.Framework.Graphics.ModelMesh.ParentBone.html) and one or more [ModelBone](/api/Microsoft.Xna.Framework.Graphics.ModelBone.html). You can transform the entire model using the parent bone as well as transform each individual mesh with its bone. To animate one or more bones, update the bone transforms during the render loop by calling [Model.CopyAbsoluteBoneTransformsTo Method](/api/Microsoft.Xna.Framework.Graphics.Model.CopyAbsoluteBoneTransformsTo.html), which iterates the individual bone transforms to make them relative to the parent bone. To draw an entire model, loop through a mesh drawing each sub mesh.

© 2012 Microsoft Corporation. All rights reserved.  

© 2023 The MonoGame Foundation.