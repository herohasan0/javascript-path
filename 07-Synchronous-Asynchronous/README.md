# Synchronous and Asynchronous


## Table of contents
* [Synchronous JavaScript](#synchronous-javascript)
* [Asynchronous JavaScript](#asynchronous-javascript)
* [Resources](#resources)

<img src="fig1.png" alt="synchronous-vs-asynchronous">

JavaScript is a single-threaded, non-blocking, asynchronous, concurrent language. It has a call stack, an event loop, a callback queue, some other apis and stuff.

JavaScript is a single-threaded programming language, single-threaded runtime, it has a single call-stack. It can do one thing at a time. That's what a single treaded means. 

## Synchronous JavaScript

As the name suggests synchronous means to be in a sequence, i.e. every statement of the code gets executed one by one. So, basically a statement has to wait for the earlier statement to get executed.

## Asynchronous JavaScript

Asynchronous code allows the program to be executed immediately where the synchronous code will block further execution of the remaining code until it finishes the current one. This may not look like a big problem but when you see it in a bigger picture you realize that it may lead to delaying the User Interface.

## Resources:
* https://adrianmejia.com/
* https://www.geeksforgeeks.org/
* What the heck is the event loop anyway ? Philip Roberts [Watch on youtube](https://www.youtube.com/watch?v=8aGhZQkoFbQ&list=LL&index=1)