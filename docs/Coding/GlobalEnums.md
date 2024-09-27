## Motivation

Often, we need to use the same enum multiple times across scenes and scripts. We do not want to have to define it multiple times as we would need to update it everywhere every time and that would be extremly prone to errors.

## Implementation

The created script "enum.gd" contains all enums used throughout the game. In project settings, the script is set as a global to be autoloaded. 

> https://docs.godotengine.org/en/stable/tutorials/scripting/singletons_autoload.html

![{953EC82D-2563-4966-956E-45394CB26BFE}](https://github.com/user-attachments/assets/3fb816b6-e899-4e75-8c5a-8871f3042b47)

The scripts used by the Beehave plugin are also autoloaded by the godot engine before any other scene and node.

When referencing the enum in scripts, first the script must be referenced:

![{A25BACB6-D7E2-4CB4-BE8F-B60B436D2F5A}](https://github.com/user-attachments/assets/ea5b4153-bfc1-47f8-9ef2-5e4951cbf2fa)
