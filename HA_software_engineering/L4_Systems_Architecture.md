# L4: Systems Architecture - When Parts Become Whole

*"A complex system that works is invariably found to have evolved from a simple system that worked."*
*- John Gall*

*"A complex system designed from scratch never works and cannot be made to work."*
*- Also John Gall, really driving the point home*

## The Emergence of Architecture

You start with a script. Just 50 lines of Python to solve a problem. Then someone asks, "Can it send emails too?" Now it's 200 lines. "Can we add a web interface?" 2,000 lines. "Can it scale to millions of users?"

Congratulations. You now have an architecture. You didn't design it. It happened to you.

## The Anatomy of Systems

Every system, no matter how unique it thinks it is, eventually grows the same organs:

```python
# Every system's evolution:
# Day 1
def process_data(data):
    return transform(data)

# Month 1
def process_data(data, user):
    if not user.is_authenticated:
        raise AuthError("Who are you?")
    return transform(data)

# Year 1
class DataProcessor:
    def __init__(self, auth_service, cache, logger, db, queue, 
                 monitoring, feature_flags, rate_limiter):
        # Welcome to architecture
```

Like hermit crabs growing into bigger shells, systems accumulate architectural patterns:

- **Authentication**: "Who are you?"
- **Authorization**: "What can you do?"
- **Caching**: "Have I seen this before?"
- **Logging**: "What happened?"
- **Monitoring**: "Is everything on fire?"
- **Rate Limiting**: "Slow down there, cowboy"

## APIs: The Contracts Between Systems

APIs are how systems lie to each other professionally.

```python
# What the API promises
@app.route('/api/users/<id>')
def get_user(id):
    """Get a user by ID. Simple!"""
    return User.get(id).to_json()

# What actually happens
@app.route('/api/users/<id>')
@rate_limit
@cache(timeout=300)
@authenticate
@log_request
@handle_errors
@deprecation_warning("Use v2")
@measure_performance
@validate_input
def get_user(id):
    # Check if ID is valid
    # Check if user exists
    # Check if caller can see this user
    # Check cache
    # Hit database (primary or replica?)
    # Transform to API format
    # Strip sensitive fields
    # Add HATEOAS links that nobody uses
    # Set cache headers
    # Log everything
    # Increment metrics
    return eventually_return_something_resembling_a_user(id)
```

REST APIs pretend the world is made of resources. GraphQL pretends clients know what they want. SOAP pretends it's still 2003. They're all lies, but useful lies.

## Databases: Where State Goes to Live Forever

The database is the soul of your system. Everything else can be rebuilt, but lose the database and you lose everything.

```sql
-- Every database's life story
-- Year 1: Beautiful normalized schema
CREATE TABLE users (
    id INT PRIMARY KEY,
    email VARCHAR(255) UNIQUE,
    created_at TIMESTAMP
);

-- Year 2: Reality strikes
ALTER TABLE users ADD COLUMN deleted_at TIMESTAMP;  -- Soft deletes
ALTER TABLE users ADD COLUMN metadata JSON;         -- Junk drawer
ALTER TABLE users ADD COLUMN legacy_id VARCHAR;     -- Migration pain
ALTER TABLE users ADD COLUMN temp_flag BOOLEAN;     -- "Temporary"

-- Year 3: Performance hacks
CREATE INDEX idx_users_email_deleted ON users(email, deleted_at);
CREATE INDEX idx_users_created_at ON users(created_at);
CREATE INDEX idx_users_everything ON users(id, email, created_at, deleted_at);
-- 47 more indexes...

-- Year 5: Nobody remembers why this exists
CREATE TABLE users_backup_backup_final_v2_really_final;
```

Databases are where idealism goes to die. You start with beautiful third normal form. You end with denormalized caches of caches, JSON columns containing entire object graphs, and stored procedures that would make Lovecraft weep.

## Microservices: The Distributed Monolith

Microservices are what happens when you solve organizational problems with technology.

```yaml
# The dream
services:
  - user-service: "Handles users"
  - order-service: "Handles orders"  
  - payment-service: "Handles payments"

# The reality
services:
  - user-service: "Handles users, some orders, a bit of payments"
  - order-service: "Handles orders, needs users, triggers payments"
  - payment-service: "Handles payments, updates orders, notifies users"
  - auth-service: "Everyone needs this"
  - notification-service: "Everyone triggers this"
  - saga-coordinator: "Cleans up the mess when something fails"
  - service-discovery: "Where is everyone?"
  - api-gateway: "The bouncer"
  - circuit-breaker: "Stops cascading failures"
  - distributed-tracing: "What's taking so long?"
  - legacy-monolith: "Still handles 60% of traffic"
```

Microservices promise independence. Instead, you get distributed transactions, eventual consistency, and the joy of debugging across 17 different log systems.

The dirty secret: Most "microservices" are just a monolith with extra network calls.

## Message Queues: The Duct Tape of Distributed Systems

When in doubt, add a queue.

```python
# Synchronous: Simple but fragile
def handle_order(order):
    process_payment(order)      # What if this is slow?
    update_inventory(order)     # What if this fails?
    send_confirmation(order)    # What if email is down?

# Asynchronous: Complex but resilient
def handle_order(order):
    queue.publish('process-payment', order)
    queue.publish('update-inventory', order)
    queue.publish('send-confirmation', order)
    # Fire and forget! (And pray)
```

Queues are like email for programs. They turn "do this now" into "do this whenever you get around to it." They also turn "this failed" into "this failed but we'll try again later maybe."

Every queue starts simple and ends up implementing:
- Retry logic (with exponential backoff)
- Dead letter queues (where messages go to die)
- Priority queues (some messages are more equal than others)
- Deduplication (because at-least-once delivery means at-least-twice)

## The CAP Theorem: Pick Two, Cry About the Third

Consistency, Availability, Partition Tolerance. Pick two. This is the universe laughing at your distributed system dreams.

- **CP Systems**: "We'd rather die than be wrong" (Banks)
- **AP Systems**: "We'd rather be wrong than be down" (Social media)
- **CA Systems**: "We live in a fantasy where networks never fail" (Your dev environment)

Real systems pick different trades at different times:
```python
if request.is_money_related():
    return consistency_over_everything()
elif request.is_user_facing():
    return available_but_maybe_stale()
else:
    return whatever_is_cheapest()
```

## Architecture Patterns: The Same Story, Different Costumes

**Monolith**: Everything in one place. Like a studio apartment.
```
┌─────────────────┐
│   Everything    │
│   In One Place  │
│   (Send Help)   │
└─────────────────┘
```

**N-Tier**: Layers upon layers. Like a wedding cake.
```
┌─────────────────┐
│   Presentation  │
├─────────────────┤
│    Business     │
├─────────────────┤
│      Data       │
└─────────────────┘
```

**Microservices**: Everything everywhere. Like a city.
```
┌────┐ ┌────┐ ┌────┐
│ A  │ │ B  │ │ C  │
└──┬─┘ └─┬──┘ └──┬─┘
   │ ┌───┴───┐   │
   └─┤   D   ├───┘
     └───────┘
```

**Serverless**: Someone else's computer. Like Airbnb for code.
```
λ → λ → λ → λ → λ
(Functions all the way down)
```

## The Reality of Architecture

Here's the thing: Architecture isn't designed. It's discovered. You don't sit down and architect a system. You evolve toward an architecture, fighting entropy every step of the way.

Every architectural decision is a trade-off:
- Monoliths are simple until they're not
- Microservices are scalable until they're not
- Databases are fast until they're not
- Caches are helpful until they're not

The best architecture is the one that lets you change your mind later. The worst architecture is the one that requires you to be right the first time.

Systems are like cities. They start as villages, grow into towns, sprawl into metropolises. They develop neighborhoods (services), highways (APIs), slums (legacy code), and downtown districts (core business logic). They have rush hours (peak traffic) and quiet nights (maintenance windows).

And like cities, the best systems aren't the ones that were perfectly planned. They're the ones that adapted, evolved, and somehow kept serving their citizens despite growing far beyond what anyone imagined.

The real mystery isn't how to build perfect architectures. It's that our imperfect architectures work at all. Every system is held together by load balancers and prayers, caches and hopes, queues and dreams. Yet somehow, they serve billions of requests, store petabytes of data, and keep the digital world turning.

We're not architects. We're digital archaeologists, constantly discovering the civilizations we're building as we build them.

---

*Next up: L5 - Complex Systems, where we'll explore distributed systems that nobody fully understands, why "the cloud" is just other people's computers having the same problems, and how DevOps is basically group therapy for systems...*