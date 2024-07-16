# Working with Hit- and Hurtboxes

## Definition

**Hit boxes** are areas where an attack will hit and do damage.   
**Hurt boxes** are areas where a player or bot can be hurt by another's attack.

## How to use them

### Hitbox

<ol>
  <li>Add the node "HitBox" to the scene</li>
  <li>Add a "CollisionShape3D" as a child of the HitBox node</li>
  <li>Add a "Shape" in the inspector of CollisionShape3D and adjust it in the viewport</li>
  <li>If not already present, add a "AnimationPlayer" and create an animation.</li>
  <li> Now you need to create a keyframe for the "disabled" property of the CollisionShape3D. For that press that button: (Image_1)</li>
  <li> Create a keyframe (right-click in the timeline) at the end of the animation and enable it (Image_2).
    
  Select the "RESET" Animation and set "disabled" property to "true" (Image_3).  
  
  This ensures that the Hitbox is only active during the attack-animation.    
  </li>
  <li>Ensure you have a "damage" variable in the Hitbox-script</li>
</ol>

Image_1:

![image](https://github.com/user-attachments/assets/55d9f991-20a9-4212-a17b-5b3ece5cf0ba)

Image_2:

![image](https://github.com/user-attachments/assets/e9fe984e-3537-4694-b9c8-93e4f12ba5bc)

Image_3:

![image](https://github.com/user-attachments/assets/92bc529f-0b2e-45ac-a3d7-23a2d4455389)

### Hurtbox

<ol>
  <li>Add the node "HurtBox" to the scene</li>
  <li>Add a "CollisionShape3D" as a child of the HurtBox node</li>
  <li>Add a "Shape" in the inspector of CollisionShape3D and adjust it in the viewport</li>
  <li>make sure the root node has a script with the method "take_damage(amount)"</li>
</ol>

## Detailed Information:  

```py linenums="1"
class_name HitBox
extends Area3D

@export var damage = 1

func _init():
	collision_layer = 2
	collision_mask = 0
```

```py linenums="1"
class_name HurtBox
extends Area3D

func _init():
	collision_layer = 0
	collision_mask = 2
	

func _ready():
	#signal to detect hitbox
	connect("area_entered", self._on_area_entered)

func _on_area_entered(hitbox: HitBox):
	if hitbox == null:
		return
	
	if owner.has_method("take_damage"):
		owner.take_damage(hitbox.damage)
```

The "class_name" keyword can be used to add the script to the global scope and make it accessible in the node selection
![image](https://github.com/user-attachments/assets/73fe2897-a13f-4d9c-a41c-4180bd1aaace)

Hit- and Hurtbox both extend **"Area3D"**, so if you add them to the scene you need CollisionShape3D as a child node.
![image](https://github.com/user-attachments/assets/318656fa-b68a-4864-bafa-2849753f7825)

The shape of the CollisionShape3D defines the effective hit or hurt area.
