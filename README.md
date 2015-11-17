# Pythine - A micro-framework that automatically parallel your python function   

## Pythine Is Fun

```python
import requests
from Pythine import Pythine

@Pythine.map(thread_num=5)
def slow_network(url, timeout=1):
    return requests.get(url, timeout=timeout).text

slow_network([
'http://www.google.com',
'http://www.microsoft.com',
'http://www.facebook.com'
] * 30)
```

The `slow_network` function will be automatically paralleled in `5` threads.

## And Easy to Use

Run in your bash
```bash
sudo pip install Pythine
```
And it's enough to get Pythine in your box.

Before using `pip`, you need to install
```bash
sudo apt-get install python-pip
```

## FAQ

### I find Pythine slows down my function! Why?

Pythine will parallel your function in CPU threads, which only benefits from heavy-job parallelism. So if your function is very efficient, e.g.
```python
def add(a):
  return a+1
```
, Pythine will definitely slow down the process!

However, we are still working on accelerate this case.

So **please only Pythine the heavy-job function.**

### The result is not as my expectation!

The reason might be:

  - (Highly possible) You need to make the function you want to Pythine threaded-safe. Sometimes the write conflict can cause a mess.
  - To be continued!

## Future Plan

1. Try to make parallelism more efficient. e.g. if the user give a large list to map, we partition the task list to sub-task lists to make each thread task heavier, which will benefit more from multi-threaded.

## Contribute

You're more than welcome to contribute by forking this repo and sending pull requests! Although we believe the concept in Pythine is very charming, the Pythine is still not perfect. We're continuously working on improving it.    
