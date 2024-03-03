# VE280 2024SP RC2

## Review of C++ Basics

### Basic Concepts

**Common data types**: `int`, `double`, `char`, `bool`, `string`.

**Input and output streams**: `cin`, `cout`.

**Basic operators**:

- Arithmetic operators: `+`, `-`, `*`, `/`, `%`.
- Comparison operators: `==`, `!=`, `>`, `<`, `>=`, `<=`.
- Logical operators: `&&`, `||`.
- Stream operators: `<<`, `>>`.
- Assignment operators: `=`, `+=`, `-=`, `*=`, `/=`, `%=`.
- Increment and decrement operators: `++`, `--`.

**Control flow**:

- `if`-`else` / `switch`-`case` statements.
- `while` / `for` loops.

### Range-based `for` loop (Won't be covered in exams)

Range-based `for` loop is a feature added in C++11 to iterate over containers. It provides a simpler and more readable way to iterate over elements of an array, vector, list, or any other container that supports the concept of iterators, namely the `begin()` and `end()` functions. The following is an example:

```cpp
std::vector<int> numbers = {1, 2, 3, 4, 5};
for(int num : numbers) { // Iterating over a STL container
}
int arr[] = {1, 2, 3, 4, 5};
for(int num : arr) { // Iterating over an array
}
```

### lvalue and rvalue

**lvalue**: an expression that may appear on the left-hand side or right-hand side of an assignment.
**rvalue**: an expression that may **only** appear on the right-hand side of an assignment.

Examples:

```cpp
int a = 114514; // a is an lvalue, 1 is an rvalue
int b = a; // b is an lvalue, a is an lvalue
const int c = a + b; // c is an rvalue, a + b is an rvalue
int *p = &a; // p is an lvalue, &a is an rvalue
```

In brief, any non-const variable is an lvalue, and any constant or expression is an rvalue.

### Function Declaration and Definition

**Declaration**:

```cpp
// return_type function_name(parameter_list);
int add(int a, int b);
void print(string s);
```

Note that this should come before the function is called.

**Definition**:

```cpp
// return_type function_name(parameter_list) {
//     function_body;
// }
int add(int a, int b) {
    return a + b;
}

void print(string s) {
    cout << s << endl;
}
```

Note that this can come before or after the function is called.

### Pointers, References, and Arrays

**Pointers**: a variable that stores the address of another variable. Changing the value of a pointer will change the value of the variable it points to.

```cpp
int a = 114514;
int *p = &a; // p is a pointer to a, &a is the address of a
cout << *p << endl; // *p is the value of a
*p = 1919810; // a is now 1919810
```

- `*` is the dereference operator, which returns the value of the variable that the pointer points to.
- `&` is the address-of operator, which returns the address of a variable.

**References**: an alias of a variable. Changing the value of a reference will change the value of the variable it refers to.

```cpp
int a = 114514;
int &r = a; // & is the reference operator, r is a reference to a
r = 1919810; // a is now 1919810
```

- A reference must be initialized when it is declared.
- After initialization, a reference cannot be changed to refer to another variable.

A small exercise:

```cpp
int x = 0;
int &r = x;
int y = 1;
r = y;
r = 2; // What is the value of x, y, and r?
```

```cpp
int x = 0;
int *p = &x;
int y = 1;
p = &y;
*p = 2; // What is the value of x, y, and *p?
```

**Arrays**: a collection of variables of the same type. The size of an array must be known at compile time. You can access the elements of an array using `[]` operator or by pointers.

```cpp
int a[5] = {1, 2, 3, 4, 5}; // a is an array of 5 integers
cout << a == &a[0] << endl; // true
cout << a[0] << endl; // 1
```

Arrays work well with pointers.

### Function Call Mechanism

When a function is called, the parameters are passed to the function. There are two ways to pass parameters:

- **Pass by value**: the value of the parameter is copied to the function. Modifying the parameter inside the function will not affect the original variable.
- **Pass by reference**: the address of the parameter is passed to the function. Modifying the parameter inside the function will affect the original variable.

A small exercise:

```cpp
void f(int x, int &y, int *z) {
    x = 1; // passed by value
    y = 1; // passed by reference
    *z = 1; // passed by reference
}

int main() {
    int a = 0;
    int b = 0;
    int c = 0;
    f(a, b, &c);
    // What are the values of a, b, and c?
    cout << a << endl;
    cout << b << endl;
    cout << c << endl;
}
```

In C++, arrays are passed by reference.

```cpp
void f(int a[]) {
    a[0] = 1; // passed by reference, the value of a[0] is changed
}
```

Advantage of pass by reference with **pointers**:

- You can directly change the value of the variable that the pointer points to. This avoid copying instances of large objects sometimes.

Advantage of pass by reference with **references**:

- More readable and intuitive than pointers.

### Structs

Structs are user-defined data types that can contain multiple variables of different types. The members of a struct can be common data types or other structs.

```cpp
struct Student {
    string name;
    int id;
    double gpa;
}; // don't forget the semicolon here
```

To declare a struct variable and access its members:

```cpp
Student s1; // s1 is a struct variable
s1.name = "Alice";
s1.id = 114514;
s1.gpa = 4.0;
Student s2 = {"Bob", 1919810, 3.9}; // another way to initialize
Student s3 = &s1; // s3 is a pointer to s1
s3->name = "Bob"; // access the members of struct pointer using ->
```

## Const Qualifiers

Const qualifiers are used to specify a variable that cannot be modified. There are two ways to use const qualifiers:

- Data Variables
- Function Parameters
- Pointers
- References
- Class member functions (This will be covered after midterm)

### Const Data Variables

Basic syntax:

```cpp
const data_type variable_name = value;
```

Properties:

- The value of a const variable cannot be changed after initialization.

```cpp
const int MAX_SIZE = 100;
MAX_SIZE = 200; // Error
```

- A const variable must be initialized when it is declared.

```cpp
const int MAX_SIZE; // Error
```

This practice greatly improves the readability of your code. It also prevents you from accidentally modifying the value of a variable.

Also, if you want to modify the size of an array, just modify the value of `MAX_SIZE` and recompile your code. You don't need to modify the size of every array in your code.

```cpp
const int MAX_SIZE = 100; // Modifying this line enables you to resize all arrays
int a[100] // Feasible, but not recommended
int a[MAX_SIZE] // Feasible, recommended
int b[MAX_SIZE]
```

### Const References

Basic syntax:

```cpp
const data_type &reference_name = variable_name;
const int &r = a;
```

Advantages:

- **Cannot be modified**.
  Recall that the parameter can be passed to functions by reference to avoid copying large objects. However, if you don't want the function to modify the parameter, you can pass it by const reference.

```cpp
Student s1 = {"Alice", 12345, 1.0};
// Recall the struct Student
void f(const Student &s) {
    s.name = "Alice";
    s.gpa = 4.0;
    cout << s.gpa << endl; // 4.0
}
```

- **Can be initialized by rvalues**.
  Recall that a reference must be initialized when it is declared. However, a const reference can be initialized by rvalues.

```cpp
const int &cref = 1; // OK
int &ref = 1; // Error
```

For function parameters, it is recommended to pass by const reference if the parameter is not modified inside the function. The type compatibility is as follows:

- `const type &` to `type &` is not allowed.
- `type &` to `const type &` is allowed.
- `const type *` to `type *` is not allowed.
- `type *` to `const type *` is allowed.

A small exercise:

```cpp
void const_reference_test(const int &r) {}
void reference_test(int &r) {}
void pointer_test(int *p) {}
int main() {
    int a = 0;
    const int b = 0;
    int *p = &a;
    const int *cp = &a;

    // Which of the following function calls are valid?
    const_reference_test(a);
    const_reference_test(b);
    const_reference_test(*p);
    const_reference_test(*cp);
    reference_test(a);
    reference_test(b);
    reference_test(*p);
    reference_test(*cp);
    pointer_test(p);
    pointer_test(cp);
}
```

### Const Pointers

The rule for `const`: `const` applies to the thing on its left. If there is nothing on its left, it applies to the thing on its right.

For const pointers, there are two cases:

- Pointer to `const`: Here the pointer can point to arbitrary variables, but the value of the variable cannot be modified.
- `const` pointer: Here the pointer can only point to one variable, but the value of the variable can be modified.

The two cases can be combined.

```cpp
const int* a                 // a pointer to a constant integer
int const * a                // a pointer to a constant integer
int* const a                 // a constant pointer to an integer
const int* const a           // a constant pointer to a constant integer
int const * const a          // a constant pointer to a constant integer
```

These declarations are all valid.

### typedef

`typedef` is used to create an alias for a data type. It is often used to simplify the declaration of complex data types. The motivation is just like using reference variables.

```cpp
typedef int* int_ptr;
// int_ptr is an alias for int*
typedef const int_ptr const_int_ptr;
// the defined alias can be used in other typedef
typedef const int* const_int_ptr;
// All in one line
```

## Procedure Abstraction

### Abstraction

Abstraction is a process of emphasizing the separation of "what" and "how". It helps programmers to use a function without knowing how it is implemented.

It only provides the details that are relevant to the user, and hide the unnecessary details.

```cpp
// In the header file, the function is declared
int add(int a, int b);

// In the cpp file, the function is defined/implemented
int add(int a, int b) {
    return a + b;
}
```

### Motivation

There're usually two roles in programming: the implementer and the user. The implementer is responsible for implementing the function, and the user is responsible for using the function. For the user, the implementation details are not important. They only need to know the interface of the function.

A simple example is that you don't need to know how `std::cout` works. You only need to know it prints things to the console.

### Benefits

- **Simplifies Project**: Helps manage complex project by focusing on the big picture instead of the detailed implementation.
- **Enhances Readability**: Hides the implementation details, making the code more readable and understandable.
- **Facilitates Maintenance**: Encapsulates code for easy maintenance and modification.

### Properties of a Good Abstraction

- **Local**: The implementation of an abstraction is independent of any other abstraction implementation.

```cpp
// Here the user doesn't need to know how multiply is implemented
int square(int a) {
    return multiply(a, a);
}
```

- **Substitutable**: The implementation of an abstraction can be replaced by another implementation as long as the interface is the same and the implementation is correct.

```cpp
// Here the implementation of multiply can be replaced by another implementation
// as long as the abstraction is the same and the implementation is correct
int multiply(int a, int b) {
    return a * b;
    // return b * a; // This is also correct
}
```

### Type Signature

The type signature of a function is the function's name, the number of parameters, and the type of each parameter. It is used to declare the function.

```cpp
int add(int a, int b);
```

### Specification Comments

Besides the type signature, a function should also have specification comments. There're usually three types of comments:

- **REQUIRES**: Preconditions that must hold, if any.
- **MODIFIES**: Variables that are modified, if any.
- **EFFECTS**: What the procedure does given legal inputs.

```cpp
int positiveAdd(int a, int b);
// REQUIRES: a > 0, b > 0
// MODIFIES: None
// EFFECTS: Returns the sum of a and b
```

Note that functions with no **REQUIRES** clause is complete, while functions with them are partial.

The convention of abstraction is really important in large projects. In this course, using abstraction to simplify the projects can make your life much easier.

## References

[1] Zhanxun Liu. VE280 RC3. 2023FA.

[2] Weikang Qian. VE280 Lecture 4-6. 2023FA.

[3] Zhongqiang Ren. VE280 Lecture 4-6. 2024SP.
