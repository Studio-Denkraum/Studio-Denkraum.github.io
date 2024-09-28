## Description

Entities such as the Player, NPCs, Enemies, Bossess, ... get a **Hurtbox** --> did something hurt me?

Abilities such as the AOE or Projectiles get a **Hitbox** --> did I hit something? 

The HurtboxComponent works in synergy with the StatComponent. Therefore the StatComponent is necessary to have the full effect of the Hurtbox aka the Entity not only getting hit but also getting damage from that hit.

## How to Use

The HitboxComponent and HurtboxComponent only fully work, when both are implemented.

### HitboxComponent

Usage in ProjectileComponent:

![{25DAECA2-93E6-4397-B399-8DEAAE448E25}](https://github.com/user-attachments/assets/e98ae5f6-ec89-442e-b1eb-db94b365e3b7)
![{30A0898E-B323-4AC2-82E5-C6937B375D40}](https://github.com/user-attachments/assets/815626de-1ed5-4b07-8b93-25c8710e7816)

- **ParentNode**: The root node of the Scene --> ProjectileComponent. Used instead of get_parent() to secure that the component will work in future e.g. even if nodes are added to group components.
- **Hitbox**: The actual Hurtbox (CollisionShape3D) representing the area where the entity hurts. Must be child of the HitboxComponent to connect to its signals.

### HurtboxComponent

Usage in Ramona (NPC):

![{F1F25E37-B584-47F0-B7D4-F126936903E3}](https://github.com/user-attachments/assets/2a6ae947-bc66-46e6-a9e1-4b5caa9dc83b) 
![{3E777C71-E154-4CB9-80F8-A14B30E092CF}](https://github.com/user-attachments/assets/423b4dec-e709-43bd-a3ca-5b44dca5e5a5)

- **StatComponent**: handling the changes to Health (and other effects regarding the Players stats)
- **ParentNode**: The root node of the Scene --> Ramona.
- **Hurtbox**: The actual Hurtbox (CollisionShape3D) representing where the entity can be hurt. Must be child of the HurtboxComponent to connect to its signals.

## Implementation

The two components communicate with each other using signals.

![hitbox-hurtbox-component](https://github.com/user-attachments/assets/91e11c22-ae54-41e1-abf0-7ae862149cdb)

The reason for this is, that the hitbox and hurtbox do not know the stats of the entities involved 
(in this example the health of the Player and the damage of the Ability).

- The HitboxComponents communicates that it collided with a Hurtbox to the Ability --> i_hit_something(hurtbox). 
The HitboxComponents connects to the _on_area_entered()-signal of its child (the Hitbox) to detect collision.

```py linenums="1"
# HitboxComponent.gd
extends Area3D
class_name Hitbox

@export var parent_node: Node3D
@export var hitbox: CollisionShape3D

signal i_hit_something(hurtbox)

func _on_area_entered(area3D: Area3D) -> void:
	if area3D is Hurtbox:
		i_hit_something.emit(area3D)

```

- The Ability knows its stat and sends the Hurtbox a signal containing the received damage --> get_damage(damage).

```py linenums="1"
# ProjectileComponent.gd
extends RigidBody3D

...

func _on_hitbox_component_i_hit_something(hurtbox: Hurtbox) -> void:
	hurtbox.take_damage(ability_resources.damage, ability_resources.damagetype)

```

- The Hurtbox itself does not change anything about the Player aka its health.
  Instead it relays the damage to the StatComponent, where the damage is actually taken.

```py linenums="1" 
# HurtboxComponent.gd
extends Area3D
class_name Hurtbox

@export var stat_component: Node
@export var parent_node: Node3D
@export var hurtbox: CollisionShape3D

func take_damage(damage: int, damage_type: Enum.DamageType) -> void:
	if (stat_component):
		stat_component.take_damage(damage, damage_type)
```


