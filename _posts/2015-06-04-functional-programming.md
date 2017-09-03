---
layout: page
title: The Next Big Thing - Functional Programming
---

As quoted by Rob Martin (Uncle Bob)

> First, it’s almost certainly true that functional programming is the next big thing

As you might already heard, the buzz which is going around Functional Programming like ..


- What is this Functional Programming which everyone is talking about ?
- Why has it become increasingly relevant in today's scenario ?
- Do I need to learn these so called Functional Programming languages ?


Quoting Wikipedia,

> "In computer science, functional programming is a programming paradigm, a style of building the structure and elements of computer programs, that treats computation as the evaluation of mathematical functions and avoids state and mutable data."


As you can see, **Functional programming** is a way of thinking to solve problems in Computer Science and Mathematics. It provides you with tools and concepts to build your programs systematically to solve any problem.  


As Quoted by John Hughes in his famous paper "Why Functional Programming Matters"

> "Functional programming is so called because a program consists entirely of functions."


In Functional Programming you structure programs as functions taking other functions as inputs or returning other functions as return values. Functions are the language primitives and that means you can toss them around in your program.


These functions are much like ordinary mathematical functions which for a particular input value always return the same value as the result.

```ruby
 f(x) = 4x + 3
```
For x = 3, you always get 15 as the result. This property of functions is called "Referential Integrity" which is an important concept in Functional Programming.

Lets have a look at things you can't do in Pure Functional Programming languages.

- No Assignments.
- No Varying Your variables. (Immutable)
- No while/for loops.
- No Control over order of execution.
- No Side effects.

Now you might be thinking as to how can anyone program without all these features.
The truth is you can. 

> Functional Programming has its roots in Lambda calculus.


Lets dive in deep into the Basic Concepts which revolve around Functional Programming:

## First Class and Higher Order Functions.
### First Class Functions:

Quoting Wikipedia:

> A Programming language is said to have first class functions if it treats functions as first class citizens.

It means that functions are language primitives and can be passed to other functions as arguments or return other functions as return values. You can assign them to variables or any data structure for that matter.


## Higher Order Functions:

> Higher order functions are functions which can either take functions as their arguments or return them as their return values.

An example of a higher order function is ***"inject"***.

A Function taking other functions as its arguments:


**In Ruby:**

To calculate sum of 1 to 10 numbers.

```ruby
 (1..10).inject(:+)
```

***"inject"*** is a higher order function which takes '+' (which is a function) as its argument  and applies that function to each value in range (1..10) and returns the list back.

**In Clojure:**

```clojure
 (reduce + (range 1 11))
```

**"reduce"** being the higher order function.

A Function returning other functions as their return values:

**In Ruby:**

```ruby
 def square(value)
    ->(x) { x * value }
 end
```

square(2) returns an anonymous function which can be called later with an argument.

```ruby
 square(2).call(10)
```
returns 20 as result.


Higher order functions enable **“Currying”**

## Currying: 

> Currying is the technique of translating the evaluation of a function that takes multiple arguments into evaluating a sequence of functions, each with a single argument.( Partial application)

```ruby
 add = proc { |x, y, z| x + y + z }
 add5 = add.curry.call(5)
 add5and6 = add5.call(6)
 add5and6.call(10)
```

“add” is a function which takes 3 arguments, we can curry the above function (add) which takes 3 arguments and generate functions which take single argument each.
i.e add5, add5and6 etc


## Pure Functions

> Pure Functions have no side effects (Memory/IO).

> Pure functions always return the same value as result for a particular input.

For any particular input x the output will always be f(X). There are no side effects.

###Advantages of pure functions:

**Referential Transparency**: 
> The function returns the same result for a particular set of arguments, so if the same function is called again with same arguments, you can cache/memoize the previously calculated result and use it.

If no data dependency between two expressions, you can run those two expressions in parallel.
Compiler can reorder the expressions any way it wants to optimise the generated code. 

## Recursion:

> Iteration in functional programming languages is usually accomplished with recursion.
> Recursion is when a function calls itself and solves a sub problem of the original problem.

Lets consider the Recursive Factorial Function.

```ruby
 def factorial(n)
   if(n==0)
     return 1
   else
     return n * factorial(n-1)
   end
 end
 ```

The factorial function calls itself recursively to calculate the result.
As you are familiar that each recursive call creates a stack. This program crashes for bigger values of n. To avoid this problem, we can rewrite the above function as this.

```ruby
 def factorial_one(n, total=0)
   if n ==0
     return total
   else
     return factorial_one(n-1, n * total)
   end
 end
 ```

```ruby
 def factorial(n)
   return factorial_one(n, 1)
 end
 ```

This version is the tail recursive version of the factorial function.

## Tail Recursion:

> A recursive function is tail recursive if the final result of the recursive call is the final result of the function itself. 

As you can observe in above program that the final result of the factorial_one is the call to function itself. At each recursive call the current total is calculated and hence there is no need to maintain a stack for each recursive call and return. Thus some smart compilers optimise this recursive call and eliminate the creation of stack for each recursive call. This methodology is called 'Tail Call Optimisation'.

### Tail Call Optimisation:

> Process by which a smart compiler can make a call to a function taking no additional space.


## Non Strict Evaluations. (Lazy Evaluation):


> Lazy evaluation does not evaluate function arguments unless their values are required to evaluate the functional call.

```ruby
 print length([2+1, 3*2, 2/0])
 ```

In lazy evaluated languages the result of the above expression is 3.
Whereas that in strictly evaluated languages the above expression crashes with an exception.

This is because the strictly evaluated languages try to evaluate the arguments passed to a function whereas that in lazily evaluated languages do not evaluate the function arguments until used.

As mentioned in Wikipedia:

### The benefits of lazy evaluation include:

- Performance increases by avoiding needless calculations, and error conditions in evaluating compound expressions.
- The ability to construct potentially infinite data structures.
- The ability to define control flow (structures) as abstractions instead of primitives.

## Advantages of FP:

- Lock Free Concurrency
- More Modular Code
- Lazy Evaluation
- Composability
- Parallelism
- Improved ways of testing
- Lesser Bugs
- Referential Transparency

## Disadvantages of FP: 

- Steep Learning Curve.
- Cryptic Concepts. (Monads)
- List of Functional Programming Languages:

## Functional Programming languages

- Clojure
- Haskell
- F#
- OCaml
- Erlang
- Lisp
- Scheme
- Scala ( Both Object and Functional )

Imperative vs Functional Programming styles: 

> In Imperative style of programming you tell the computer what to do.
> In Functional style, instead of telling what to do, you rather describe what you want done.

Lets see the difference through an example:
In this example we calculate the sum of 10 numbers (1-10).

### Imperative: 

```ruby
 total = 0
 i = 0
 while i <= 10
   total += i
   i = i + 1
 end
total
```

### Functional: 

```ruby
 (1..10).inject(:+)
```

As you see, the functional style of programming is a lot more expressive and precise. 

> Functional Programming is like describing your problem to a mathematician whereas,
> Imperative Programming is like giving instructions to an idiot.

In Imperative programming we have special constructs in language for iteration, whereas in Functional programming languages we make use of recursion heavily. 


## Why Functional Programming is relevant today ?


 Functional Languages use a paradigm of programming wherein the Functions are pure and are referentially transparent which means that the functions lack side effects. The functions are non dependent on each other and always independently execute irrespective of other functions. This immensely helps in running these functions in parallel on multiple cores.

The main reason that Functional Programming languages are gaining traction these days include processors being shipped with Multiple cores, thus encouraging software developers to utilise the multi core architecture of processors and run programs in parallel to speed up the process of program execution. 

Writing concurrent programs is indeed supported in Imperative paradigm, but usually this process is troublesome and error prone. 
    
## Do you need to have this skill ?

Yes, it is  a must. 
For one thing, the world is moving towards concurrency and parallel computing, which means that the knowledge of functional programming languages will be a must.

Secondly, understanding and coding in functional paradigm will help you in getting a new insight into solving problems or rather approaching for a solution to a problem. This in-turn will make you a better programmer in any language of your choice. 

