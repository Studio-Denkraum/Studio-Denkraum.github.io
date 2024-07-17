# Base Entity

## Usage

The script Entity serves as a base for the player node as well as the enemy and npc nodes. 
It contains basic attributes to describe the states of health, energy etc. as well as functions to modify these states. 
With load_ability, abilities used by the entity can be loaded in the scene.

![gameDev_baseEntity](https://github.com/user-attachments/assets/2daec1a7-3848-47a1-a36e-456f32d945ef)

The attribute "Resistence" could be implemented with a dictionary as follows:

```py linenums="1"
enum DAMAGE_TYPE {FIRE, ICE, ...}

var resistance = {DAMAGE_TYPE.FIRE: 0, DAMAGE_TYPE.ICE: 10}
```

# Implementation in Godot

❤️
