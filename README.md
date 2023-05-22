# IDEA Module Compilation Bug

Demonstrate a bug with how IDEA compiles modules.

Dependency hierarchy is as follows:

```
    A     B
     \   /|
       C  |
       |  |
   important
```

Attempting to compile the project through IDEA generates the following error:

```
.../important-module/src/com/example/important/Main.java:9:21
java: cannot access com.example.a.MyClass
  class file for com.example.a.MyClass not found
```

This shouldn't happen because `Main.java` does not import `a.MyClass`.
It should be provided transitively by `c.AwesomeClass`.

Crucially, module `c` should not need to `export` these modules.