## Functionality

Handle changes to the base stats of an entity (Player, Enemy, NPC)

## Implementation

### Properties

**stat**: StatResource
→ Resource with the entities stats (*data/stat/stat_resource.gd*)

### Stat Changes

Health and Energy can be instantiously be changed e.g. by using Energy for abilities or getting hit:

- `func take_damage(damage: int, damage_type: Enum.DamageType)`
- `func use_energy(amount: int)`
- `func heal(amount: int)`

When the entity receives damage, the damage is first filtered through the entity's resistances and the result is then applied -> `func _filter_through_resistance(damage: int, damage_type: Enum.DamageType)`

### Effects

Additionally, effects can be applied: Instead of once, stat changes are applied every tick over a set duration (or indefinitely, if set as such). An example would be a damage-over-time burning effect after getting hit by a fire ability. 

> A Tick in this case refers to our own defined one-second interval, in which effects are applied and the stats are updated.

Effects are stored in the EffectQueue and applied every tick. Effects are Resources definied by the Script EffectResource and stored under *data/effect/resources*. 

```py linenums="1"
# data/effect/effect_resource.gd
extends Resource
class_name EffectResource

## Unique identifier
@export var uid: int
## Name of the effect
@export var name := ''
## Icon for the status preview
@export var icon: Texture2D
## Associated condition. Is added at the beginning of the effect and removed at the end.
@export var condition: Enum.Condition
## Duration of effect in ticks.
## [br][code]0.0[/code] is interpreted as the effect being instantanous and only applied once.
@export var duration := 0.0
## Impact is going on indefinite
@export var indefinite := false
## How is the value applied to the base stat.
@export var procedure: Enum.StatProcedure
## Stat of the entity that is affected.
@export var stat: Enum.Stat
## Value to apply to base stat (every tick).
@export var value := 0.0
## Handling of multiple applications of the same effect.
@export var stack_type:= Enum.ImpactStackType.NOT_STACKABLE
```

#### `add_effect(effect: EffectResource)`

When a new effect is added to the Queue, it is first checked, if the same effect is already applied (comparing the effect's UID). Depending on the set StackType (Enum `Enum.ImpactStackType` under *global/enum.gd*), the effect in the queue is modified. 

- NOT_STACKABLE: Nothing is changed
- DURATION_STACKED: The duration of the effect is refreshed, when the second one is applied
- IMPACT_STACKED: The value change of the effect is applied twice as much (e.g. double burning damage)
- DURATION_AND_IMPACT_STACKED: Both the duration and the impact are stacked

#### `_apply_effects()`

Every tick, the effects in the queue are applied:

1. Check if effect has finished (AND is not indefinite) → remove effect from queue and associated condition from entity
2. Effect has not finished → Using the external script *global/utility.gd* to apply the set effect to the stat (`Utility.apply_effect(effect: EffectResource, stat_resource: StatResource)`)

To apply the effect, three values from the EffectResource are important:

- `var stat: Enum.Stat`: which stat is impacted (health, energy, ...)
- `var value := 0.0`: what value is applied in the effect?
- `var procedure: Enum.StatProcedure`: how is the value applied?

```py linenums="1"
# global/enum.gd
enum StatProcedure {
	NONE = 0 << 0,
	ADD = 1 << 0, # add the value to base stat
	MULTIPLY = 1 << 1, # multiply base stat by this value
	ADD_PERCENTAGE = 1 << 2, # add the value as percentage of the base stat
}
``` 


### Communication with StatUIComponent

To keep the UI updated, a signal is emitted each time the current energy and health value changes or whenever the entity dies.

![image](https://github.com/user-attachments/assets/7cc18e21-100f-4a03-be3c-47b5d2e13b46)

```py linenums="1"
# signals for environment and ui
signal died
signal health_changed(new_value)
signal energy_changed(new_value)
```

Additionally, the getters for these values are created to be used by the StatUIComponent.

```py linenums="1"
func get_max_health() -> int:
	return stat.health_max

func get_max_energy() -> int:
	return stat.energy_max
	
func get_current_health() -> int:
	return stat.health_current

func get_current_energy() -> int:
	return stat.energy_current
 
func get_temp_health() -> int:
	return stat.health_temp

```
