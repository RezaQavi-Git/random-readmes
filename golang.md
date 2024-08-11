# Golang

## Difference between make() and new()
`new()`: allocates memory for a new zeroed value of a specified type and returns a pointer to it. It is primarily used for initializing and obtaining a pointer to a newly allocated zeroed value of a given type, usually for data types like structs.
- When dealing with value types like structs, you can use new() to allocate memory for a new zeroed value. This is suitable for scenarios where you want a pointer to an initialized structure.

`make()`: is used for initializing slices, maps, and channels – data structures that require runtime initialization. Unlike new(), make() returns an initialized (non-zeroed) value of a specified type.
- For slices, maps, and channels, where initialization involves setting up data structures and internal pointers, use make() to create an initialized instance.

Keep in mind that new() returns a pointer, while make() returns a non-zeroed value. 


reference: [freecodecamp](https://www.freecodecamp.org/news/new-vs-make-functions-in-go/)