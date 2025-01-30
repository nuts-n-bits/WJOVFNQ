A2: 

Implementation: 
    - I simply translated the natural language description in langauge.pdf into the antlr4 grammar in MiniC.g4
    - To resolve the issue of `if (...) a; b; else c;`, I disallowed `stmt` to recursively include itself, and explicitly used `stmt+` where they are called for (inside `scope`s).

Testing: 
    - I ran `grun MiniC prog -gui` and typed some sample C program, then visually inspected the resulting tree.
    - I also ran the autotester.
    - An invalid version is used to test the edge case: `if (...) a; b; else c;`
    - Sample looks like this: 

```
int a, b;

// wrong case
void main() {
    for (a; b; c) {
        a; b; c;
    }
    if (true)
        a; 
        b;
    else 
        c;
}

// correct case
void main() {
    for (a; b; c) {
        a; b; c;
    }
    if (true)
        a; 
    else 
        c;
}

// correct case 2
void main() {
    if (a)
    while (b)
    for (;;)
    return c;    
}

```