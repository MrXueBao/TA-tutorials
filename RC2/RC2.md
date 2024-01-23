# VE280 2024SP RC2

## Review of C++ Basics

### Basic Concepts

Common data types: `int`, `double`, `char`, `bool`, `string`.

Input and output streams: `cin`, `cout`.

Basic operators:

- Arithmetic operators: `+`, `-`, `*`, `/`, `%`.
- Comparison operators: `==`, `!=`, `>`, `<`, `>=`, `<=`.
- Logical operators: `&&`, `||`.
- Stream operators: `<<`, `>>`.
- Assignment operators: `=`, `+=`, `-=`, `*=`, `/=`, `%=`.
- Increment and decrement operators: `++`, `--`.

Control flow:

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

lvalue: an expression that may appear on the left-hand side or right-hand side of an assignment.
rvalue: an expression that may **only** appear on the right-hand side of an assignment.

Examples:

```cpp
int a = 114514; // a is an lvalue, 1 is an rvalue
int b = a; // b is an lvalue, a is an lvalue
const int c = a + b; // c is an rvalue, a + b is an rvalue
int *p = &a; // p is an lvalue, &a is an rvalue
```

In brief, any non-const variable is an lvalue, and any constant or expression is an rvalue.

### Function Declaration and Definition

Declaration:

```cpp
// return_type function_name(parameter_list);
int add(int a, int b);
void print(string s);
```

Note that this should come before the function is called.

Definition:

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

Try to find the final value of all variables:

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
    cout << a << endl; // 0
    cout << b << endl; // 1
    cout << c << endl; // 1
}
```

In C++, arrays are passed by reference.

```cpp
void f(int a[]) {
    a[0] = 1; // passed by reference, the value of a[0] is changed
}
```

Advantage of pass by reference with pointers:

- You can directly change the value of the variable that the pointer points to. This avoid copying instances of large objects sometimes.

Advantage of pass by reference with references:

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
