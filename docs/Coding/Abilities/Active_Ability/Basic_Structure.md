##Where do I create a new Ability

All abilitys are saved in the "abilities" folder. 

##File Naming 

Because of the way abilities are loaded it is **very** important that the folder and the script have the same name.

![image](https://github.com/user-attachments/assets/05952247-11c3-4c9a-9b18-e8b0558360d9)


##Components of an Ability

The minimal requirements of an ability is a node3D with the same name as the ability.
Here a script controlls the fundamental executions and therefore **requires** a function with the name "execute".

The main functionality of the ability is handeled in components which are added as childen to the root node. 

![image](https://github.com/user-attachments/assets/2f62d744-efc4-431b-aa45-c572d8fccfd9)

