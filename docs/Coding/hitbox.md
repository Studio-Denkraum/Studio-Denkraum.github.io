### Hitbox
test

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

![image](https://github.com/user-attachments/assets/69c56ba9-82e1-44e9-84a1-8f51f46f34c0)
