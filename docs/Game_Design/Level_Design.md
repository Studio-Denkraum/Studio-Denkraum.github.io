### Level Design

Zum Thema Design der "Level"/Räume/Biome Map
-> finde es sehr cool, dass es bei [Celeste](https://www.youtube.com/watch?v=cX9NJPwseIQ&ab_channel=EncryptedDuck) Chapter gibt, in denen sich der Mood visuell und von der Musik her stark unterscheidet

#### Level-Ideen
- Verlassende Gleise / Bahnstation (komplett Überwuchert, vereinzelnt Züge / Abteile)

***

**3D Background/Tilemap:**
Nach kurzer Recherche hab ich herausgefunden, dass man in Godot GripMaps (https://docs.godotengine.org/en/stable/tutorials/3d/using_gridmaps.html) benutzen kann.

"Enter the gungeon" benutzt dasselbe Prinzip, um einen 2.5D look zu generieren:
![image](https://github.com/Androx765/Game_dev/assets/63010306/33124ea4-2cce-4d91-833d-44f0599fc977)

Mehr Insight dazu:
https://www.youtube.com/watch?v=XK5qpEmUA6w
Wichtig ist Orthogonal Camera!

Texturen austauschen für Gridmap MeshLibrary:
https://www.reddit.com/r/godot/comments/y1c913/problem_with_glb_meshes/
Tldr: Changing Textures on a MeshLibrary/Gridmap is not doable. Probably have to create a new MeshLibrary and place Tiles again?

***
