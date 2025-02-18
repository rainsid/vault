# Ownership
- is a set of rules that govern how a Rust program manages memory

## Ownership Rules
- each value in Rust has an *owner*
- there can only be one owner at a time
- when the owner goes out of scope, the value will be dropped

## Variable Scope
- a scope is a range within a program for which an item is valid
``` rust
    {                      // s is not valid here, it’s not yet declared
        let s = "hello";   // s is valid from this point forward

        // do stuff with s
    }                      // this scope is now over, and s is no longer valid
```
