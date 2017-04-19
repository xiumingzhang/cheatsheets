### Loop through all objects

```
import bpy
scene = bpy.context.scene
for ob in scene.objects:
    if ob.type == 'MESH' and ob.name.startswith("Cube"):
        ob.select = True
    else: 
        ob.select = False
bpy.ops.object.delete()
```


### Node tree (shader) setup in Cycles

```
for ob in bpy.context.scene.objects:
	if ob.type == 'MESH' and ('Plane' not in ob.name):
		node_tree = ob.data.materials[0].node_tree
		nodes = node_tree.nodes
		nodes.remove(nodes.get('Glossy BSDF')) # remove default
		nodes.new('ShaderNodeBsdfGlass')
		node_tree.links.new(nodes['Mix'].outputs[0], nodes['Glass BSDF'].inputs[0])
		node_tree.links.new(nodes['Glass BSDF'].outputs[0], nodes['Mix Shader'].inputs[2])
```