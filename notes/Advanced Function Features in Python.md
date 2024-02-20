# Advanced Function Features in Python
Yesterday I learned about a few functional programming tools in Python that I'd like to document. 

These features like higher-order functions, partials, and `cached_property` can enhance code efficiency and readability. 

## Lambda Functions
Lambda functions in Python are anonymous, single-expression functions for creating quick functions that are not complex enough to require a full function definition. They are frequently used in conjunction with higher-order functions.
## Higher-Order Functions

Higher-order functions either take a function as an argument or return a function as a result. They allow flexible code reuse and abstraction.

```python
from typing import Callable

def filter_players(players: list[dict[str, str]], condition: Callable[[dict[str, str]], bool]):
    # Higher-order function to filter players based on a condition
    return [player for player in players if condition(player)]

# Usage example: filtering players by position
players = [{"name": "John Doe", "position": "forward"}, {"name": "Jane Doe", "position": "goalkeeper"}]
forwards = filter_players(players, lambda player: player["position"] == "forward")
print(forwards)  # Output: [{'name': 'John Doe', 'position': 'forward'}]
```

## Partial Function Application

Partial functions allow you to fix a certain number of arguments of a function and generate a new function.

```python
from functools import partial

def assign_player_to_team(team_name: str, player_name: str) -> None:
    print(f"{player_name} has been assigned to {team_name}")

# Creating a partial function for a specific team
assign_to_red_team = partial(assign_player_to_team, "Red Team")
# Assigning a player to the Red Team
assign_to_red_team("Alice")

```

## `cached_property` Decorator

The `cached_property` decorator caches the result of a property method in class instances. This is useful for properties with large computations.

```python
from functools import cached_property
from dataclasses import dataclass

@dataclass
class Team:
    name: str
    games_played: int
    goals_scored: int

    @cached_property
    def average_goals_per_game(self):
        print(f"Calculating average goals for {self.name}")
        return self.goals_scored / self.games_played

# Usage
team = Team("Blue Team", 10, 25)
print(team.average_goals_per_game)  # Output: 2.5
print(team.average_goals_per_game)  # Cached result, no recalculation
```

## Single Dispatch

Single dispatch allows functions to behave differently based on the type of the first argument, promoting polymorphism without having to use complex class hierarchies. 

```python
from functools import singledispatch
from typing import Any

@singledispatch
def add(x: Any, y: Any) -> Any:
    raise NotImplementedError("Unsupported type")

@add.register(int)
def _(x: int, y: int) -> int:
    return x + y

@add.register(str)
def _(x: str, y: str) -> str:
    return f"{x} {y}"


print(add(1, 2))   # Integers: 3
print(add("Hello", "World"))   # Strings: Hello World
```
