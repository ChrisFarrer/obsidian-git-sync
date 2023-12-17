---
Title: Homework 4
Source: 
Created: 2023-11-28 21:48
Class: CSCI 305 - Analysis of Algorithms 1
tags:
---

# Assignment 4

I briefly worked with Ksusha Gotham on question one of this assignment. Other than that, I worked alone. 
## 1. Cribbage Scores

#### 1. How many 5-card outcomes are possible?

One way of approaching this problem is by dividing the question into two parts. Viewing the turned up card as a separate outcome rather than part of our hand, we have 52 different cards, and we're choosing four of them. This can be expressed using combination notation as:
$$52C4 = \dbinom {52}{4}$$
Then, for each of these outcomes, there are 48 other cards left. When we multiply that by our previous expression, we achieve:
$$\dbinom{52}{4} \times 48 = 12,994,800$$
#### 2. How many ways to make hand 1?

Hand one must take the form of:
$$\underline{5^*} \;\;\;\;\;\;\; \underline{5} \; \underline{5} \; \underline{J} \; \underline{J^*}$$
The asterisk denotes that the 5 turned up and one of the Jacks are the same suit. Because we know that both of these must be present, it farther limits our potential hands. 

We can divide the problem into three parts. First, we need to determine how many combinations of the two 5s we can make in our hand. Usually, there'd be 4 suits to choose from, but we know that one of the 5s must be the turned up card. Therefore, we're limited to choosing 2 fives from the remaining 3 suits: $\dbinom{3}{2}$ 

Next, we can determine how many Jacks are in our hand. One of them must match the turned up 5, and because the suit isn't left up to chance, we can exclude it from our consideration. That leaves us with three suits to choose for our last Jack:  $\dbinom{3}{1}$ 

Now that we have our combinations, we have to consider the possible positions our 5s and Js can end up in our hand. That can be expressed as: $\dbinom{4}{2}$ because we have four positions and only two unique values (not counting suits).

Putting it together, we get: $\dbinom{3}{2}$ x $\dbinom{3}{1}$ x $\dbinom{4}{2}$ = 36

#### 3. How many ways to make hand 2?

Since the turned-up card doesn't matter in this scenario, we can consider this hand as if we were to simply draw all 5 cards. To account for the suits each value can take, we can express this hand using two series of combination expressions.

The four can be one of 4 suits, same for the 6, and the 5s are can be any combination of 3 of the 4 suits. This is expressed as:
$$\dbinom{4}{1} \times \dbinom{4}{1} \times \dbinom{4}{3} = 16$$

To account for the ordering, we can use another series of combinations, this time decrementing the possibilities for the remaining spaces, starting with the 3 fives, then the six, then the four. 
$$\dbinom{5}{3} \times \dbinom{2}{1} \times \dbinom{1}{1} = 20$$
Combining the two together we get: 20 x 16 = 320


## 2. Randomized Algorithms

#### 1. Explain why it cannot be the case that once every n searches the algorithm takes $\Theta({n^3})$. 

We can use the definition of expectation to derive:
$$E[X] = q * \Theta(n^3) + (1-q)*\Theta(n)$$
In this case, q is the probability that $\Theta(n^3)$ runtime occurs. We can write it in this way because we know every other instance other than once every n will have the cost $\Theta(n)$ associated with it.

Plugging in 1/n for q, we get:
$$E[X] = \frac{1}{n} * \Theta(n^3) + (1- \frac{1}{n})*\Theta(n)$$
We can disregard the asymptotic notation:
$$E[X] = \frac{1}{n} *n^3 + (1- \frac{1}{n})*n$$

This algebraically simplifies to:
$$E[X] = n^2 + n - 1$$

This means that the dominating behavior of our expected runtime would be $O(n^2)$, and we would never achieve $O(n)$.

#### If, occasionally, the algorithm takes time $\Theta(2^n)$, how rarely must this occur?

We can use a similar setup as the first problem, except now we're trying to find what value of q would make the algorithm behave linearly.

To start, we have:
$$E[X] = q * \Theta(2^n) + (1- q)*\Theta(n)$$

Getting rid of asymptotic notation, we get:
$$E[X] = q * 2^n + (1- q)*n$$
To make the left side of this equation behave linearly, we have to satisfy:
$$q \times 2^n = n \rightarrow q = \frac{n}{2^n}$$
Thus, any number less than $\frac{n}{2^n}$ will not cause the left side of the equation to dominate, and because the denominator scales faster, it will not conflict with the righthand side of the equation.

## 3. Boats

#### What is the expected number of boats that return to their home village?

By simply multiplying the probability of success (1/100) by the number of trials (100): $$100 \times \frac{1}{100} = 1$$
In this case, we would expect one boat to return to it's home village.

#### What is the expected number of villages where 2 boats show up?

We know that $E(X) = 1$, thus $\lambda = 1$ . Using the Poisson distribution, we can say:
$$P(X=2) = \frac{\lambda^2 \times e^{-\lambda}}{2!} \rightarrow \frac{1}{2e}$$
Now that we have the probability, we can multiply by the amount of trials (villages) to find the expected value. 
$$\frac{1}{2e} \times 100 = \frac{50}{e}$$
