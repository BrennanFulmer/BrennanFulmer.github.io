---
layout: post
title:      "Difference between pass-by-value and pass-by-reference"
date:       2018-06-14 19:15:57 +0000
permalink:  difference_between_pass-by-value_and_pass-by-reference
---


I'll start with the recent example that finally crystallized this concept for me.

```
def fork_found?(board)
	fake = board
	fake.each_with_index { |spot, index|
			if spot == ' '
				fake[index] = 'X'
```

This code snippet is from the Tic Tac Toe with AI project.
I was writing a method so that the computer's AI would be able to detect forks by testing random moves on a seperate copy of the board array.
What initially eluded me though was why this kept resulting in an X being added to the board even when the computer player was assigned O.
Upon doing some research I realized that while Ruby is pass-by-value its more nuanced than that.
In pass-by-value languages when a function is called with a variable the function just gets a copy of the variables value to work with so any changes made don't impact the original variable.
As you would expect pass-by-reference then means that variables are treated as references to a value instead of a value in and of themselves.
So in practice when passed a variable the changes functions make directly affect the original variable because the same value(s) it references are being operated on.
Getting back to my example though, if Ruby is pass by value this should have worked right?
The complication is that in Ruby variable values are references so a more accurate descrition of how it handles parameter passing would be pass-by-value-reference. The underlying reason behind this contradiction has to do with how these different approaches store data in memory.
In pass-by-value when a function is called with values it copies them somewhere else into memory and since these different memory blocks aren't connected any modifications aren't communicated.
In pass-by-reference a variables value is only ever stored in one memory location so any changes made have to affect every variable with said value.
In what I'm calling Ruby's pass-by-value-reference a value is only ever stored in one memory location but different variables have different nicknames for it. 
Even though those nicknames differ since the overall value in memory they refer to is the same any changes made to that value on one variable affect all variables.
The exception to this rule and the solution I ended up using to solve my problem was the dup method.
This method creates a copy of a variables value(s) but not the object(s) they refer to.
Dup does this by creating a new copy of the object the original variable references and giving the new object the same values.
The end result is an identical object at a different location in memory so I was free to simulate board moves without consequence to the original.

