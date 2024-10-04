## Making Enums global

Often, we need to use the same enum multiple times across scenes and scripts. We do not want to have to define it multiple times as we would need to update it everywhere every time and that would be extremly prone to errors.

## Implementation

The created script "enum.gd" contains all enums used throughout the game. In project settings, the script is set as a global to be autoloaded. 

> https://docs.godotengine.org/en/stable/tutorials/scripting/singletons_autoload.html

![{953EC82D-2563-4966-956E-45394CB26BFE}](https://github.com/user-attachments/assets/3fb816b6-e899-4e75-8c5a-8871f3042b47)

The scripts used by the Beehave plugin are also autoloaded by the godot engine before any other scene and node.

When referencing the enum in scripts, first the script `Enum` must be referenced:

![{A25BACB6-D7E2-4CB4-BE8F-B60B436D2F5A}](https://github.com/user-attachments/assets/ea5b4153-bfc1-47f8-9ef2-5e4951cbf2fa)

## Bitshifting the enum value

Instead of either not assigning an integer value to the Enum or asigning it the numbers 1, 2, ..., we use the bitshift operator LEFTSHIFT `<<` like this:

```py linenums="1"
enum Condition {
  INVULNERABLE = 1 << 0, 
  BURNING = 1 << 1,
  SLOWED = 1 << 2,
  ...
}
```

### Why do we do this? 

There are a few benefits from doing this:

- Performance Optimization: Might or might not be applicable in our context, but we do not loose anything by doing it and only win if we optimize the game flow
> #### Would bit shifting be useful in game development?
> Bit shifting can be very useful in game development, especially for tasks that require performance optimization. It's often used in graphics programming, for manipulating pixel data, or in systems where memory and processing efficiency are critical. Bit shifting allows developers to perform operations quickly, which is essential for maintaining high frame rates in games.
> (https://www.lenovo.com/us/en/glossary/bit-shift/?orgRef=https%253A%252F%252Fwww.google.com%252F)
- Fun things we can do: We can assigning multiple enum values to one attribute, which is much more performant compared to using arrays or dictionaries.

### Example 

An entity (Player/Enemy/...) can have multiple active conditions, which affect its stats etc. Before, I would have implemented this by using either (A) an Dictionary with all possible conditions and assign a boolean to it or (B) an Array containing all active conditions. In both cases, it would entail a lot of performance looking through the Dictionary or Array to find the right value.

Instead, we create an attribute `condition` of type Enum.Condition and can assign new conditions, remove conditions and check for specific conditions using bitwise operators `|`, `^` and `&`:

We assign new values using `|` (bitwise OR)
```py linenums="1"
var current_condition = Enum.Condition.SLOWED       # = 00000100
current_condition |= Enum.Condition.BURNING         # 00000100 | 00000010 = 00000110
```

We remove values using `^` (bitwise XOR)
```py linenums="1"
current_condition ^= Enum.Condition.BURNING         # 00000110 ^ 00000010 = 00000110
```

We check for values using `&` (bitwise AND)
```py linenums="1"
if current_condition & Enum.Condition.SLOWED        # 00000110 & 00000100 = 00000100 => true
  print("Entity is slowed")
if current_condition & Enum.Condition.INVULNERABLE  # 00000110 & 00000001 = 00000000 => false
  print("Entity is invulnerable")
```
### Sources

> What is Bitshift (IBM): https://www.ibm.com/docs/en/i/7.3?topic=expressions-bitwise-left-right-shift-operators
> 
> Discussion regarding this in Reddit: https://www.reddit.com/r/godot/comments/hb382k/bitwise_operations_bit_flags/
> 
> Bitshift in C++: https://stackoverflow.com/questions/18841113/c-assigning-enums-explicit-values-using-bit-shifting
