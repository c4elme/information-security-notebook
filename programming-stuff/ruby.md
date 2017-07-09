"!" - will apply the effect of the method to variable itself.

var.to\_i- will convert 'var' to Integer

ARGV \(ARGV.first, ARGV.second .. and so on\)- "argument variable" - This variable holds the arguments you pass to your Ruby script when you run it.

`$stdin.gets.chomp` - use this if there's an ARGV.

"Defining a functon"

`function(*args)`- if you  are not sure how many arguments that you will be passing



def &lt;function name&gt;\(&lt;parameter&gt;\) 

\#do something

end



multiple\_line\_string = &lt;&lt;END

\tThelovely world

with logic so firmly planted

cannot discern \n the needs of love

nor comprehend passion from intuition

and requires an explanation

\n\t\twherethere is none.

END



filemanipulatuionmethods



&gt; .open\(f,a\)

&gt; .read

&gt; .write\(f\)



== CONTROL FLOW ==

\#Sample Codes

\#if 

if 10 &gt; 20

\#prints false

end



\#ifelsif

if 10 &gt; 20

\#prints false

elsif 10 &lt; 20

\#prints true

end



if 10 &gt; 20

\#prints false

else

\#10 will be never be greater than 20

end



\#for

for number in 1..10

puts number \#will print 1 - 10

end



\#while

while true

puts "infinite loop"

end



\#Sample Code

\#This will change all the letter 's' to "th"



print "Thtring,pleathe!: "

user\_input = gets.chomp

user\_input.downcase!



if user\_input.include? "s"

  user\_input.gsub!\(/s/, "th"\)

else

  puts "Nothing to do here!"

end



puts "Your string is: \#{user\_input}"



== CODE BLOCKS == 



\# The block, {\|i\| putsi}, is passed the current

\# array item each time it is evaluated. This block

\# prints the item. 

\[1, 2, 3, 4, 5\].each { \|i\| putsi}



\# This block prints the number 5 for each item.

\# \(It chooses to ignore the passed item, which is allowed.\)

\[1, 2, 3, 4, 5\].each { \|i\| putsi\*5 }



== SORTING ==



Method/s

.sort

.reverse

Example of Sorting



\#will sort fruits to descending order



fruits = \["orange", "apple", "banana", "pear", "grapes"\]



fruits.sort! do \|firstFruit,secondFruit\| 

secondFruit&lt;=&gt;firstFruit

end



def alphabetize\(arr, rev=false\)

    arr.sort!

    if rev

        arr.reverse!

    else

        arr

    end

end

numbers = \[7,5,8,6,4,1,3,2\]

puts alphabetize\(numbers\)





== The Combined Comparison Operator ==



The combined comparison operator to compare two Ruby objects. \(&lt;=&gt;\)

0 = first &gt; second

1 = first &lt; second

-1 = first == second



== Iterators == 



.each

\#each

\(1..10\).each do \|count\|

puts count

End



times {\|i\| block }→self



times→an\_enumerator

Iterates the given block int times, passing in values from zero to int - 1.



If no block is given, an [Enumerator](http://ruby-doc.org/core-2.2.2/Enumerator.html) is returned instead.

5.timesdo\|i\|  
printi, " "  
end  
\#=&gt; 0 1 2 3 4





== HASHES==

Hashes are just collections of key-value pairs, where a unique key is associated with some value.

Example: 



breakfast = { "bacon" =&gt; "tasty",  
  "eggs" =&gt; "tasty",  
  "oatmeal" =&gt; "healthy",  
  "OJ" =&gt; "juicy"  
}



We can create hashes several ways, but two of the most popular are hash literal notation:

new\_hash = {"one"=&gt;1}  


and hash constructor notation:

new\_hash = Hash.new



It's important to realize that falseandnil are not the samething:false means "not true," while nil is Ruby's way of saying "nothing at all."



Accessing Hash



hash\[key\]



Ex:

new\_hash\['one'\]



You don't have to settle for nil as a default value, however. If you create your hash using the Hash.new syntax, you can specify a default like so:

my\_hash = Hash.new\("Trady Blix"\)  


Now if you try to access a nonexistent key in my\_hash, you'll get "Trady Blix"as a result.

== Symbols ==

What's a Symbol?

You can think of a Ruby symbol as a sort of name. It's important to remember that symbols aren'tstrings:

"string"== :string\# false  




Above and beyond the different syntax, there's a key behavior of symbols that makes them different from strings: while there can be multiple different strings that all have the same value, there's only onecopyofany particular symbol at a given time.

Symbol Syntax

Symbols always start with a colon \(:\). They must be valid Ruby variable names, so the first character after the colon has to be a letter or underscore \(\_\); after that, any combination of letters, numbers, and underscores is allowed.

What are Symbols Used For?

Symbols pop up in a lot of places in Ruby, but they're primarily used either as hash keys or for referencing method names. \(We'll see how symbols can reference methods in a later lesson.\)

sounds= {  
:cat=&gt;"meow",  
:dog=&gt;"woof",  
:computer=&gt;10010110,  
}  


Symbols make good hash keys for a few reasons:

1. They're immutable, meaning they can't be changed once they're created;

2. Only one copy of any symbol exists at a given time, so they save memory;

3. Symbol-as-keys are faster than strings-as-keys because of the above two reasons.

Converting Between Symbols and Strings

Converting between strings and symbols is a snap.

:sasquatch.to\_s  
\# ==&gt; "sasquatch"  


"sasquatch".to\_sym  
\# ==&gt; :sasquatch  


The .to\_s and .to\_sym methods are what you're looking for!



Exercise Code



strings = \["HTML", "CSS", "JavaScript", "Python", "Ruby"\]



\# Add your code below!

symbols = \[\]



strings.eachdo \|lang\|

s = lang.to\_sym

     symbols.push\(s.intern\)

end



\#USE OF INTERN

strings = \["HTML", "CSS", "JavaScript", "Python", "Ruby"\]



\# Add your code below!

symbols = \[\]



strings.eachdo \|lang\|

s = lang.intern

     symbols.push\(s\)

end



The Hash Rocket Has Landed

However, the hash syntax has changed in Ruby 1.9. Just when you were getting comfortable!



The good news is that the new syntax is easier to type than the old hash rocket syntax, and if you're used to JavaScript objects or Python dictionaries, it will look very familiar:



new\_hash = { one: 1,

  two: 2,

  three: 3

}



The two changes are:



You put the colon at the end of the symbol, not at the beginning;

You don't need the hash rocket anymore.

It's important to note that even though these keys have colons at the end instead of the beginning, they're still symbols!



puts new\_hash

\# ==&gt; {:one=&gt;1, :two=&gt;2, :three=&gt;3}



From now on, we'll use the new 1.9 hash syntax when giving examples or providing default code. You'll want to be familiar with the hash rocket style when reading other people's code, which might be older.



Code:

movies = {

    double007: "WOW",

forrest\_gump: "WOW"

}



Becoming More Selective

We know how to grab a specific value from a hash by specifying the associated key, but what if we want to filter a hash for values that meet certain criteria? For that, we can useselect.

grades= {alice:100,  
bob:92,  
chris:95,  
dave:97  
}  


grades.select{\|name,grade\|grade&lt;97}  
\# ==&gt; {:bob=&gt;92, :chris=&gt;95}  


grades.select{ \|k,v\|k==:alice}  
\# ==&gt; {:alice=&gt;100}



Exercise Code



movie\_ratings = {

  memento: 3,

  primer: 3.5,

  the\_matrix: 5,

truman\_show: 4,

  red\_dawn: 1.5,

  skyfall: 4,

alex\_cross: 2,

  uhf: 1,

  lion\_king: 3.5

}

\# Add your code below!



good\_movies = movie\_ratings.select {\|name, rating\| rating &gt; 3}



Ruby includes two hash methods,.each\_key and .each\_value, that do exactly what you'd expect:

my\_hash= {one:1,two:2,three:3}  


my\_hash.each\_key{ \|k\|printk," "}  
\# ==&gt; one two three  


my\_hash.each\_value{ \|v\|printv," "}  
\# ==&gt; 1 2 3  


Let's wrap up our study of Ruby hashes and symbols by testing these methods out.

Code Sample

movie\_ratings = {

  memento: 3,

  primer: 3.5,

  the\_matrix: 3,

truman\_show: 4,

  red\_dawn: 1.5,

  skyfall: 4,

alex\_cross: 2,

  uhf: 1,

  lion\_king: 3.5

}

\# Add your code below!

movie\_ratings.each\_key {\|k\| puts k}



The Case Statement

Good work! Now we'll want to create the main body of our program:thecase statement, which will decide what actions to take based on what the user types in.

if and else are powerful, but we can get bogged down in ifs and elsifsif we have a lot of conditions to check. Thankfully, Ruby provides us with a concise alternative: the casestatement. The syntax looks like this:

caselanguage  
when"JS"  
puts"Websites!"  
when"Python"  
puts"Science!"  
when"Ruby"  
puts"Web apps!"  
else  
puts"I don't know!"  
end





A Night at the Movies \| Exercise Code:



movies = {

forrestgump:  4,

cloverfield:  4,

themartian: 4

}

puts "Choices: "

puts "-- ADD"

puts "-- UPDATE"

puts "-- DISPLAY"

puts "-- DELETE"



puts "Please enter your choice: "

choice = gets.chomp



case choice

    when "add"

        \# puts "Added!"

        puts "Please Enter the Movie title: "

        title = gets.chomp

        puts "What is your rating?: "

        rating = gets.chomp

        if movies\[title.to\_sym\].nil?

            movies\[title.to\_sym\] = rating.to\_i

            puts "New pair was added"

        else

            puts "Movie already exists."

        end

    when "update"

        \# puts "Updated!"

        puts "Please enter the movie title: "

        title = gets.chomp



        if movies\[title.to\_sym\].nil?

            puts "Movie does not exist."

        else

            puts "Enter the new rating: "

            rating = gets.chomp

            movies\[title.to\_sym\] = rating.to\_i

        end

    when "display"

        \# puts "Movies!"

movies.eachdo \|movie, rating\|

            puts "\#{movie}: \#{rating}"

        end

    when "delete"

        \# puts "Deleted!"

        puts "Please enter the title you want to delete: "

        title = gets.chomp



        if movies\[title.to\_sym\].nil?

            puts "Movie does no exist!"

        else

            movies.delete\(title.to\_sym\)

            \# puts "Deleted!"

        end

    else

        puts "Error!"

end



Ternary Condition



boolean ? "if true" : "if false"



When and Then: The Case Statement

The if/else statement is powerful, but we can get bogged down in ifs andelsifsif we have a lot of conditions to check. Thankfully, Ruby provides us with a concise alternative: the case statement. The syntax looks like this:



case language  
when "JS"  
  puts "Websites!"  
when "Python"  
  puts "Science!"  
when "Ruby"  
  puts "Web apps!"  
else  
  puts "I don't know!"  
end  


But you can fold it up like so:



case language  
  when "JS" then puts "Websites!"  
  when "Python" then puts "Science!"  
  when "Ruby" then puts "Web apps!"  
  else puts "I don't know!"  
end

