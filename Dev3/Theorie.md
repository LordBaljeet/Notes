[TOCM]

# Test 252

# 1. Important code
1. To create an Object file: `g++ -Wall -std=c++20 -pedantic-errors -c 001_empty.cpp`


   &rarr; `-Wall` for all warnings.

   &rarr; `-std=c++20` to specify the program c++ version.

   &rarr; `-pedantic-errors` to show errors.

2. To create the executable : `g++ -o 001_empty.exe 001_empty.o`

# 2. Start coding
## 2.1. main file :
The main file has a return type of `int` and is called `main()` with no arguments.
### 2.1.1. example :
```
#include <iostream>

int main() {
    std::cout << "Hello World!" << std::endl;
    return 0;
}
```

&rarr; `#include <iostream>` to use the system input and output ports. Without it, you can't print nor read to the console.

&rarr; `std::cout` to use `cout` method of the `std` namespace. It allows for a print to the console.

&rarr; `std::endl` to use `endl` method of the `std` namespace. It ends the line and flushes the output.

&rarr; The method returns `0` to indicate that all went good (*the return can be created by the compiler so you don't really need to write it*).

Note: we can write `using namespace std;` before the `main()` method. That allows as to just write `cout` and `endl` instead of `std::cout` and `std::endl`.

## 2.2. &#9888; Important!
C++ is a very dumb programming language. It only reads your code once, from top to bottom.

That can lead to your program not working if you use call a function that has been written below the call.

example:

    #include <iostream>

    int main()
    {
        show(42);
    }

    void show(int i)
    {
        std::cout << "in show : " << i;
    }

**Note:** This code will not be executed.

# 3. Operators:

## 3.1. `<<` Operator:

`<<` is the ***insertion operator***.It works the same as a concatenation operator. It concatenates whatever it is on its right to whatever it is on its left.

example of use :

    std::cout << "Hello " << "World" << "!" << std::endl;

 This would print `Hello World!` to the console.

## 3.2. `::` Operator:

`::` is the ***scope resolution operator***. It is the same as the `.` operator in java. `std::cout` is the same as `std.cout`.


# 4. C++ file types:

C++ uses `.h` and `.cpp` file types.

## 4.1. Header files:

`.h` indicates a `header` file. Those files are like `abstract` classes in java. They only contain the `signature` of a methode.

example of fct.h file:

    void show(int i);

The header files usually have the same name as their source files, so there is no `#include<filename>` needed as the `Linker` would link both files together.

## 4.2. Source files:

`.cpp` indicates a `source` file. Those files contain the implementation of one or multiple methods.

example of fct.cpp file:

    #include <iostream>

    void show(int i){
        std::cout << "Hello " << i << std::endl;
    }

As the file name is the same as its header file. The `Linker` can link the method signature with its implementation.

example of use for `show(int i)` method:

    #include "fct.h"

    int main() {
        show(42);
    }

You can use a method that has been implemented in a different file by including its header.
In this case, we used the method `show()` by writing down `#include "fct.h"` before calling it.

# 5. Arithmetic Types:

In C++, there are 5 different arithmetic types:

&rarr; char.

&rarr; short (int).

&rarr; int.

&rarr; long (int).

&rarr; long long (int).

They rank in size as follow:

char <= short <= int <= long <= long long

Some of them are also int, like long int. They can also be either `signed`(+ and/or -) or `unsigned` (only +). 

There is also double and float types. They are basically a branch of long.

## 5.1. Conversion:

You can convert certain types to others using the `static_cast<>()`. You simply put the type to convert to between `< >`.

# 6. Error Types:

## 6.1. Linker Errors:

As said above, C++ is dumb. It can only read from top to bottom once. You can only call a method if it was implemented above or include the header file.

A linker error occur when the linker didn't find the declaration of the called method. Either because it was not declared, or was declared after it was called.

example 1:

    #include <iostream>

    int main()
    {
        show(42);
    }

    void show(int i)
    {
        std::cout << "in show : " << i;
    }

This code will generate a Linker error because the linker did not find the declaration oh the methode `show()` when it read its call.

example 2:

    #include <iostream>

    int main()
    {
        count_till(100);
    }

This code will also generate a Linker error.

## 6.2. Compiler Errors:

Compiler errors come after linker's errors. They occur when the called method has been declared before, but there is a problem in its body, whether the body does not exist, 

or it is not a working body. They can also occur in case of bad conversion, bad call of a method (too much/few arguments, wrong argument type, etc..) or even syntax errors.

example 1:

    #include <iostream>

    void show(int i);

    int main()
    {
        show(42);
    }

In this case, the code will generate a Compiler error because the method `show()` has no body.

example 2:

    #include <iostream>

    int show(int i) {
        i++;
        return true;
    };

    int main()
    {
        show(42);
    }

This code will also generate a Compiler error because the method `show()` has wrong return value.

# 7. Polymorphism:

In case of multiple different methods having the same name, the compiler would choose which one to use following this order:

1. Exact correspondence
2. Templates
3. Numeric promotion
   1. char, signed char, unsigned char, short, unsigned short, bool &rarr; int.
   2. float &rarr; double.
4. Standart conversion
5. Conversions defined by user.

&#9888;Â Sometimes, 2 methods are viable to call for the given argument.In this case, a Compiler error would occur because the compiler can't decide which one to choose.

example :

    #include <iostream>

    using namespace std;

    void f(char)
    {
        cout << "f(char)" << endl;
    }

    void f(int)
    {
        cout << "f(int)" << endl;
    }

    int main()
    {
        f(400L);
    }

In this example, a `long int` can either be converted to `int` or `char` equally. The compiler can't decide and thus would generate an error.

# 8. Default Arguments:

You can set default values to a method's arguments using `=` operator:

example 1:

    void position(int x, int y=10)
    {
        std::cout << "x: " << x << '\n';
        std::cout << "y: " << y << '\n';
    }

In this case, if the user didn't provide a value for `y` argument, it is defaulted to 10. The user must still give a value for `x` as it has no default value.

example 2:

    void position3d(int x=10, int y=10, int z=10 )
    {
        std::cout << "x: " << x << '\n';
        std::cout << "y: " << y << '\n';
        std::cout << "z: " << z << '\n';
    }

In this case, if the user didn't provide any values as arguments, they are all defaulted to 10. The user can call the method with no arguments and it will run fine.

&#9888;Â Important

The following code will generate a Compiler error :

    void position(int x=10, int y)
    {
        std::cout << "x: " << x << '\n';
        std::cout << "y: " << y << '\n';
    }

You can default either all of the arguments, or all except the first one.

# 9. References:

In C++, there is the `&` operator. When used in a variable declaration, it makes that variable a reference to another variable.

example:

    int i = 10;

    int &ri {i};

In this case, `ri` is a reference to `i`, and thus, modifying `ri` would also modify `i`.

&#9888;Â Important

Just like constants, a reference variable must be instantiated, otherwise it will generate a Compiler error.

    int &ri; // error!

References can also be constants, in which case, they cannot be modified and thus cannot modify the referenced variable.

# 10. Type Inference:

## 10.1. auto:
 `auto` can be used if you assign a variable `a` to a variable `b`, but dont know `b`'s type.

example:

    double b = 12.3;
    auto a = b;

You can also use it if you assign a variable `a` to the return value of a function.

example:

    int doubleIt() {
        return 2;
    }

    auto a = doubleIt();

In this example, the return value of the method would be calculated and its type would be the type of `a`;

&#9888;Â Important

The following example would generate a Compiler error. A variable of type `auto` must be assigned to a value;

    auto a;

## 10.2. decltype:

`decltype` is used for the same reasons as `auto`.

example:

    double b = 12.3;
    decltype(b) a;

However, there are some differences between the 2.

1. `decltype` must not be assigned to a value when declared, just like the example above.
2. It does not calculate the the method's return value, but only the type of return of the method.

# 11. Pointers:

Pointers works the same as [references](#9. References:). When you modify a pointer, you also modify the value of the variable that's pointed to by the pointer.

    int b = 23;
    int * a = b;

`a` points towards the adress of `b`.

    int b = 23; // adress = 100
    int * a = b; // a points towards the adress of b => 100
    cout << a; // prints the adress pointed by a => 100, not its value.
    cout << *a; // prints the value of the adress pointed by a => 23.

&#9888;Â Important

The following wont work as a reference doesn't have nor points towards an adress, and pointers needs adress to point towards.

    int a = 23;
    int &b = a;
    int *c = b; // COMPILER_ERROR

**Note:** You can have a pointer of pointer, as follow:

    int a = 23;
    int *b = a;
    int **c = b;

    **c = 10; // => b = 10 => a = 10

&#9888; Important

    int a = 23; // adress = 100;
    int *b = a;
    int **c = b;

    cout <<c; adress of *b = 100;
    c = 10; // changes the adress pointed by c to 10.VERY BAD!

    cout << *c; // adress of b.
    *c = 10; // changes the adress pointed by b to 10.VERY BAD!

    cout << **c; // value of the adress pointed by b => a;
    **c = 10; // changes the value of the adress pointed by b => changes a.