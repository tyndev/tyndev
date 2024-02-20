# Issues with Mutable Default Arguments and Class Attributes

The key takeaway here is to be cautious when using mutable items like lists as default arguments and class-level default attributes. 

I have ran into this problem a few times as a new developer and learned my lesson.

The solution is to try to only use immutable objects (e.g., tuples) as default arguments. When necessary, mutable defaults must be initialized within the function or method body.

## Functions: Avoid Mutable Default Arguments
**Issue**: Using mutable default arguments like lists can lead to unexpected behavior. For example, if you call the function more than once, your list won't be reset to empty as it maintains the mutable object's data after the original default is set at interpret time.

**Solution**: Use `None` as a default value and initialize the list inside the function.

```python
def add_player(team=None):
    if team is None:
        team = []
    team.append("New Player")
    return team
```

## Classes: Avoid Mutable Class Attributes
**Issue**: Mutable class attributes are shared across all instances, potentially leading to data sharing where it's not intended.

**Solution**: Initialize mutable objects like lists in the `__init__` method to ensure they are unique to each instance.

```python
class SoccerTeam:
    def __init__(self):
        self.players = []

    def add_player(self, player_name):
        self.players.append(player_name)
```

## Data Classes: Use Default Factory for Mutable Attributes
**Issue**: Mutable default values in data classes is a similar issue to mutable class attributes.

**Solution**: Initialize default mutable objects with the `default_factory` keyword arhguemnt which is part of the `field` function in Python's `Dataclasses`. 

```python
from dataclasses import dataclass, field

@dataclass
class Player:
    name: str
    nicknames: list[str] = field(default_factory=list)
```

### Summary
- For functions, initialize lists (or other mutable objects) within the function body if using them as default arguments.
- For class attributes that are mutable, always initialize them in the `__init__` method to avoid sharing between instances.
- For data class default attribute values, use `default_factory`to avoid sharing between instances.
