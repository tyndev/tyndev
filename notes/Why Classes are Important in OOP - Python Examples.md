 
# Why are Classes Important in Object Oriented Programming? - Python Examples

Classes are important in programming because they give you a way to consistently define a type of data in a way that can grow with your software. 

As a new software developer, I could mimic the structure of a class. 

But I didn't understand why. 

They often are not needed for simple scripts, but classes will save you time and frustration if a script ever grows into something more. 
## What are classes in programming? 
Classes are the foundational building blocks of Object-Oriented Programming (OOP), defining the structure and behavior of objects.

- A **class** is a blueprint for a type of object. 
- An **object** is an instance of a class. 
- **Attributes** store data about an object. 
- **Methods** are functions in a class that act on an object's data.

This model provides a structured approach to encapsulate data (attributes) and behaviors (methods) for organized, reusable, and scalable code.
## But why are classes actually important? 
Below is example code for a soccer player function that should have been written as a class. As you read through the code think of this example:

| class         | object       | method        | attribute | data      |
| ------------- | ------------ | ------------- | --------- | --------- |
| soccer player | Lionel Messi | scoring goals | goals     | 700 goals |
| soccer player | Peter Crouch | scoring goals | goals     | 108 goals |
### A Simple Python Function Without a Class
At first, you might not see why you would need a class with the below function describing soccer player stats. 

```python
def player_stats(name, position, goals, assists):
    return f"Name: {name}, Position: {position}, Goals: {goals}, Assists: {assists}"
```

### Adding New Variables to the Function Gets Messy
As you realize that you need more variables to capture all of the soccer player stats, the function gets out of hand. Plus, each time you add a stat, you have to update every function that needs player stats as an argument.

```python
def player_stats(name, position, goals, assists, fitness_level, matches_played, yellow_cards, red_cards, scored_goal, received_card):
    scoring_action = f"Scored {scored_goal} goal(s)" if scored_goal else "No goals this match"
    return f"""Name: {name}, Position: {position}, Goals: {goals}, Assists: {assists},
               Fitness Level: {fitness_level}%, Matches Played: {matches_played},
               Yellow Cards: {yellow_cards}, Red Cards: {red_cards},
               Match Actions: {scoring_action}, {card_action}"""
```

### Classes Fix this with Reusable and Scalable Code
Creating a 'Soccer Player' class enables you to define a new stats about the players. They instantly become available to every method that takes a soccer player argument. You can now reference these attributes or call these methods anywhere in your program. 

```python
class SoccerPlayer:
    def __init__(self, name, position, goals=0, assists=0, fitness_level=100, matches_played=0, yellow_cards=0, red_cards=0):
        self.name = name
        self.position = position
        self.goals = goals
        self.assists = assists
        self.fitness_level = fitness_level
        self.matches_played = matches_played
        self.yellow_cards = yellow_cards
        self.red_cards = red_cards
		
    def score_goal(self, number_of_goals=1):
        self.goals += number_of_goals
        return f"{self.name} scored {number_of_goals} goal(s)!"
		
    def assist(self, number_of_assists=1):
        self.assists += number_of_assists
        return f"{self.name} made {number_of_assists} assist(s)!"
		
    def show_stats(self):
        return f"""
		        Name: {self.name}, Position: {position}, 
			    Goals: {self.goals}, Assists: {self.assists}
			    """
```

## What are the trade-offs of using classes in Python? 
Notice that the original function above is much much less verbose than the class code. 

Writing a simple function is much quicker if you know that the type of thing your code is modeling will not have many attributes or behaviors. It isn't a bad thing to move fast. 

But classes slow you down now, to save time later with organized, reusable, and scalable code. 

---
Keep learning about Object-Oriented Programming:
- Encapsulation
- Inheritance
- Polymorphism
- Abstraction

Start learning about Algorithms:
- linear and binary search
- sort types: bubble, insertion, selection, merge, and quick
- DFS vs BFS (Depth vs Breadth)
- Dynamic Programming

