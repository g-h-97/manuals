

# Data Types

## Int

The `int` data type is integer of 32bit aka 8B in x86.

## Float

Floating point number

## Char

A character

## Double

64bit Float

## Static

The `static` data type is able to exist on multiple scopes, meaning it does not get garbaged if the scope it's declared in exits.Basically it exists for the entire program's life time. It's value is initialized before the program starts if not explicitly done.

## Const

The `const` data type is constant no matter what, so it's value can never change.

## Struct

A `struct` data type is a user defined type that contains other data types or other structs. It can be defined

```c
struct mystruct {
    int number=0;
    double value;
    char string;
}
```

The variable of type `struct mystruct` can be declared like so

```c
struct mystruct mystruct_var;
```

## Typedef

Allow to create an alias for a data type, for example for a `struct`

```c
typedef struct mystruct {
    int number=0;
    double value;
    char string;
}
```

Which will make defining a new variable like this, where the `struct` key work is omitted

```c
mystruct mystruct_var;
```


## class

They are a user defined data types


# C Program Memory Layout

The size of each segment can be seen using the `size` command on a binary.

```
__________________
|                |
|     Stack      |
|________________|
|       ▼        |
|                |
|                |
|                |
|       ▲        |
|________________|
|      Heap      |
|________________|
|  Uninitialized |
|      Data      |
|     (BSS)      |
|________________|
|   Initialized  |
|      Data      |
|________________|
|      Text      |
|________________|
```

## Stack

The stack is a LIFO^[Last In First Out] structure

## Heap

The heap is

## Uninitialized Data (BSS)

The BSS^[Block Started by Symbol] segment contains variable that are initialized to arithmetic `0` by the kernel when the program starts running.

## Initialized Data

The `Data Segment` contains the variables that were initialized explicitly by the program, it can divided into two part `Read Only` & `Read Write`
