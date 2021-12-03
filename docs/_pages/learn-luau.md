---
permalink: /learn-luau
title: Learning Luau
toc: true
---



Luau can be a tricky language to learn for people who have never written code before. This tutorial is aimed for absolute beginners, especially those who have never written a line of code before.

## Getting Started: Recipes & CookieBot

We want to make cookies (but we don't *actually* want to make them). We have a recipe for making cookies, and we will have a robot, **CookieBot 3**, make the cookies for us. Let's look at exactly how a robot would understand our recipe.

```md
Recipe for Cookies!

Ingredients:
 - 1 parts butter
 - 3 parts flour
 - 1 part sugar
 - 1 part egg
 - Some chocolate chips

You need:
 - An oven
 - A bowl
 - A pan
 - A spoon
```

We've already told our robot some very important information: *What it needs*. These are also known as **dependencies.** For example, our robot now knows it needs to find a pan, bowl, and roller. It can have all of these tools ready, and does not need to find the tools right as they are needed!

```md
To *HEAT THE OVEN*, you should:

    - Set the temperature to 350 degrees
    - Do other tasks until the oven has preheated

You're done *HEATING THE OVEN*!

To *ADD AN INGREGIENT* with *A NEW INGREDIENT*, you should:

    - Put *A NEW INGREDIENT* into the bowl.
    - Mix with the spoon until even

You're done *ADDING AN INGREGIENT*!
```
Now, we've told our robot about some common tasks. These tasks may be repetitive, or we may want to keep these tasks out of the way of our recipe so that it is easier for humans to read. Both are excellent reasons why we should create these tasks!

In Luau, these tasks are called **functions**, and it is how we organize our code. Imagine having to write out how to mix ingredients every time we wanted our robot to mix an egg with flour!
Now that we're done telling our robot about basic tasks, we can start writing our recipe.

Functions can take arguments, just like `*A NEW INGREDIENT*` in our `*ADD AN INGREDIENT*` function. This allows us to have the same function do multiple tasks--We won't have to make a function specifically for adding flour or eggs, when we can use the argument to switch between ingredients!

```md
To *MAKE THE COOKIES*, you should:

    - *HEAT THE OVEN*
    - *ADD AN INGREDIENT*: Butter
    - *ADD AN INGREDIENT*: Sugar

    - Mix with the spoon some more

    - *ADD AN INGREDIENT*: Egg
    - *ADD AN INGREDIENT*: Flour

    Now we're ready to prepare our pan!

    - Take *THE MIXTURE* out of the bowl
    - Take *A SMALL CHUNK* out of the mixture, about 1 cubic inch.
    - For each chunk, you should:
       - Roll *A SMALL CHUNK* until it is a sphere
       - Place *A SMALL CHUNK* on the pan, such that it is 2-3 inches away from all other small chunks.

    Ready to bake!

    - Put the pan in the oven
    - Wait 14 minutes
    - Take the pan out of the oven

You're done *MAKING THE COOKIES!*

```

Now that we have written out all of our instructions, CookieBot will read our instructions from top-to-bottom, and will do exactly what we ask it do to. We could have CookieBot keep the cookies in the oven for two hours if we wanted it to!

We have just discovered basic programming syntax. In reality, this way of programming is not far off from how Luau comprehends and runs code.

> **Syntax:** Special symbols and words used in a programming language, like `+`, `*`, and `function`

## Basic Types

Luau has several built-in datatypes. Each of these types is designed for a specific purpose, but because of Luau's flexibility, they can be used for a variety of tasks.

### Booleans
**Booleans** allow us to say if something is "true" or "false". These are great for a variety of tasks where you only need to know if something is "true" or "false". For example, "Is the lightbulb on?" can be answered as a "true"/"false" question.

```lua
have_dinosaurs_escaped = false
have_dinosaurs_eaten_people = false
are_dinosaurs_friendly = true
```

### Strings 
**Strings** are how we store text in our programs. There are many ways to create a string. To start with, we'll use quotes (`"text"` and `'text, 2'`) to create strings.

We can't have strings outside of quotes in our code, because then Luau would not know which parts of our file is for code, and which parts are for text.

As an example, we'll create some text to store the names of our enemies and friends.

```lua
friend = "Bob"
enemy = 'Alice'
```

Now, when we run this code, `friend` will be set to `"Bob"`, and `enemy` will be set to `"Alice"`.

We can *concatenate* strings if we want to append one string to another. We do this by using the concatenation operator, or `..`
```lua
say_hello = "Hello there, " .. "Alice" .. "!"
```

This allows us to personalize strings. Maybe we want to warn our worst enemy not to come a step closer!
```lua
warning = "Don't you dare set foot on my land, " .. enemy .. ", or you will be destroyed!'
```

### Numbers
**Numbers** allow us to work with numbers and perform math in our code. Luau numbers can have decimals, exponents, and can be really, really large (up to `2^53`, or a number with 15 zeroes!)

We can do some math with numbers, using the standard `+`, `-`, `*`, and `/` symbols.

If we want to find the sum of three numbers, we just write the equation like we would on paper:

```lua
number = 2 + 7 + 15
```

Luau also allows us to write code in parenthesis, to explicitly state the order we want our numbers to be operated on. We can put as many parenthesis as we like in our code.

```lua
number = (2 * 4) + (2/((2/7)-19))
```

We can also use exponents, including `e`.
```lua
number = 2^64
number_2 = 2.35e+19
```

Luau has some aditional symbols we can use for math: `+=`, `-=`, `*=`, et cetera. Let's take a peek at how these are used.

```lua
my_number = 17

--  These two are EXACTLY the same!
my_number = my_number * 4
my_number *= 4
```

Using these symbols can be quicker and easier than writing it out yourself.

## Tables

**Tables** are an extraordinarily useful way of keeping track of information. Up until now, we've been assigning our numbers and names to *variables*, which can be hard to keep track of.

Tables store information in a key-value format, which is a very intuitive way of storing information. Here's an example:

| Key       | Value         |
|-----------|-------        |
| Enemy     | "Alice"       |
| Friend    | "Bob"         |
| Number    | 1.844674e+19  |

At first, this may seem counter-intuitive, but it can be very useful, especially when you want to store multiple enemies and friends.

Let's take a look at how we create a table.

```lua
my_table = {
    Enemy = "Alice",
    Friend = "Bob",
    Number = 1.844674e+19
}
```
To start with, we will wrap our table in curly braces (`{ and }`), which tells Luau that we want to create a table.
Next, when we want to add an item to our table, we use the same code we used to set variables: `key = value`. At the end of a table entry, we use a comma (`,`) or semicolon (`;`) to tell Luau that we are ready to add the next entry.

However, table entries cannot start with a number. What if we wanted to store a list of something?
```lua
--  THIS CODE DOES NOT WORK
my_fruit = {
    1 = "Apple",
    2 = "Bannana"
}
```
Or, what if we wanted to use a variable as a key in a table?

```lua

favorite_fruit = "Favorite Fruit"

my_fruit = {
    favorite_fruit = "Apples"
}

```

We can tell Luau that we want to use a data type, like a string or number, when creating a table.

```lua
favorite_fruit = "Favorite Fruit"

my_fruit = {
    [favorite_fruit] = "Apples",
    ["Second Favorite Fruit"] = "Watermelon",
    [1] = "Bannanas",
    [2] = "Tomatoes",
    [true] = "This table has a key of 'true'!"
}
```

> **Note:** Just like tables, Lua (and Luau) variables cannot start with a number. However, you **cannot** use braces (`[ and ]`) to create a variable, as in `["bannana"] = "a fruit"` is not allowed.

### Arrays

Using `[1], [2], [3]...` may get repetitive, so Lua has some syntax sugar for creating arrays. You don't need to define a key with arrays--You just need to list the values.

```lua
my_array = {
    "First Item",
    "Second Item",
    "Third Item",
    "Fourth Item!!!",
}

--  This is the exact same as
my_table = {
    [1] = "First Item",
    [2] = "Second Item",
    [3] = "Third Item",
    --  ...
}
```

> **Syntax Sugar:** A special way of writing code which is designed to make programming easier.

### Reading from tables

Great! We've learned how to put information *in* to a table, but now what if we want to take information *out*? There are two main ways, depending on your use case.

If you know the key when you write your code, and it does not begin with a number, you can use a dot (`.`):
```lua
Enemy = my_table.Enemy
```
Otherwise, you can use braces just like when you create a table.
```lua
first_fruit = my_fruit[1]
true_fruit = my_fruit[true]
favorite_fruit_value = my_fruit[favorite_fruit]
```

**Tables have weird behavior when used as keys** (they are perfectly fine to be used as values), so you should avoid using tables as keys. Here's an example:

```lua

key = { bannana = "a fruit" }
second_key = { bannana = "a fruit" }

table = {
    [key] = "Congradulations! You used the right table."
}

value = table[key] -- Works!
second_value = table[second_key] -- Does not work :(
```

Even though the tables have the same value, because they were created as seperate tables, they cannot be used interchangeably as table keys.

## Variables

Now, we've learned about all the basic data types, and we've so far been setting variables in our code. For example, when we learned about numbers, running `number = ...` sets a variable called `number`.

Like other things in luau, multiple variables can be set at once. If we wanted to set `a`, `b`, and `c`, we don't have to write `a = ...` every time.

```lua
a = 4
b = 38
c = "Pineapple"

--  The above is equivalent to 
a, b, c = 4, 38, "Pineapple"

```

## Functions

As we learned with CookieBot, functions are a great way to organize repetitive routines. In Lua, functions are very comphrehensive, and allow you to do almost anything. 

Luau provides several built-in functions, like `print`, which writes some text to the screen (don't worry, `print` doesn't have anything to do with printers!)

If we want to invoke a function and have Luau execute it's contents, we'll need to tell Luau *how* we want to run our function. For example, doing this:
```lua
print
```
Won't do anything, because Luau does not know if you want to use the function or not. To explicitly tell Luau, "I want to use this function", we use parenthesis!
```lua
print()
```
Now, Luau will execute the function's contents. Even if we do this, however, all that shows up is a blank line. `print` expects you to provide a value to print, whether it be a string, number, or boolean. If we don't give `print` anything, it will just give us an empty line!

Within the parenthesis, we can provide *arguments*. Arguments are how we pass information into the function. Arguments can be anything: a string, table, or even another function!

In this case, we want to tell Luau that we want to say "hello world". We can do this by putting "hello world" within the parenthesis:
```lua
print( "Hello, world!" )
```

If you want to give the function multiple arguments, you can separate arguments with a comma.
```lua
print("Hello World!")
--  As many spaces as you want!
print     ("Hello World!")
--  Separate arguments with a comma
print ("Hello", "World!")

--  THIS DOES NOT WORK:
--  You can't have a comma at the end with no argument:
print ("Hello", ) <-- Error!
```

Lua functions can also return values. As we learned with variables, we can accept multiple return values from a single function:
```lua
my_value = get_one_number()

first_number, second_number, third_number = get_three_numbers()
```

Now, let's write our first function! We will begin by meeting some new people. We will accept a single argument, `name`, and use the `return` keyword to pass our greeting back to our code once the function is complete.

```lua
function meet_new_person(name)
    return "It's nice to meet you, "..name.."!"
end

greetings = {
    meet_new_person("alice"),
    meet_new_person("bob"),
}
```

Great! Now, let's take a closer look at what we just did.

When we created our function, we accepted a single argument, called `name`. From this point forwards, `name` becomes a variable in the function. We can use it, so long as we provide an argument to our function when we tell Luau to execute it. If we don't provide an argument, we might run into some issues down the line.

```lua
meet_new_person("alice")
meet_new_person()   --  Error! Attempt to concatenate nil with string.
```

We can also provide more arguments for our functions than the function will use. If this is the case, Luau will throw away any extra values.

```lua
meet_new_person("alice", "bob") --  "bob" goes unused.
```

### Anonymous functions & values

Functions are very versatile. For example, here's an *anonymous* function:
```lua
my_greet_function = function(name)
    return "It's nice to meet you, "..name.."! I am now an anonymous function!"
end
```

Functions are normal values, just like tables and numbers. We can make a function a variable just like anything else!

```lua
function meet_new_person(name)
    return "It's nice to meet you, "..name.."!"
end

meet_new_person_var = meet_new_person 
-- Note! this is what luau assumes you want to do when you do not include parenthesis.
```

### Table Methods

Luau has a lot of syntax sugar when it comes to creating functions. Let's take a quick second to look at how we can make writing and using Luau functions more enjoyable.

Tables are a huge part about how we work with functions. When we organize code into multiple files, we want to be able to share code between files easily. Instead of explicitly taking each function from a file, we can bundle all of our functions into a table and use it that way.

We can start by defining our table, and then use `function Table.Index(args...)` to write our functions.

```lua
module = {}

function Module.sayHello(name)
    return "Hello, " .. name
end

Module.sayHello("bob")
```

### Self

Luau has one more trick up it's sleve: `:`! `:` is a special operator, sometimes called the `self` operator, which allows you to write *Object-oriented code* easier.

> **Object Oriented Code:** Instead of writing code in functions, you will create tables that contain all the functions you need.

When we use `:`, we tell Luau that we would like to tell the function we are using what table it is currently in. Take this example:

```lua
module = {}

function Module.createGreeter(name)

    local greeter = {
        name = name
    }

    function greeter:SayHello(newName)
        return "Hello, " .. newName .. "! My name is " .. self.name .. "! Nice to meet you :)"
    end

    return greeter

end

my_greeter = Module.createGreeter("bob")
my_other_greeter = Module.createGreeter("alice")

my_greeter:SayHello("alice")
my_other_greeter:SayHello("bob")
```

> **Note:** See that `local` right there? Take notes! We're going to be learning what this does in the next section.

We have created two tables! Each of these `greeter` tables has a function inside of it, called `SayHello`. If we were to call `my_greeter.SayHello()`, `SayHello()` would not know it was a value in a table! When we use `my_greeter:SayHello()`, we tell Luau to set `self` to `my_greeter`, so that the function can automate certain tasks. In reality, when we use `my_greeter:SayHello` to *create* a function, Luau really just adds a new argument, called "self", to the beginning of our argument list.

Here's another example:
```lua

function my_func(self, arg1)
    print("self = ", self)
    print("arg1 = ", arg1)
end

my_table = {
    my_func = my_func
}

function my_table:my_func_two(arg1)
    print("self = ", self)
    print("arg1 = ", arg1)
end

--  These four function executions are EXACTLY the same!
my_table.my_func(my_table, 5)
my_table:my_func(5)

my_table.my_func_two(my_table,5)
my_table:my_func_two(5)
```
Notice how `:` and `.` can be used interchangeably. This makes `self` functions very versatile. While they may seem complex and pointless at first, but this syntax shortcut will become your best friend as you explore advanced concepts of Luau programming.

## Local Variables

We can also set variables as `local`. Local variables are neat ways to organize your variables. So far, we've been working with *global* variables, which can get messy.
Here's an example: In this function, we want to say hello to people using a global variable.
```lua
function say_hello(person)
    greeting = "Nice to meet you, ".. person
    return greeting
end

print (say_hello("Jack"))
print (say_hello("Jane"))

--!!!
print (greeting)
```
But wait! because we used a *global* variable, our *greeting* variable has escaped into the rest of our code, instead of staying contained within the function.
This is why global variables are not ideal--They are shared between all functions, and can be slow to use!

Let's look at the same example, but with local variables.

```lua
function say_hello(person)
    local greeting = "Nice to meet you, ".. person
    return greeting
end

print (say_hello("Jack"))
print (say_hello("Jane"))

--This errors, because "greeting" cannot be found!
print (greeting)
```

Now, `greeting` is contained within our function. It cannot escape to mess with other bits of our code. Local variables are a lot faster than global variables, so ideally you should *only* use local variables.

*Functions can be local too!* Lua has some neat syntax sugar specifically for creating "local" functions.

```lua
local function local_function()

end
```

These functions are normal local variables (just like `local local_function = function() .. end`). 

## Upvalues

Upvalues are an awesome tool Luau gives programmers. Let's take a look at an example where upvalues are useful:

```lua
local function create_counter()
    local value = 0
    return {
        increment = function()
            value += 1
        end,
        decrement = function()
            value -= 1
        end,
    }
end
```

Of course, we could write this out using tables, `:`, and `self`, but this is a lot quicker. Taking a closer look, however, there *should* be a problem with this code.
```lua
    ...
    --  Okay, so we define "value" here.
    local value = 0
    return {
        increment = function()  -- And we create a new function
            --  But wait! "value" does not belong to "increment"!
            --  It was defined in a different function!
            --  This should cause an error, right?
            value += 1
        end,
        ...
```
Fortunately, Luau takes care of all this for us, and it has a name: Upvalues! No matter where `increment` or `decrement` go in your code, they will all still be associated with the same number. Phew!