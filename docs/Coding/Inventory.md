InventoryData is a Resource. It has an Array that can hold SlotData. 
SlotData holds ItemData and quantity. ItemData holds all information on a specific item (name, description, stackable, texture). 
There is another Resource type named ItemDataEquip that inherits all parameters from ItemData but extends it with all needed parameters for equipment.

If Slots are updated (item-pickup, dragNdrop, etc.) it updates InventoryData via signals. It then sends a signal to InventoryInterface to update the visuals.

![Inventory drawio](https://github.com/user-attachments/assets/2475fe21-c277-4073-bd18-7b70ae014064)
