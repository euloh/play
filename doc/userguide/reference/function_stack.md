
# stack

Records a stack trace to the buffer.
Alternatively, returns a `dt_stack_t` value that can be stored in a variable.

```
dt_stack_t stack([uint32_t *frames*])
```

The `stack` function records a kernel stack trace to the directed buffer.
The function includes an option to specify the number of frames deep to record from the kernel stack.
If no value is specified, the number of stack frames recorded is the number that's specified by the `stackframes` runtime option.
The `dtrace` command reports frames, either up to the root frame or until the specified limit has been reached, whichever comes first.

The `stack` function can also be used as the key to an aggregation.

Or, its value may be used as a value to a variable.

## How to use stack to obtain a kernel stack trace for a particular probe

In this example, `stack()` is an action that prints the kernel stack.

```
fbt::ksys_write:entry
{
        stack();
        exit(0);
}

```

Alternatively, here `stack()` is used to assign to a variable and print later using `%k` conversion.

```
        v = stack(3);
        printf("%k", v);
```

**Parent topic:**[DTrace Function Reference](../reference/dtrace_functions.md)

