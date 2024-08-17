## Usage

The script Entity serves as a base for the player node as well as the enemy and npc nodes. 
It contains basic attributes to describe the states of health, energy etc. as well as functions to modify these states. 
With load_ability, abilities used by the entity can be loaded in the scene.

![gameDev_baseEntity](https://github.com/user-attachments/assets/2daec1a7-3848-47a1-a36e-456f32d945ef)

The attribute "Resistence" could be implemented with a dictionary as follows:

```py linenums="1"
enum DAMAGE_TYPE {FIRE, ICE, ...}

// Example: the player is vulnerable against Fire damage 
// and resistent against Ice damage
var resistance = {DAMAGE_TYPE.FIRE: -10, DAMAGE_TYPE.ICE: 10}
```

## Implementation

Attributes include basic stats like Health, Energy, Armor and movement & physic specific stats: 
- (current and maximal) speed / velocity: How fast does the entity move? 
- acceleration: How fast does the entity get fast? ("the rate of change of the velocity of an object")
- agility: How fast can the entity turn? (not used, instead currently **angular_rotation** in Player Node)

The functions include modifying these values as well as loading abilites. This makes the modular implementation of abilities possible.
