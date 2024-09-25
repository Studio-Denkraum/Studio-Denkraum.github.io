## Enemy

Enemy is created with components. 
They use the MovementComponent with an InteractionArea3D. The enemy is walking towards the Player, if it enters the InteractionArea (detected by the corresponding group). 
If the Player leaves the InteractionArea the enemy stops moving. 
### Requirements
- all of the Environment of the Game needs to be a child of NavigationRegion3D
- Enemy needs a NavigationAgent3D
- Enemy needs InteractionArea3D