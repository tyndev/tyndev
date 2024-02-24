# How to Get Concurrency with Synchronous Requests in Python
Below is a summary of my learnings on concurrent programming with HTTP requests in Python as an example. 
## Types of Concurrency
First, I think it is helpful to understand the difference between concurrent, asynchronous, and parallel. 
- **Concurrent**: this is the ability of a program to make progress on multiple tasks seemingly at the same time.
	- **Asynchronous**: this means the program is able to switch to other tasks while waiting for a slow task to finish. 
	- **Parallel**: this means the program is able to run multiple tasks/threads at the exact same time. 

Asynchronous and parallel programming are distinct, however, both are ways to accomplish concurrency. 

Python can be asynchronous, but not parallel. 
## Synchronous vs Asynchronous - A Real Life Example
As an electrical engineer in the power industry, when I think of the words `asynchronous` and `synchronous`, I think of generators, motors, and faults. 

But I'll use a simple day-to-day example which really helps me understand more intuitively these terms in the context of software development: 
- Meetings are synchronous
- Email is asynchronous 

In meetings, only one person talks at a time and everyone is expected to focus on the speaker until they have an opportunity to talk. This is synchronous. 

In email, one person sends an email and is able to work on something else while they wait for a response. This is asynchronous. 

## How to Make Requests Asynchronous in Python
Some functions like those in the `requests` library are synchronous or non-concurrent. However, they can be made asynchronous with the use of the `asyncio` library. 

The `requests` library in Python makes HTTP requests to web servers **synchronously.** This means the main event loop has to pause and wait for an HTTP request before moving on on to something else. It is a blocking function. 

The following code can be used to turn synchronous `requests` into asynchronous `requests`. 

```python
import asyncio
import requests

JSON = int | str | float | bool | None | dict[str, "JSON"] | list["JSON"]
JSONObject = dict[str, JSON]
JSONList = list[JSON]

def http_get_sync(url: str) -> JSONObject:
    response = requests.get(url)
    return response.json()

async def http_get(url: str) -> JSONObject:
    return await asyncio.to_thread(http_get_sync, url)
```

While this method is one way to make synchronous `requests` asynchronous, there are other libraries and approaches available that are designed to handle HTTP requests asynchronously (such as `aiohttp`).
