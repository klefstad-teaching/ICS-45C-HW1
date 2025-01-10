# ICS 45C Homework 1

Unit conversion, character stack, & letter count
Refresh your browser tab frequently to see any updates or changes (highlighted)

## Getting the assignment

1. Accept the assignment by click the link in canvas
2. Once you accept the invite you will reach a page that says "You're ready to go"
3. Clik the url from that page that looks similar to this: `https://github.com/klefstad-teaching/ics-45c-hw1-<GitHubUsername>`, it may take a bit of time for the repo to be ready.
4. There will be a green `<> Code` Button on the top right, click that and then click the middle tab `SSH`
5. Copy that link
6. Go to your hub and go into the ICS45C folder, and open up the terminal and type in the following command:
```bash
git clone git@github.com:klefstad-teaching/ics-45c-hw1-<GitHubUserName>.git HW1
```
7. Go to VSCode and open up the `HW1` Folder

## Directory Structure

For all the GTests to work and for the autograder to work as intented the directory structure must remain the same:

```bash
├── CMakeLists.txt
├── CMakePresets.json
├── gtest
│   ├── gtestmain.cpp
│   ├── count_gtests.cpp
│   ├── knot_gtests.cpp
│   └── stack_gtests.cpp
└── src
    ├── convert_knots.cpp
    ├── convert_knots.hpp
    ├── letter_count.cpp
    ├── letter_count.hpp
    ├── stack.cpp
    └── stack.hpp
```

## Overview and Objectives

Homework 1 consists of writing 3 small programs in C++:

1. `convert_knots.hpp` — A program that converts knots into miles per minute, using the data types int and double.
2. `stack.hpp` — A program that implements a stack, using it to reverse the characters in each line of input.
3. `letter_count.hpp` — A program that counts the frequency of occurrence of every letter in the input.

## Relation to Course Objectives

With `convert_knots`, you will gain experience writing C++ functions, understanding the difference between function **declarations** and **definitions**, and passing parameters and returning a value. You will deal with mixed-type arithmetic with `int` and `double`, and the issues that arise with type conversion and rounding.

With `stack`, you will implement a class, add error handling, and gain experience with using an array as a stack. It gives you experience with `++` and `--` and how to use their return values properly, as well as reading and writing I/O with strings.

With `letter_count`, you gain more experience with C++ arrays, characters, dealing with characters as indices into an array, and more I/O.

## Programs, Files, and Classes

First read the instructions and code screenshots thoroughly.

> ⚠️ Be sure to use exactly the names given in these instructions for files, functions, and classes, because the autograder will be expecting those exact names.

Write one program at a time in the order given, then run it to see if it works, then submit to GradeScope.

## 1. Convert_knots

The program named convert_knots converts knots into miles per minute.

- The file `convert_knots.hpp` contains the function that does the conversion.
- The file `convert_knots.cpp` contains the `main()` function which calls the function in `convert_knots.hpp`
- The file `knot_gtests.cpp` tests the function with the GTest platform, provided on Github.
  
### 1.1 convert_knots.hpp

In a file named `convert_knots.hpp`, write a function called `knots_to_miles_per_minute`, that takes one parameter named `knot` of type `int`, and returns a `double` value of the knots converted to miles per minute.

#### Use these numbers to compute the conversion:

 - 1 knot = 1 nautical mile per hour = 6076 feet per hour
 - 1 mph = 1 mile per hour = 5280 feet per hour
 - 1 hour = 60 minutes

### 1.2 convert_knots.cpp

Next, in a file named `convert_knots.cpp`, write a `main()` function that calls your function `knots_to_miles_per_minute`. Read an `integer` from `cin` and then print the number converted to miles per minute, as a `double` floating point, to `cout` by `calling knots_to_miles_per_minute`.

Here is an example that you may use, or you may write your own version.

![Screenshot of convert_knots.cpp](/assets/1-2.png)

Build and run

To compile, use the [Build](#build-instructions) instructions found below

> 💡 C++ is notorious for its long, incomprehensible compiler messages. If you get compiler errors, read this [tutorial](https://www.learncpp.com/cpp-tutorial/developing-your-first-program/) about how to develop your program one thing at a time to constrain where the problem lies, how to interpret compiler messages, and how to debug.

### 1.3 Test convert_knots.hpp with GTest

Before you submit to GradeScope, test your `convert_knots.hpp` with GTest, using the file `knot_gtests.cpp`. GTests will also be used by the autograder. Writing unit tests is a best practice, and in future homeworks we will test your unit tests. For now, this is an opportunity to see how GTest works and experiment with it.

![Screenshot of knot_gtests.cpp](/assets/1-3.png)

As you can see, this test file includes your `convert_knots.hpp` file that you just wrote, and has a test for comparing the output of `knots_to_miles_per_minute` for input `2` with the output `0.0385393`. The expression `EXPECT_NEAR(x, y, d)` checks if `x` and `y` are within `d` of each other. Otherwise the test fails. So in this case we check with a precision of only `0.01`.

If you have implemented the conversion correctly, this test should pass. However, just to be sure, you should add another test. This time, we want to test that our output for `3` is correct. Add your test just below where it says `// ADD YOUR TEST HERE`:

```cpp
TEST(ConvertKnots, Three) {
    EXPECT_NEAR(0.057539, knots_to_miles_per_minute(3), 0.01);
}
```

This will add a test to the `ConvertKnots` set named `Three` and test that the values of your function and the number provided are (approximately) equal. Now that you have added another test, you should build the `knot_gtests` target with CMake and run it. The output should look something like this:

![Screenshot of cmake output](/assets/1-3-2.png)

Once your `convert_knots` program seems to be working correctly, you can submit it to GradeScope for autograding, following the instructions to submit from GitHub.

## 2 stack
The second program implements a stack of characters. To understand how a stack works, read [What is a Stack](https://runestone.academy/ns/books/published/cppds/LinearBasic/WhatisaStack.html?mode=browsing)? and [The Stack Abstract Data Type](https://runestone.academy/ns/books/published/cppds/LinearBasic/TheStackAbstractDataType.html?mode=browsing).

 - In the file `stack.hpp`, define class `Stack` and 2 helper functions.
 - In the file `stack.cpp`, write a `main()` function that calls the functions in `stack.hpp`, reading a line of characters and printing them in reverse order until the user types the keystroke for the end of file (`Control-D`)
 - In the file named `stack_gtests.cpp` provided on GitHub, use GTests to test your stack.

### 2.1 stack.hpp

Implement a **stack** that holds up to `1000` characters, using an array of `1000` type `char`. Use good programming style to define a **symbolic constant** for the `Stack` capacity, and use **ONLY** that symbolic constant thereafter. The number `1000` should not appear in your program more than **ONCE**!

Below is a **class declaration** listing those member functions. A class declaration lists the methods of the class, with each method statement ending in a semicolon. Convert each member function declaration into a class **definition** by **replacing the semicolons** at the end of each declaration with the body of each of these methods enclosed in **curly braces**.

> Remember, when you are learning a new programming language, NEVER copy/paste code! Type all the code below carefully, while thinking about its meaning, in order to master C++ syntax as quickly as possible. It will save you time later!

![Screenshot of stack.hpp](/assets/2-1.png)
Comments are ABOVE the relevant line of code.

Do all reasonable error checking in these class methods.

 - `push()` must add the character to the stack only if the stack is not full.  
 - `pop()` and `top()` will return the top character only if the stack is not empty.  
 - `top()` or `pop()` on an empty stack should return `@` (the at sign character).
 - You can also print error messages.

### 2.2 stack.cpp 

In a file named `stack.cpp`, write a `main()` function that does the following:

 - declares a Stack object,
 - declares a String object,
 - then loops,
    - reading a line of input at a time,
    - pushes the character onto the Stack,
    - then pops them off and prints them as they are popped off, thereby printing the reverse of each line.

Write and use the helper functions `push_all()` and `pop_all()` to do the work in the body of the `main()` loop. Note `pop_all()` must print a newline at the end to behave properly when used as shown in the screenshot below.

Finally, `main()` should return `0` at **End of File**, which is sent when the user types `Control+D` (the Control key and D key at the same time, without the angle brackets). This key combination causes **End Of File** to be true, causing your program to exit successfully.

Study this example for inspiration on how to write your `stack.cpp`. Notice that `stack.cpp` must `#include "stack.hpp"` in order to access the definitions made in `stack.hpp`. Double quotes surround `stack.hpp`, because it is your own file. Angle brackets are used with library files, such as `#include <iostream>` Also note that Standard Library header files do not use .hpp (or .h).

![Screenshot of stack.cpp](/assets/2-2.png)

## Sample Output

```
stack
raymondklefstad
datsfelkdnomyar
this is a test of my silly line reversing program
margorp gnisrever enil yllis ym fo tset a si siht
madam Im Adam
madA mI madam
racecar
racecar
radar
radar
deified
deified
civic
civic
^D  
⬆️(type a <Control-D> to send end-of-file to exit the program)
```

### 2.3 Test stack with GTest

Before you submit to GradeScope, test your `stack` program with GTests, which will also be used by the autograder. Use the `stack_gtests.cpp` file provided in this repo.

Once your `stack` program seems to be working correctly, submit it to GradeScope for autograding, following the insturctions [here](#submission).

## 3 letter_count.cpp

Program 3, named `letter_count`, counts the frequency of occurrence of every letter in the input.

 - In the file `letter_count.hpp`, write the functions given in the description and screenshot below.
 - In the file `letter_count.cpp`, write a `main()` function that calls the functions in `letter_count.hpp` appropriately to implement the program.
 - In the file named `count_gtests.cpp` provided here, use GTests to test your `letter_count`.

The `letter_count` program reads strings from cin - one line at a time - and counts the frequency of occurrence of all the letters (ignoring all other characters), then prints to cout the uppercase letters A through Z with their corresponding frequencies.

The frequency counting is [case insensitive](https://en.wikipedia.org/wiki/Case_sensitivity), counting all the letters as if they were uppercase. For example, 5 a's and 2 A's would be counted as 7 A's.

Your program will use **an array of** `int` **indexed by** `char`. Write a helper function, `char_to_index()`, to convert characters to valid array indices, e.g., `A to 0`, `B to 1`, ..., `Z to 25`. Also write another helper function, `index_to_char()`, to convert back the other way from an index to a char, e.g., `0 to A`, `1 to B`, ..., `25 to Z`.

 - Define an array of `N_CHARS`, which is 26, `int` counters indexed from 0 to 25, corresponding to letters from A to Z. Initialize all these `int` counters to zero.
 - Read each line of text into a `std::string` variable from the standard input (`cin`) one line at a time. Call `count()` to increment the counters associated with each letter in the line. Ignore any characters that are not letters. If any letter is a lowercase letter, convert it to uppercase.  Then increment the counter associated with that `char` in your array.
 - When finished counting the characters in the input, use the helper function, `print_counts()`, to write the characters with their associated frequency count (one per line, in the order A to Z) to `cout`. Here is the format of your output with no extra newlines.
<Letter><space><Count><newline>


### Example output looks like this:

```
A 725
B 103
C 355
... the letters D through W
X 15
Y 100
Z 9
```

![Screenshot of letter_count.hpp](/assets/3-1.png)
![Screenshot of letter_count.cpp](/assets/3-2.png)



## Build and run

To compile, follow the Build instructions [here](#build-instructions). 

### Sample input and output files for letter_count
 - Sample input file named [sample_doc.txt](https://ics.uci.edu/~klefstad/public/45c/sample_doc.txt) (provided here in src/)
 - Sample output file named [letter_count.txt](https://ics.uci.edu/~klefstad/public/45c/hw2/letter_count.txt)

With the sample input and output files, use the following command to run `letter_count` (hw1 $ is the Bash command prompt):

```bash
./build/count < src/sample_doc.txt > src/sample_output.txt
```

### 3.1 Test letter_count with GTest

Before you submit to GradeScope, test your `lettercount` program with GTests, which will also be used by the autograder. Use the `count_gtests.cpp` file in this repo.

Once your `stack` program seems to be working correctly, submit it to GradeScope for autograding, following the instructions [here](#build-instructions).

## How to Submit

In GradeScope for Homework 1, submit from GitHub the 6 files described above to GradeScope for autograding, following the instructions on GitHub.

 - `convert_knots.hpp`
 - `convert_knots.cpp`
 - `stack.hpp`
 - `stack.cpp`
 - `letter_count.hpp`
 - `letter_count.cpp`

The autograder program will compile your files using g++ (the same version as the Hub). Do not use a different compiler/different platform to write your programs! Troubleshooting help can only be provided for Hub/g++.

## Build Instructions

If you are not already in a terminal, you will need
to open a terminal and move into your project folder as show below:


**IMPORTANT**
You will need to make sure you have `Gtest` installed

```bash
sudo apt-get install -y libgtest-dev libgmock-dev
```

This time, we are going to go into a little more detail on how `CMake` works. The `CMake` process is
basically comprised of two steps: producing project build files, and actually building the executable for
the project. To produce the build files for our project we run the first command:

```bash
# Build Generator Command
cmake --preset default # Create a folder named `build` and run `CMake` to produce build files there
```

This command should only need to be run once! If you change `CMakeLists.txt` or add new files, you will need to run
this command again to update the build instructions.
Once you have the `build` folder and files, you will want to build the actual program. This can be done two ways.
You can either build everything at once:

```bash
# Target Build Command
cmake --build build   # Will build all of the `targets` described in the `CMake` file
```

Or you can pick a specific target to build. For this homework, there are 6 possible `targets`:
* `knot` (which is the `convert_knots.cpp` file),
*  `knot_gtests` (`knot_gtests.cpp`),
*  `stack` (`stack.cpp`)
* `stack_gtests` (`stack_gtests.cpp`),
* `count` (`letter_count.cpp`), and
* `count_gtests` (`letter_count.cpp`).
  
These `targets` are defined in the `CMakeLists.txt` file as `project(<name> CXX)`, so if you want to find
the `targets` yourself, you can always check that file. We will also always give you the available `targets`
in this class. Below are the individual `target` commands you can run:

```bash
# Build only convert_knots.cpp:
cmake --build build --target knot

# Build only Knot tests:
cmake --build build --target knot_gtests

# Build only stack.cpp:
cmake --build build --target stack

# Build only Stack tests:
cmake --build build --target stack_gtests

# Build only letter_count.cpp:
cmake --build build --target count

# Build only the Letter Count tests:
cmake --build build --target count_gtests
```

NOTE: If you build all targets with the `cmake --build build` command, you DO NOT need to
run the individual commands. The advantage of running the individual build commands is
being able to build only the parts you want to test. Also, unlike the Build Generator 
Command (`cmake --preset default`), you will need to run the Target Build Command 
(`cmake --build build <--target target>`) every time you make changes to your `*.cpp` or `*.hpp`
files. For example, if you build `knot_gtests.cpp`, and find out that your conversion does
not work for numbers above `10`, you will need to change `convert_knots.hpp`. Once you have
changed it, when you want to test it again, you can run:

```bash
cmake --build build --target knot_gtests
```

And it will build just that code with your updated changes! Very handy for testing one task
at a time.

After you have built your intended target, you will have three new executables you can run!
You will have `hw` which will be the code from `main.cpp`, `knot_gtests`, and `stack_gtests`.
You can run each one with the commands shown below:

```bash
./build/knot          # Runs the 'main' function from src/convert_knots.cpp
./build/stack         # Runs the 'main' function from src/stack.cpp
./build/count         # Runs the 'main' function from src/letter_count.cpp
./build/knot_gtests   # Runs the 'knot' gtest set of tests
./build/stack_gtests  # Runs the 'Stack' gtests
./build/count_gtests  # Runs the 'Letter Count' gtests
```

Once you have run the code above and it either produces the output you expected or passes
all provided tests, congratulations! You are now ready to [submit](#submission) your homework!

## Submission

All submissions will be done through [GradeScope](https://www.gradescope.com/). Open the GradeScope page
and select `HW1`.

First, we need to make sure that we commit all of our changes we made! In a terminal inside your project folder,
run the following command:

```bash
git commit -a -m "Submission commit of HW1."
```

Now that we have committed out changes, we need to push them to `GitHub` so that `Gradescope` can see them.

```bash
git push -u my_repo
```

Now on GradeScope, press the submit button, choose the `GitHub` option, and select your project and branch
as shown below:

![](docs/cs45c_hw1_github.png)

Now the autograder will run and give you a score!

## Credit

All code moved from [ICS45c](https://github.com/RayKlefstad/ICS45c/tree/hw1)
