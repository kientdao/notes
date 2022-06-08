---
title: Collatz Conjecture
date: 03-08-2021
private: false
---

## What is it?

The Collatz Conjecture can be defined simply as:

$$
F(x) =
     \begin{cases}
       \dfrac{n}{2} &\text{if }{n} \equiv 0 \\
       3{n}+1 &\text{if }{n} \equiv 1 \\
     \end{cases}
$$

With any number being passed in recursivly converging on 1 (apparently). [[cout-vs-printf]] C++ cout VS printf

Still unsolved, but verified for everynumber under 2<sup>68</sup>, so gotta start around 3 quintillion.

By adding 1 to your number x, you shuffle its prime factors in a certain way. Its easy to see that x and x+1 share no factors in common, but what else can you say about the factors of x+1 by looking at the factors of x? This, I believe, is the main issue at heart here. The issue of "what the fuck does addition of 1 do to the prime factorization of a number".

there's a pretty shitty "proof" [here](https://deepthoughtnews.wordpress.com/2019/12/13/solved-the-collatz-conjecture/), written in C#, obviously.

Pretty much, someone thought they were smart by finding out that x must eventually hit some kind of 2<sup>k</sup>, good read if you're looking for some satire though.
