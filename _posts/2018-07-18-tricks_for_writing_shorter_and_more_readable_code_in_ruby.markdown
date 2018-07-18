---
layout: post
title:      "Tricks For Writing Shorter And More Readable Code In Ruby"
date:       2018-07-18 19:20:18 +0000
permalink:  tricks_for_writing_shorter_and_more_readable_code_in_ruby
---


<p>Consider the following code example.</p>

```
def winner
	 combo = won?

		if combo
			board.cells[  combo[0]  ] 
		end
end
```

<p> While the Tic Tac Toe program's code this snippet was taken from isn't included, the imporant part is that we have such a short IF statement condition and variable declaration that make it feel as though we've wasted lines. For simple methods like this I think its best to make them into a single line of code that reads like a sentence. At this point you may be thinking "I bet he's just going to use a single line IF statement, this is not helpful". While that would be shorter it would arguably make the code less readable.​</p>

```
def winner
	 if combo = won? then board.cells[ combo[0] ] end
end
```

<p> The IF-THEN statement is an alternative to the single line IF statement that doesn't get used enough. The refactored example above uses that in addition to setting a variable in the IF statement's condition to make it both shorter and more readable. </p>

<p> Here's another example of a refactor opportunity. </p>

```
def play
    turn until over?
    
		if winner
		  puts "Congratulations #{winner}!" 
		else
		  puts "Cat's Game!"
		end
end
```

<p> The IF statement at the bottom of the play method above is going to puts a phrase no matter what and the logic is so simple that its needlessly long. By combining the ternary operator and the fact that puts knows how to process a methods return value you can shorten the method into just this. </p>

```
  def play
    turn until over?
    puts winner ? "Congratulations #{winner}!" : "Cat's Game!"
end
```

<p> Here again we both save lines and make the method more readable. </p>

<p> What about this example, is there any way to apply a similar approach to simplify (spoiler yes)? </p>

```
def set_enemy_token
  if @player_token == 'O'
	  @enemy_token = 'X'
	else 
	  @enemy_token = 'O'
	end
end
```

<p> Like the previous example by using the ternary operator and Ruby's very kind handling of return values we can turn this entire method into one line. </p>

```
def set_enemy_token
  @enemy_token = @player_token == 'O' ? 'X' : 'O'
end
```

<p> While you're writing code its easy to get stuck in a pattern like turning everything into long IF statements. There's not necessarily anything wrong with that as simple conditionals are an essential part of any program or language, but it will rob you of the opportunity to practice other methods and to expand your knowledge of a languages syntax.​</p>



