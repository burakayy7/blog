---
navigation: true
cover: "assets/images/arduinoEng/arduino_prog2.png"
title: How to get started with Engineering | Arduino Programming
date: 2024-06-27
class: post-template
layout: post
current: post
subclass: 'post'
tags: arduino
---

Now, if we want to be a good engineer in this day and age, we need to also know Computer Science. Arduino especially relies on this as this is how we will program the Board.

Ok, so you probably have learned that Arduino is a development platform where you program a microcontroller. In the Arduino Environment, you do this with the [Arduino API](https://docs.arduino.cc/learn/programming/reference/) (I am assuming you have downloaded the Arduino IDE in the previous lessons).

Let's dive in!!


# Arduino Sketches
### A look at the Arduino IDE

So, if you open the IDE, a new sketch should automatically appear. I will revist the details later, but you should see something like this:

```cpp
void setup() {
    
}

void loop() {

}
```

I will go into how these work more later, but for now, just know that _void setup()_ is a place which you can put in code that you want to **only run once at the beginning of the program** and _void loop()_ is code for **running continuously, in a loop**.

For most of the examples below, I will run them in setup(). **And please note that in C++, you _must_ end every line of code with a semicolon: ";"!**





# Variables

So, let's say you had a bunch of data or information you wanted to store in a computer program, how would you do that? The simple way is to declare a _variable_ and the compiler (converting code to machine language) will the Arduino how to store a piece of information. 

That's simply what a variable is, a way to store information. 

Let's see a few examples of the different types of info you can store:

- Characters: store single characters, like 'A' or '$'

- Integers: stores integer numbers, like 20 or 4

- Floats: stores numbers with a decimal value, up to a certain degree, like 30.799 or 3.1415

- Doubles: can store even more deicmal values that floats, like 40.2991988476

- Strings: is actually a class/object that stores a group of characters, like "Hello"


Now, let's see how we can use these in Arduino code (which is just C++) to store data. 

```cpp

int age = 30;
String name = "Bob";

void setup() {
    Serial.begin(9600);
    Serial.println(name);
    Serial.println(age);
}

void loop() {

}
```

As you can see, to declare an Integer, I use the keyword _int_ which signals that the variable name I enter after this will be an Integer.

So the below code will just declare a variable as an Integer:

```cpp
int height;
```

but to give the variable "height" a value, I must assign it using an equal sign and then put a corresponding value that matches the variable type:

```cpp
int shoe_size = 20;
```

So after the variable type, I can name it any name I want, but it cannot contain ANY spaces, because any space seperates different parts of the program instructions.

So all of the following are valid variable names:
```cpp
hello_world;

silly_cat_videos;

broken_latptop_that_I_dontWant;

camelBackNotationAlsoWorks;

Woohoo_Big_summer_Blowout;

```

Floats, are not much different:

```cpp
float this_is_a_float = 10.9;

float pi = 3.1415;
```

And similarly, we can declare Strings and characters:

```cpp

String name = "Bob";

char initial = 'B';
```


As you can see, with this tool of storing values in different types of variables, we can allow certain "programmable" ideas in our code.

### Arithmetic

I want to quickly touch on how we can use these variables in our program.

Adding Integers:

```cpp
int num1 = 5;
int num2 = 10;
int num3 = num1 + num2;
```

Here I just declared a new Integer Variable that is set to (equal sign) the sum (by using the + sign) of num1 and num2; This is how variables are used, you can just call their value later by refrencing their variable name.

Below is how we can "increment" values:

```cpp
num3 = num3 + num2;
```

How this works is that we set the memory space for num3 to what num3 is now plus num2. So every time this line of code is run, num2 is added to num3. The above is equavalent to the below, just a different notation:
```cpp
num3 += num2;
```

I can also subtract:
```cpp
num3 -= num1;
```

multiply:
```cpp
num3 *= num2;
```

or divide:
```cpp
num3 /= num1;
```


# Functions

So let's say you have a piece of code that you want to use in multiple places in your program. There are two options: either copy/paste that code every time, or have some variable declaration that is actually a 'mini program' that will run that piece of code every time you call it.

In modern programming, this is called _functions._ In our Aruino C++ Programming language, here is how we make a function:

```cpp
int number = 0;
void function1() {
    number = number + 1;
}
```

So now, every time I want to increment _number_, instead of writing that line of code, and just simply call the function. Let's break the above code apart; the _void_ key word refers to what this function will return. Every function can return a value, say I'm making a calculation, I can have a function return or output the final value of the math calculation. So when we define a function, we have to define which type of variable will it return. In this case, we made it a void (which is nothing, basically), which means this function will not return anything.

But now let's say I want to increment the number by a variable amount, how would I do that:

```cpp
int amount = 5;
int number = 0;
void function2(int addAmount) {
    number += addAmount;
}
```

In the parenthesis of the function, I can make a variable, in this case an Integer named _addAmount_, and I can refrence that in the code. Here is how I would use this function:

```cpp
function2(4);
```
So here, number is incremented by 4 instead of 1 in function1. All of the code is written in between the parenthesis, that is what defines the function code, everything in between the parenthesis.


**Again, like all the other things, I will go in more detail once we actually start coding!**




# Arduino Sketches, revisited

So now that we know about functions, we can see that the _setup()_ and _loop()_ sections in the Arduino IDE, are really just functions that are already defined for us. In these functions, we will write our main code, but we can also make our own functions!

In the following lessons, we will write code to accomplish tasks using these two; this lesson was just an introductary lesson for coding.

