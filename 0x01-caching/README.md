# 0x01. Caching

## More Info
### Parent class `BaseCaching`
All your classes must inherit from `BaseCaching` defined below:
```bash
$ cat base_caching.py
```
```py
#!/usr/bin/python3
""" BaseCaching module
"""

class BaseCaching():
    """ BaseCaching defines:
      - constants of your caching system
      - where your data are stored (in a dictionary)
    """
    MAX_ITEMS = 4

    def __init__(self):
        """ Initiliaze
        """
        self.cache_data = {}

    def print_cache(self):
        """ Print the cache
        """
        print("Current cache:")
        for key in sorted(self.cache_data.keys()):
            print("{}: {}".format(key, self.cache_data.get(key)))

    def put(self, key, item):
        """ Add an item in the cache
        """
        raise NotImplementedError("put must be implemented in your cache class")

    def get(self, key):
        """ Get an item by key
        """
        raise NotImplementedError("get must be implemented in your cache class")
```


## Tasks
### [0. Basic dictionary](./0-basic_cache.py)

Create a class `BasicCache` that inherits from `BaseCaching` and is a caching system:

- [x] You must use `self.cache_data` - dictionary from the parent class `BaseCaching`
- [x] This caching system doesn’t have limit
- [x] `def put(self, key, item):`
    - [x] Must assign to the dictionary `self.cache_data` the item value for the `key` key.
    - [x] If `key` or `item` is `None`, this method should not do anything.
- [x] `def get(self, key):`
    - [x] Must return the value in `self.cache_data` linked to `key`.
    - [x] If `key` is `None` or if the `key` doesn’t exist in `self.cache_data`, return `None`.
```bash
guillaume@ubuntu:~/0x01$ cat 0-main.py
#!/usr/bin/python3
""" 0-main """
BasicCache = __import__('0-basic_cache').BasicCache

my_cache = BasicCache()
my_cache.print_cache()
my_cache.put("A", "Hello")
my_cache.put("B", "World")
my_cache.put("C", "Holberton")
my_cache.print_cache()
print(my_cache.get("A"))
print(my_cache.get("B"))
print(my_cache.get("C"))
print(my_cache.get("D"))
my_cache.print_cache()
my_cache.put("D", "School")
my_cache.put("E", "Battery")
my_cache.put("A", "Street")
my_cache.print_cache()
print(my_cache.get("A"))

guillaume@ubuntu:~/0x01$ ./0-main.py
Current cache:
Current cache:
A: Hello
B: World
C: Holberton
Hello
World
Holberton
None
Current cache:
A: Hello
B: World
C: Holberton
Current cache:
A: Street
B: World
C: Holberton
D: School
E: Battery
Street
guillaume@ubuntu:~/0x01$ 
```
  
### [1. FIFO caching](./1-fifo_cache.py)

Create a class `FIFOCache` that inherits from `BaseCaching` and is a caching system:

- [x] You must use `self.cache_data` - dictionary from the parent class `BaseCaching`
- [x] You can overload `def __init__(self):` but don’t forget to call the parent init: `super().__init__()`
- [x] `def put(self, key, item):`
    - [x] Must assign to the dictionary `self.cache_data` the `item` value for the `key` key.
    - [x] If `key` or `item` is `None`, this method should not do anything.
    - [x] If the number of items in `self.cache_data` is higher that `BaseCaching.MAX_ITEMS:`
        - [x] you must discard the first `item` put in cache (`FIFO` algorithm)
        - [x] you must print `DISCARD:` with the `key` discarded and following by a new line
- [x] `def get(self, key):`
    - [x] Must return the value in `self.cache_data` linked to `key`.
    - [x] If `key` is `None` or if the `key` doesn’t exist in `self.cache_data`, return `None`.

```bash
guillaume@ubuntu:~/0x01$ cat 1-main.py
#!/usr/bin/python3
""" 1-main """
FIFOCache = __import__('1-fifo_cache').FIFOCache

my_cache = FIFOCache()
my_cache.put("A", "Hello")
my_cache.put("B", "World")
my_cache.put("C", "Holberton")
my_cache.put("D", "School")
my_cache.print_cache()
my_cache.put("E", "Battery")
my_cache.print_cache()
my_cache.put("C", "Street")
my_cache.print_cache()
my_cache.put("F", "Mission")
my_cache.print_cache()

guillaume@ubuntu:~/0x01$ ./1-main.py
Current cache:
A: Hello
B: World
C: Holberton
D: School
DISCARD: A
Current cache:
B: World
C: Holberton
D: School
E: Battery
Current cache:
B: World
C: Street
D: School
E: Battery
DISCARD: B
Current cache:
C: Street
D: School
E: Battery
F: Mission
guillaume@ubuntu:~/0x01$ 
```
  
### [2. LIFO Caching](./2-lifo_cache.py)

Create a class `LIFOCache` that inherits from `BaseCaching` and is a caching system:

- [x] You must use `self.cache_data` - dictionary from the parent class `BaseCaching`
- [x] You can overload `def __init__(self):` but don’t forget to call the parent init: `super().__init__()`
- [x] `def put(self, key, item):`
    - [x] Must assign to the dictionary `self.cache_data` the `item` value for the `key` key.
    - [x] If `key` or `item` is `None`, this method should not do anything.
    - [x] If the number of `items` in `self.cache_data` is higher that `BaseCaching.MAX_ITEMS`:
        - [x] you must discard the last `item` put in cache (`LIFO` algorithm)
        - [x] you must print `DISCARD:` with the `key` discarded and following by a new line
- [x] `def get(self, key):`
    - [x] Must return the value in `self.cache_data` linked to key.
    - [x] If `key` is `None` or if the `key` doesn’t exist in `self.cache_data`, return `None`.
```bash
guillaume@ubuntu:~/0x01$ cat 2-main.py
#!/usr/bin/python3
""" 2-main """
LIFOCache = __import__('2-lifo_cache').LIFOCache

my_cache = LIFOCache()
my_cache.put("A", "Hello")
my_cache.put("B", "World")
my_cache.put("C", "Holberton")
my_cache.put("D", "School")
my_cache.print_cache()
my_cache.put("E", "Battery")
my_cache.print_cache()
my_cache.put("C", "Street")
my_cache.print_cache()
my_cache.put("F", "Mission")
my_cache.print_cache()
my_cache.put("G", "San Francisco")
my_cache.print_cache()

guillaume@ubuntu:~/0x01$ ./2-main.py
Current cache:
A: Hello
B: World
C: Holberton
D: School
DISCARD: D
Current cache:
A: Hello
B: World
C: Holberton
E: Battery
Current cache:
A: Hello
B: World
C: Street
E: Battery
DISCARD: C
Current cache:
A: Hello
B: World
E: Battery
F: Mission
DISCARD: F
Current cache:
A: Hello
B: World
E: Battery
G: San Francisco
guillaume@ubuntu:~/0x01$
```

### [3. LRU Caching](./3-lru_cache.py)

Create a class `LRUCache` that inherits from `BaseCaching` and is a caching system:

- [x] You must use `self.cache_data` - dictionary from the parent class `BaseCaching`
- [x] You can overload `def __init__(self):` but don’t forget to call the parent init: `super().__init__()`
- [x] `def put(self, key, item)`:
    - [x] Must assign to the dictionary `self.cache_data` the `item` value for the `key` key.
    - [x] If `key` or `item` is `None`, this method should not do anything.
    - [x] If the number of items in `self.cache_data` is higher that `BaseCaching.MAX_ITEMS`:
        - [x] you must discard the least recently used `item` (LRU algorithm)
        - [x] you must print DISCARD: with the `key` discarded and following by a new line
- [x] `def get(self, key):`
    - [x] Must return the value in `self.cache_data` linked to `key`.
    - [x] If `key` is `None` or if the key doesn’t exist in `self.cache_data`, return `None`.
```bash
guillaume@ubuntu:~/0x01$ cat 3-main.py
#!/usr/bin/python3
""" 3-main """
LRUCache = __import__('3-lru_cache').LRUCache

my_cache = LRUCache()
my_cache.put("A", "Hello")
my_cache.put("B", "World")
my_cache.put("C", "Holberton")
my_cache.put("D", "School")
my_cache.print_cache()
print(my_cache.get("B"))
my_cache.put("E", "Battery")
my_cache.print_cache()
my_cache.put("C", "Street")
my_cache.print_cache()
print(my_cache.get("A"))
print(my_cache.get("B"))
print(my_cache.get("C"))
my_cache.put("F", "Mission")
my_cache.print_cache()
my_cache.put("G", "San Francisco")
my_cache.print_cache()
my_cache.put("H", "H")
my_cache.print_cache()
my_cache.put("I", "I")
my_cache.print_cache()
my_cache.put("J", "J")
my_cache.print_cache()
my_cache.put("K", "K")
my_cache.print_cache()

guillaume@ubuntu:~/0x01$ ./3-main.py
Current cache:
A: Hello
B: World
C: Holberton
D: School
World
DISCARD: A
Current cache:
B: World
C: Holberton
D: School
E: Battery
Current cache:
B: World
C: Street
D: School
E: Battery
None
World
Street
DISCARD: D
Current cache:
B: World
C: Street
E: Battery
F: Mission
DISCARD: E
Current cache:
B: World
C: Street
F: Mission
G: San Francisco
DISCARD: B
Current cache:
C: Street
F: Mission
G: San Francisco
H: H
DISCARD: C
Current cache:
F: Mission
G: San Francisco
H: H
I: I
DISCARD: F
Current cache:
G: San Francisco
H: H
I: I
J: J
DISCARD: G
Current cache:
H: H
I: I
J: J
K: K
guillaume@ubuntu:~/0x01$ 
```
   
### [4. MRU Caching](./4-mru_cache.py)

Create a class `MRUCache` that inherits from `BaseCaching` and is a caching system:

- [x] You must use `self.cache_data` - dictionary from the parent class `BaseCaching`
- [x] You can overload `def __init__(self)`: but don’t forget to call the parent init: `uper().__init__()`
- [x] `def put(self, key, item):`
    - [x] Must assign to the dictionary `self.cache_data` the `item` value for the `key` key.
    - [x] If `key` or `item` is `None`, this method should not do anything.
    - [x] If the number of items in `self.cache_data` is higher that `BaseCaching.MAX_ITEMS`:
        - [x] you must discard the most recently used `item` (MRU algorithm)
        - [x] you must print `DISCARD:` with the `key` discarded and following by a new line
- [x] `def get(self, key):`
    - [x] Must return the value in `self.cache_data` linked to key.
    - [x] If `key` is `None` or if the `key` doesn’t exist in `self.cache_data`, return `None`.
```bash
guillaume@ubuntu:~/0x01$ cat 4-main.py
#!/usr/bin/python3
""" 4-main """
MRUCache = __import__('4-mru_cache').MRUCache

my_cache = MRUCache()
my_cache.put("A", "Hello")
my_cache.put("B", "World")
my_cache.put("C", "Holberton")
my_cache.put("D", "School")
my_cache.print_cache()
print(my_cache.get("B"))
my_cache.put("E", "Battery")
my_cache.print_cache()
my_cache.put("C", "Street")
my_cache.print_cache()
print(my_cache.get("A"))
print(my_cache.get("B"))
print(my_cache.get("C"))
my_cache.put("F", "Mission")
my_cache.print_cache()
my_cache.put("G", "San Francisco")
my_cache.print_cache()
my_cache.put("H", "H")
my_cache.print_cache()
my_cache.put("I", "I")
my_cache.print_cache()
my_cache.put("J", "J")
my_cache.print_cache()
my_cache.put("K", "K")
my_cache.print_cache()

guillaume@ubuntu:~/0x01$ ./4-main.py
Current cache:
A: Hello
B: World
C: Holberton
D: School
World
DISCARD: B
Current cache:
A: Hello
C: Holberton
D: School
E: Battery
Current cache:
A: Hello
C: Street
D: School
E: Battery
Hello
None
Street
DISCARD: C
Current cache:
A: Hello
D: School
E: Battery
F: Mission
DISCARD: F
Current cache:
A: Hello
D: School
E: Battery
G: San Francisco
DISCARD: G
Current cache:
A: Hello
D: School
E: Battery
H: H
DISCARD: H
Current cache:
A: Hello
D: School
E: Battery
I: I
DISCARD: I
Current cache:
A: Hello
D: School
E: Battery
J: J
DISCARD: J
Current cache:
A: Hello
D: School
E: Battery
K: K
guillaume@ubuntu:~/0x01$ 
```
   
### [5. LFU Caching](./100-lfu_cache.py)

Create a class `LFUCache` that inherits from `BaseCaching` and is a caching system:

- [x] You must use `self.cache_data `- dictionary from the parent class `BaseCaching`
- [x] You can overload `def __init__(self):` but don’t forget to call the parent init: `super().__init__()`
- [x] `def put(self, key, item):`
    - [x] Must assign to the dictionary `self.cache_data` the `item` value for the `key` key.
    - [x] If `key or `item` is `None`, this method should not do anything.
    - [x] If the number of `items` in `self.cache_data` is higher that `BaseCaching.MAX_ITEMS`:
        - [x] you must discard the least frequency used `item` (LFU algorithm)
        - [x] if you find more than 1 `item` to discard, you must use the `LRU` algorithm to discard only the least recently used
        - [x] you must print `DISCARD:` with the `key` discarded and following by a new line
- [x] `def get(self, key):`
    - [x] Must return the value in `self.cache_data` linked to `key`.
    - [x] If `key` is `None` or if the `key` doesn’t exist in `self.cache_data`, return `None.`

```sh
guillaume@ubuntu:~/0x01$ cat 100-main.py
#!/usr/bin/python3
""" 100-main """
LFUCache = __import__('100-lfu_cache').LFUCache

my_cache = LFUCache()
my_cache.put("A", "Hello")
my_cache.put("B", "World")
my_cache.put("C", "Holberton")
my_cache.put("D", "School")
my_cache.print_cache()
print(my_cache.get("B"))
my_cache.put("E", "Battery")
my_cache.print_cache()
my_cache.put("C", "Street")
my_cache.print_cache()
print(my_cache.get("A"))
print(my_cache.get("B"))
print(my_cache.get("C"))
my_cache.put("F", "Mission")
my_cache.print_cache()
my_cache.put("G", "San Francisco")
my_cache.print_cache()
my_cache.put("H", "H")
my_cache.print_cache()
my_cache.put("I", "I")
my_cache.print_cache()
print(my_cache.get("I"))
print(my_cache.get("H"))
print(my_cache.get("I"))
print(my_cache.get("H"))
print(my_cache.get("I"))
print(my_cache.get("H"))
my_cache.put("J", "J")
my_cache.print_cache()
my_cache.put("K", "K")
my_cache.print_cache()
my_cache.put("L", "L")
my_cache.print_cache()
my_cache.put("M", "M")
my_cache.print_cache()

guillaume@ubuntu:~/0x01$ ./100-main.py
Current cache:
A: Hello
B: World
C: Holberton
D: School
World
DISCARD: A
Current cache:
B: World
C: Holberton
D: School
E: Battery
Current cache:
B: World
C: Street
D: School
E: Battery
None
World
Street
DISCARD: D
Current cache:
B: World
C: Street
E: Battery
F: Mission
DISCARD: E
Current cache:
B: World
C: Street
F: Mission
G: San Francisco
DISCARD: F
Current cache:
B: World
C: Street
G: San Francisco
H: H
DISCARD: G
Current cache:
B: World
C: Street
H: H
I: I
I
H
I
H
I
H
DISCARD: B
Current cache:
C: Street
H: H
I: I
J: J
DISCARD: J
Current cache:
C: Street
H: H
I: I
K: K
DISCARD: K
Current cache:
C: Street
H: H
I: I
L: L
DISCARD: L
Current cache:
C: Street
H: H
I: I
M: M
guillaume@ubuntu:~/0x01$ 
```