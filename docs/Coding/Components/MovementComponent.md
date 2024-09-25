## Movement Component
This component will move the parentNode3D towards the Player if the Player enters an InteractionArea3D.
This code moves the parent_node towards the player.global_transform.origin.
```py linenums="1"
var target_pos = player.global_transform.origin
    nav_agent.target_position = target_pos
    var current_location = parent_node.global_transform.origin
    var next_location = nav_agent.get_next_path_position()
    var new_velocity = (next_location - current_location).normalized() * speed
    parent_node.velocity = new_velocity
    parent_node.move_and_slide()
```
This code detects every Node3D and checks if its part of the Group "Player" and if true, assigns this body to the variable "player". This can be extended for all other Groups. 
```py linenums="1"
func _on_interaction_area_3d_body_entered(body: Node3D) -> void:
	for group in body.get_groups():
		match group:
			"Player":
				player = body
		# if more needed just add here
```