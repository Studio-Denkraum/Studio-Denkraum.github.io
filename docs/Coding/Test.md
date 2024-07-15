```gd linenums="1"
    extends CharacterBody3D

    @export var speed = 5.0
    @export var acceleration = 5.0

    # Get the gravity from the project settings to be synced with RigidBody nodes.
    var gravity = ProjectSettings.get_setting("physics/3d/default_gravity")

    # attack animation names
    var attacks = [
        "melee_attack"
    ]
    var is_attacking = false

    @onready var mesh_node: Node3D = $playerModelWAnim
    @onready var anim_tree = $playerModelWAnim.get_children()[2]
    @onready var anim_state = $playerModelWAnim.get_children()[2].get("parameters/playback")


    func _physics_process(delta):
        # Add the gravity.
        if not is_on_floor():
            velocity.y -= gravity * delta
        
        get_move_input(delta)
        move_and_slide()
        
        # handle rotation
        if velocity.length() > 1.0:
            var angular_rotation = 10
            mesh_node.rotation.y = lerp_angle(mesh_node.rotation.y, atan2(velocity.x, velocity.z) - rotation.y, delta * angular_rotation)
```