# Classes vs Data Classes in Python

Data classes in Python reduce boilerplate code when the main objective of the class is store data. 

I explained the benefits of regular classes in [[Why Classes are Important in OOP - Python Examples]]. However, I have found that classes create difficulties when representing structured data. 

Data classes give us efficient, consistent code and allow us to leverage type hints. 

## Structured Data as a Regular Class in Python
Here is a simple class for a book. 
```python
class Book():
    def __init__(self, title: str, author: str, year: int):
        self.title = title
        self.author = author
        self.year = year
        
def main() -> None:
    book = Book(title="Control Systems Engineering", author="Norman S. Nise", year=2015)
    print(book)
    
if __name__ == "__main__":
    main()
```

The print(book) output of this is not very useful. 
```bash
<__main__.Book object at 0x000002AD9A4E1290>
```

To fix this, you could add a dunder method to the Book class. 
```python
class Book():
    def __init__(self, title: str, author: str, year: int):
        self.title = title
        self.author = author
        self.year = year
        
    def __str__(self) -> str:
        return f"{self.title}, {self.author}, {self.year}"
```

Now, the output is useful, but that took some effort. 
```bash
Control Systems Engineering, Norman S. Nise, 2015
```

Now, imagine needing to add an attribute about a book such as the `genre`. You would need to update this in at least three places. 
1. The __init__ signature.
2. The attribute assignment list. 
3. The dunder method. 

There is a better way. 

## Data Classes are Better for Structured Data in Python
Here you will see a much less verbose class compared to the original class. 
```python
from dataclasses import dataclass

@dataclass 
class Book:
    title: str
    author: str
    year: int        
    
def main() -> None:
    book = Book(title="Control Systems Engineering", author="Norman S. Nise", year=2015)
    print(book)
    
if __name__ == "__main__":
    main()
```

And when you print the object, you get a much more readable response without the extra dunder method which must be maintained with changes. 
```bash
Book(title='Control Systems Engineering', author='Norman S. Nise', year=2015)
```

Now, in order to add that genre we mentioned, all you need to do is update one location within the class. 
```python
@dataclass 
class Book:
    title: str
    author: str
    year: int 
    genre: str 
```

And when you update the date, you'll easily get what you need. 
```bash
Book(title='Control Systems Engineering', author='Norman S. Nise', year=2015, genre='engineering textbook')
```

## When to use each? 
Deciding when to use regular classes vs data classes is pretty straightforward. 
- Use regular classes when you need to encapsulate complex behavior. 
- Use data classes when you need to store data and want type hints. 

## Other Features of Data Classes to Learn About
- Default values
- Excluding arguments from the initializer 
- Use post_init to generate attributes
- Private/protected members
- Excluding data from the repr
- Freezing a data class
