## Functionality

Recognizing the start and end of an interaction, when the player steps into or out of the specified area and make the implementing node turn to player and turn back, after ending the interaction.

## Implementation

### Properties

**interaction_area**: Area3D
--> Area where the interaction is trigger

**parent_node**: Node3D
--> Root node of implementing node, that will be rotated

**label**: Label3D
--> Label, visible when player is within interaction_area

**follow_player**: bool
--> If true, the implementing node continues to rotate to look at player, while they are in the area. Otherwise, it only rotates once when the player enters the area.

### Set up

After checking if all properties were set, we connect to the signals of the interaction_area:

```py linenums="1"
interaction_area.body_entered.connect(_on_interaction_area_body_entered)
interaction_area.body_exited.connect(_on_interaction_area_body_exited)
```

Additionally, we set up a timer with a wait time of 1 second. The implementing node will wait that time, before turning back to its original position after the player exited the area. 

```py linenums="1"
# create timer
turn_back_timer = Timer.new()
turn_back_timer.wait_time = 1
# connect timer signal
turn_back_timer.timeout.connect(_on_turn_back_timer_timeout)
add_child(turn_back_timer)
```

### Rotation

When the implementing node is set up, the current rotation (& scale) is saved into "original_basis". When the player is detected in the area, the "target_basis" is set to looking at the player (see below). 

```py linenums="1"
func rotateToPlayer() -> void:
	# normalized vector pointing from this to player
	player_vector = parent_node.global_position.direction_to(player.position)
	# get rotation and scale of player
	player_basis = Basis.looking_at(player_vector)
	target_basis = player_basis
```
After exiting the area, a timer is started and after its timeout, the "target_basis" is set to the "original_basis" prompting the node to turn back to its original rotation. 

The rotation itself is implemented using **Basis.slerp**, to change the rotation every delta by a defined "weight" to the target (see below, line 7). As we only want the node to turn around the y axis to not have a leaning node, we have to reset the Z and X rotation to 0 (line 9 and 10)

```py linenums="1"
func _process(_delta: float) -> void:
	if (target_basis):
		if is_in_interaction_area && follow_player:
			rotateToPlayer()
		# slowly turn either to face player entity or 
		# (if they exited the interaction area) back to its original position
		parent_node.basis = parent_node.basis.slerp(target_basis, 0.05)
		# reset z and x rotation, to only turn around y axis 
		parent_node.rotation.z = 0
		parent_node.rotation.x = 0
```

When "follow_player" is set as true, the "target_base" is updated every delta to represent the players position (see above, line 3 and 4). 
