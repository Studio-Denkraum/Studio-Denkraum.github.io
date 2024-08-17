# Abilities and UI

## Filesystem

```
res://scenes/game  
	abilities  
		active_abilities  
			ability1  
				ability1.gd (inherits from active_ability.gd)  
				ability1.tscn (scene with ability1.gd script and ability1 "model"  
			ability2  
				ability2.gd  
				ability2.tscn  
			active_ability.gd (Basis class)  
		passive_abilities  
			
			passive_ability.gd (Basis class)  
	ability_ui  
		active_abilities  
			ability1  
				ability1.tres (Resource of ability.gd with own name)  
			ability2  
				ability2.tres  
		passive_abilities  
				
		ability_inventory.tscn (scene with ability-UI)
		ability_inventory.tres (Stores arrays of selected active abilities and passives)
		ability_inventory.gd (inherits from resource, own class_name, defines arrays)
		ability.gd (inherits from resource, own class_name, has variable “name: String”)
		+ further UI-Nodes
```

## Relation of Ability System and UI

Player-script looks at which abilities are added to the ability_inventory (are contained in ability_inventory.tres). 
The name of each ability is taken and loaded.
the ability_inventory.tscn node is instantiated as a child instance
