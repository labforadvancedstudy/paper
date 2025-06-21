# L3: Design Principles - Where Coding Becomes Design

*"There are only two hard things in Computer Science: cache invalidation and naming things."*
*- Phil Karlton*

*"There are only two hard things in Computer Science: cache invalidation, naming things, and convincing your manager that refactoring isn't a waste of time."*
*- Every developer ever*

## The Leap from Code to Design

A junior developer writes code that works. A senior developer writes code that others can understand. A principal engineer writes code that doesn't need to be written.

This is level 3 - where we stop thinking about what code does and start thinking about what code means.

## Algorithms: Crystallized Problem-Solving

An algorithm is a thought so clear it can be executed by a machine. It's the difference between "sort these numbers" and:

```python
def bubble_sort(arr):
    n = len(arr)
    for i in range(n):
        for j in range(n - i - 1):
            if arr[j] > arr[j + 1]:
                arr[j], arr[j + 1] = arr[j + 1], arr[j]
    return arr
```

But here's the thing - bubble sort is terrible. It's O(n²), which is computer science speak for "gets slower faster than you can imagine." Yet we teach it first. Why?

Because bubble sort is how humans think about sorting. Watch someone organize playing cards - they bubble sort. The computer science breakthrough wasn't inventing bubble sort, it was realizing we could do better:

```python
# Merge sort - O(n log n) - computer thinking, not human thinking
def merge_sort(arr):
    if len(arr) <= 1:
        return arr
    
    mid = len(arr) // 2
    left = merge_sort(arr[:mid])
    right = merge_sort(arr[mid:])
    
    return merge(left, right)
```

Merge sort is alien logic. No human naturally thinks "I'll split this in half recursively until I have single elements, then merge them back in order." But computers love it.

Algorithms are where human intuition goes to die and computational thinking is born.

## Abstraction: The Art of Productive Forgetting

Abstraction is controlled amnesia. It's the art of forgetting details on purpose.

```python
# Level 0: What's actually happening
file_handle = os.open("/tmp/data.txt", os.O_RDONLY)
data = os.read(file_handle, 1024)
os.close(file_handle)

# Level 1: Hide the file handle
with open("/tmp/data.txt", "r") as f:
    data = f.read()

# Level 2: Hide the file entirely
data = load_data()

# Level 3: Hide the loading
data = get_user_preferences()

# Level 4: Hide the concept
user.prefers_dark_mode  # What data? What file?
```

Each level forgets more details. By level 4, you've forgotten there's even a file involved. This is either beautiful or terrifying, depending on whether you're the one debugging it at 3am.

The Platonic ideal of abstraction is the button. You push it, something happens. You don't care how. Until it breaks. Then suddenly you care very much about all those forgotten details.

## Design Patterns: The Shared Hallucinations

Design patterns are like memes for code architecture. Someone solved a problem once, gave it a name, and now we all pretend it's a universal truth.

**The Singleton Pattern**: "There can only be one!"
```python
class DatabaseConnection:
    _instance = None
    
    def __new__(cls):
        if cls._instance is None:
            cls._instance = super().__new__(cls)
        return cls._instance

# No matter how many times you create it, same object
db1 = DatabaseConnection()
db2 = DatabaseConnection()
assert db1 is db2  # Same object!
```

Singletons are like Highlanders - there can be only one. Also like Highlanders, they seemed like a good idea in the 80s but now everyone realizes they cause more problems than they solve.

**The Observer Pattern**: "I'll call you, don't call me"
```python
class NewsPublisher:
    def __init__(self):
        self.subscribers = []
    
    def attach(self, subscriber):
        self.subscribers.append(subscriber)
    
    def notify(self, article):
        for sub in self.subscribers:
            sub.update(article)

class EmailSubscriber:
    def update(self, article):
        print(f"Emailing: {article}")

# The magic: publisher doesn't know about EmailSubscriber specifically
```

The Observer pattern is how we teach objects to gossip. It's also why your app has 47 different event systems that don't talk to each other.

## Testing: Proof of Correctness (Sort Of)

Testing is the art of proving your code works by showing it doesn't fail in the ways you thought to check.

```python
def add(a, b):
    return a + b

def test_add():
    assert add(2, 2) == 4
    assert add(0, 0) == 0
    assert add(-1, 1) == 0
    # Ship it! What could go wrong?

# Later...
add("2", "2")  # "22" - oops
add([1], [2])  # [1, 2] - arrays add differently
add(float('inf'), float('-inf'))  # nan - math is broken
```

Tests are like wearing a seatbelt. They won't prevent all accidents, but when things go wrong, you'll be glad they're there. Also like seatbelts, everyone agrees they're important but somehow there's never enough time to use them properly.

**The Testing Pyramid** (more like Testing Jenga):
- Unit tests: Test individual functions (fast, focused, fragile)
- Integration tests: Test components together (slower, realistic, flaky)
- End-to-end tests: Test everything (glacial, comprehensive, impossible to maintain)

The dirty secret: Most "unit" tests are secretly integration tests, most integration tests are secretly prayers, and most end-to-end tests are secretly broken.

## SOLID: The Ten Commandments (But Five)

SOLID principles are what happens when object-oriented programming goes to therapy:

**S - Single Responsibility**: "I do one thing!"
```python
# Bad: FileManagerAndEmailerAndDatabaseHandler
class GodObject:
    def save_file(self): ...
    def send_email(self): ...
    def query_database(self): ...
    def make_coffee(self): ...

# Good: Each class has one job
class FileManager:
    def save(self): ...

class EmailService:
    def send(self): ...
```

**O - Open/Closed**: "Extend me, don't change me!"
Like a restaurant that's open for business but closed for renovations. You can add new menu items but can't change the kitchen.

**L - Liskov Substitution**: "Children should behave like parents!"
If it walks like a duck and quacks like a duck, it better not explode when you try to make it swim.

**I - Interface Segregation**: "Don't make me implement methods I don't use!"
Like a Swiss Army knife where you only need the knife but you're forced to carry the toothpick, scissors, and that weird hook thing nobody knows what it's for.

**D - Dependency Inversion**: "Depend on abstractions, not concretions!"
Don't marry the implementation, date the interface.

## The Reality of Design

Here's what they don't tell you in design pattern books: All abstractions leak. Every pattern has an anti-pattern. Today's best practice is tomorrow's technical debt.

The real skill isn't knowing patterns - it's knowing when to break them. It's recognizing that sometimes the elegant solution is too clever, and the ugly solution ships on time.

```python
# The elegant way
class AbstractFactoryBuilder:
    def create_factory(self, factory_type):
        return FactoryFactory.get_factory(factory_type)

# The way that actually ships
def process_data(data):
    # TODO: Make this less awful
    # TODO: It's been 5 years, the TODO is now load-bearing
    return data.replace("bad", "good")
```

Design is where programming becomes philosophy. It's where we ask not "does it work?" but "should it work this way?" It's where we realize that code isn't just instructions for machines - it's communication between humans across time.

Every design decision is a bet about the future. Every abstraction is a promise you're making to future-you. Every test is an attempt to prove that promise isn't a lie.

The real mystery isn't how to design perfect systems. It's that despite our best efforts to design perfect systems, we keep building things that work anyway. Like a city that grows organically despite urban planning, codebases develop their own logic, their own neighborhoods, their own no-go zones.

We're not architects building cathedrals. We're gardeners tending forests that grow in fast-forward, where trees can uproot and replant themselves, and sometimes the squirrels refactor everything while you're at lunch.

---

*Next up: L4 - Systems Architecture, where we'll discover why every system eventually grows an authentication service, how microservices are like city-states (constantly at war), and why the database is always the bottleneck...*