
<br><br><br>
<br><br><br>
<br><br><br>
<br><br><br>
<br><br><br>

# Zero Cost Exceptions

<br><br><br>
<br><br><br>
<br><br><br>
<br><br><br>
<br><br><br>
<br><br><br>

---

# "Zero Cost"

"Zero cost" doesn't mean that it has no cost, unfortunately.

* If an Exception is **not** raised, the cost of the `try-except` or `try-finally`
is negligible.
* If an Exception is raised, "zero cost" exception handling is actually more expensive.
* Overall, the cost is reduced considerably.

<br><br><br>
<br><br><br>
<br><br><br>

---

# Example Code

```Python 
def f():
    try:
        g(0)
    except:
        return "fail"
```

<br><br><br>
<br><br><br>

```Python 
def frame_size():
   return sys.getsizeof(sys._getframe())
```

<br><br><br>
<br><br><br>
<br><br><br>
<br><br><br>

---

## Bytecode 

The function `f` compiles to:

### 3.10 

```
start:
  SETUP_FINALLY     except   # Pushes (type, level, handler)
  LOAD_GLOBAL       g
  LOAD_CONST        0
  CALL_FUNCTION     1
  POP_TOP
end:
  POP_BLOCK                  # Pops top of block stack.
  LOAD_CONST        None
  RETURN_VALUE

except:
  POP_TOP
  POP_TOP
  POP_TOP
  POP_EXCEPT
  LOAD_CONST        'fail'
  RETURN_VALUE
```


### 3.11

```
start:
  LOAD_GLOBAL       g
  LOAD_CONST        0
  CALL              1
  POP_TOP
end:
  LOAD_CONST        None
  RETURN_VALUE

except:
  PUSH_EXC_INFO
  POP_TOP
  POP_EXCEPT
  LOAD_CONST        'fail'
  RETURN_VALUE

ExceptionTable:
  start to end -> except
```

## Frame Size

Up to Python 3.10, the exception handling stack took up 240 bytes per frame object.
### 3.10 

```Python
>>> frame_size()
400
```

### 3.11

```Python
>>> frame_size()
168
```

