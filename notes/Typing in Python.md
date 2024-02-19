
# Typing in Python

Python is a **strongly typed** language that does not require explicit type declaration (meaning it is **dynamically typed**). However, using Type Annotations gives Python **optional static typing**. 

## Strong vs Weak Typing
**Strong** typing means that the type of a value doesn't implicitly change. Whereas **weak** typing languages will implicitly convert, for example, numbers to strings. 

For example, in Python (a strongly typed language), if you try to concatenate a string and an integer, you'll get a TypeError:

```python
s = "Hello, I am "
age = 23
print(s + age) # TypeError: can only concatenate str (not "int") to str
```

In JavaScript (a weakly typed language), if you try to concatenate a string and a number, the number will be implicitly converted into a string:

```javascript
var s = "Hello, I am ";
var age = 23;
console.log(s + age); // "Hello, I am 23"
```

## Dynamic vs Static Typing
While **dynamically typed*** languages allow you to declare a variable to be one data type and then later in the same script assign it another data type, **static typing** does not. 

Python introduced **optional static typing** in Python 3.5 through a feature called Type Annotations. It's still inherently dynamic but offers some tools for static type checking.

### Type Annotations in Python
**Type Annotations** is not intended to make Python into a statically typed language, but rather to allow for improved development practices and better IDE support. 

This is important because if you give a variable a type `str`, for example, when it is actually an `int` you won't actually get a `TypeError` at runtime. That is because Python ignores Type Annotations when it runs in order maintain its dynamic typing. 

So then why add type annotations at all? 

Because they give us a powerful resource when developing code. With them, the code is more readable. Plus, features of the IDE help us with hints and through strict type checking options in the editor when writing. 

### Duck Typing in Python
**Duck Typing** in Python simplifies an object's type. Instead of checking an object's class, Python looks at what the object can do. If an object behaves like a duck (has duck-like methods), Python treats it as a duck.

This approach is possible because Python is a dynamically typed language, meaning you don't have to declare types explicitly. For instance, both strings and lists can be used with `len()` because they implement the `__len__` dunder method, not because of their specific type. The same method can be defined for a class so that `len()` can be used on an instance of that class.

Here's a quick example:

```python
str_example = "Hello World!"
list_example = [1, 2, 3, 4]
len(str_example) # 12 (str_example must have a __len__ dunder method)
len(list_example) # 4 (list_example must have a __len__ dunder method)

class Book:
	def __init__(self, title: str, author: str, pages: int):
		self.title = title
		self.author = author
		self.pages = pages
	def __len__(self): # define len dunder for Book
		return self.pages

print(len(Book("Power Systems", "Glover", 805))) # prints 805 b/c we defined __len__
```

In essence, Python's flexibility with types allows for more general and adaptable code.
