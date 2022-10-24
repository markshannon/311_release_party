
<br><br><br>
<br><br><br>
<br><br><br>
<br><br><br>
<br><br><br>

# Contiguous Frame Stack

<br><br><br>
<br><br><br>
<br><br><br>
<br><br><br>
<br><br><br>
<br><br><br>

---

# Python frames

Running code in any language (except old versions of Fortran) needs a stack.

```Python
def foo(x):
    return bar() + x
```

The value of `x` needs to be stored somewhere while calling `bar`, and since it is
possible that `bar` with call `foo`, we need a stack.



![Frame object](./frame_object.gv.png)



# The Python frame stack

As code executes, these frames form a stack. Up to Python 3.10, this stack
was implemented as a linked list, meaning that each function call needed a 
separate piece of heap allocated memory.

## Python 3.10

![Frame stack](./frame_stack.gv.png)

## Python 3.11

### Before Call

![Before call](./frames_example_before.gv.png)

### After Call

![After call](./frames_example_after.gv.png)


# Handling generators, tracebacks and introspection.

## With a generator in the stack

![With generator](./frames_with_generator.gv.png)


# Creating a frame object

## Before

![Before call](./frames_example_before.gv.png)

## After Creating a frame object

![With frame object](./frames_with_object.gv.png)

## After returning

![Frame after return](./frames_with_object_after_return.gv.png)

