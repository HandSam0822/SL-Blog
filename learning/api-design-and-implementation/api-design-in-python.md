# API Design in Python

### Flexible function definitions

* Can return multiple values (i.e., a tuple)&#x20;
* Positional and named arguments

```python
def f(x, y): 
    return 10*x + y 

f(3, 1) # 31 
f(y=3, x=1) # 13
```

* Can unpack arguments to a function&#x20;

```python
p = (3, 1) 
f(*p) # 31 

# when input has many fields, unpacking provides greater readibility
d = {'x’: 1, 'y’: 3} 
f(**d) # 13
```

* Keyword arguments

```python
def f(**kwargs):
    x = kwargs['x']
    y = kwargs['y']
    return 10*x + y
```

### Generator functions

Produce an iterator by yielding a result, continue where you left off when **next** called again

```python
def fast_range(start, stop):
    if stop < start:
        m = f'start must be <= stop (start={start}, stop={stop})'
        raise ValueError(m)
    while start < stop:
        result = start
        start += 1
        yield result

# numbers is the head of iterator
numbers = fast_range(0, 100)
for val in numbers:
    print(val)
```

### Decorator

Decorators are callable objects that wrap the execution of a function

```python
def do_twice(func):
    def wrapper_do_twice():
        func()
        func()
    return wrapper_do_twice

@do_twice
def say_hello():
    print("Hello")

# Every time say_hello is called, it would be passed to do_twice function
# common use case is for validation before execution (login required...)
say_hello()
>> Hello
>> Hello

```

Reference: [https://realpython.com/primer-on-python-decorators/](https://realpython.com/primer-on-python-decorators/)

### Python Good Practice&#x20;

#### Default arguments must be immutable&#x20;

<pre class="language-python"><code class="lang-python"># [X] Never use a mutable default value, it won't work as expected:
<strong>def append_to_values(x, values=[]): 
</strong>    values.append(x) 
    return values 
        
list1 = append_to_values(10) 
list2 = append_to_values(42) 
print(list1) # expected: [10], Output: [10, 42] 
print(list2) # expected: [42], Output: [10, 42]


# [O] Use None and document the actual default if a mutable value is needed
def append_to_values(x, values = None):
    if not values:
        return [x]
    values.append(x)
    return values

</code></pre>

#### Prevent name argument

Named args cannot be renamed in the future!

<pre class="language-python"><code class="lang-python"># Cannot rename arguments to numerator, denominator 
def fraction(a, b): 
    return a / b 
<strong>fraction(b=3, a=1) # 1/3
</strong>
# With / in function definition, we can prevent arguments being used as named arguments 
def fraction(a, b, /): 
 return a / b 
fraction(b=3, a=1) # TypeError 


</code></pre>

#### Force boolean argument to be named

Without a named argument, the meaning of a Boolean argument is often unclear.

For example, what does `get_temperature(False)` mean?

In Python 3, there is a simple way to enforce it! By adding a `*` in the function arguments, we force all _succeeding_ arguments to be named. E.g. by having the first argument be `*`, we force all arguments to be named.

```python
def safe_division(*, number, divisor, ignore_overflow, ignore_zero_division):

>>> safe_division(1, 2, True, False)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: safe_division() takes 0 positional arguments but 4 were given



>>> safe_division(number=10**1000, divisor=3**-100,
ignore_overflow=True, ignore_zero_division=False)
0
```

Another example

```python
# With * in function definition, we can force arguments to be used as named arguments 
def get_temperature(*, celsius=False):

get_temperature() # works fine
get_temperature(celsius=True) # is clear
get_temperature(True) # TypeError

```

