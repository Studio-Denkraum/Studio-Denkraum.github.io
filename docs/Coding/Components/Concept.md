## Motivation

Instead of implementing complex inheritance hierachies, where we would very quickly loose track of where what happens, we decided to implement functionalities as cohesive modules (-> components). 

The aim is to use these almost as black boxes, to build complex abilities/enemies/npcs/etc.

## Implementation

To build a new component, we create **(1) a scene** made up only of a root node of type Node. To this scene we attach **(2) a script** with the same node, containing all the functionality of the component. 
We need a scene, so that we can use the component as module in other scenes, by simply drag-and-dropping them into the scene. 

### File Structure

The components are stored in a /component folder under /game. For each component, we create a new folder with the components name containing the same named scene and connected script.

### Properties

With the @export keyword, we can make properties used by the component appear in the editor. This way, we can write our component in a way, 
that the user of the component only needs to set the appropriate properties in order to use it. That way, the person does not have to take a look at the components code itself (-> black box).

## Example

*In the file structure*

![image](https://github.com/user-attachments/assets/e4e52bec-de34-4086-8c42-f91656f44c5e)

*The component scene*

![image](https://github.com/user-attachments/assets/9f49f992-aa10-41a9-a4aa-919f36fbf88c)

*Used in a scene*

![image](https://github.com/user-attachments/assets/b8ec3012-037d-475b-8946-692a767c5fba)

> Using ##, we can add descriptions to the exported properties as well as the component itself, making it even more self-explanatory.

*Component's properties in Editor*

![image](https://github.com/user-attachments/assets/241db417-1698-4c2f-b814-bd6fc3923ff0)

