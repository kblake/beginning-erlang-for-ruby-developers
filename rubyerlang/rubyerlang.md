!SLIDE incremental bullets

# Learning Erlang through Ruby

* Look at Ruby code and then try to compare to a similar piece of code in Erlang. 
* Not all code can be a perfect match or fit. 
* This will allow you to use existing knowledge to better learn Erlang.

!SLIDE incremental commandline

#Shell

<br /><br />
<br /><br />


	$ irb		
		
	>> 1 + 1
	2

	$ erl

	Eshell V5.8  (abort with ^G)
	1> 1 + 1.
	2


!SLIDE

#Variables in Ruby

	@@@ ruby
	x = 10
	x = "john"
	x = 3.14


!SLIDE bullets

#Variables in Erlang

	@@@ ruby
	X = 10. 
	Y = "john".
	Z = 3.14.
	X = 4.

<br /><br />
** exception error: no match of right hand side value 4

Huh?

!SLIDE bullets incremental

#Pattern matching

* = looks like an assignment operator but 
* it is really a pattern matching operator
* X is unbound
* X = 10 is bound
* can only bind a variable once


!SLIDE

#Pattern matching

	@@@ ruby
	X.
	variable X is unbound

	X = 2 + 4.
	X = 6.
	X = 3 + 3.
	X = 6 + 0.
	X = 5 + 1.
	X = 6 * 1.


!SLIDE

#Ruby Symbol

	@@@ ruby
	temp = :hot
	age = :old

!SLIDE

#Erlang Atom

##Non numeric constant value<br />
##Start with lower case letter<br /><br />

	@@@ ruby
	Temp = hot.
	Age = old.
	

!SLIDE

#Ruby Struct or Hash

	@@@ ruby
	Customer = Struct.new(:name, :age)
	c = Customer.new("john", 99)

	customer = {:name => "John", :age => 99}

!SLIDE

#Erlang Tuple

##Convention is to use a meaningful atom that represents the data that follows<br /><br />


	@@@ ruby
	Person = {person, {name, "john"}, {age, 99}}.

!SLIDE

#More Pattern Matching

	@@@ruby
	%extracting values out of a tuple

	Point = {point, 10, 45}.
	{point, X, Y} = Point.
	
	%10 is bound to X
	%45 is bound to Y
	%point, well is just a point
	

!SLIDE

#Ruby Array

	@@@ ruby
	numbers = [1, 2, 3]
	information = ["john", 99, :blue]
	
!SLIDE

#Erlang List

	@@@ ruby
	Numbers = [1, 2, 3].
	Information = ["john", 99, blue].
	ShoppingList = [{bananas, 10}, {milk, 2}].

!SLIDE bullets incremental

#Getting values out of a list

* **head** is the first item in the list
* **tail** is the rest of the list

!SLIDE bullets incremental

#Getting values out of a list

	@@@ruby
	Nums = [1,2,3,4,5]
	[Head|Tail] = Nums.
	% Head has the value of 1
	% Tail has the rest	[2,3,4,5]

	[Head2|Tail2] = Tail.
	% Head2 has the value of 2
	% Tail2 has the rest [3,4,5]

	
!SLIDE smaller

#Methods

	@@@ruby
	class Geometry
  		def self.area(shape, options = {})
    		return options[:base] * options[:height] if shape == :rectangle
    		return 3.14 * options[:radius]**2 if shape == :circle
    		(options[:base] * options[:height])/2 if shape == :triangle
  		end
	end

	#call the code elsewhere

	Geometry.area(:rectangle, {:base => 4, :height => 5})
	Geometry.area(:circle, {:radius => 4})
	Geometry.area(:triangle, {:base => 4, :height => 5})


!SLIDE smaller

#Functions

	@@@ruby
	-module(geometry).
	-export([area/1]).

	area({rectangle, Base, Height}) -> Base * Height;
	area({circle, Radius}) -> 3.14 * Radius * Radius;
	area({triangle, Base, Height}) -> area({rectangle, Base, Height})/2.

	%call the code elsewhere

	geometry:area({rectangle, 4, 5}).
	geometry:area({circle, 4}).
	geometry:area({triangle, 4, 5}).

!SLIDE incremental bullets

#Calling the correct clause

* no conditionals
* pattern match arguments

!SLIDE center

![functions pattern matching](functions-pattern-matching.jpg)

!SLIDE center

![functions pattern matching](circle-match.jpg)


!SLIDE center

![functions pattern matching](triangle-match.jpg)


!SLIDE

#Ruby Anonymous functions

	@@@ruby
	triple = lambda{|x| 3 * x}
	triple.call(10)
	triple[10]

	upit = lambda do |by_what, num| 
  		return num * 2 if by_what == "double"
  		return num * 3 if by_what == "triple"
	end

	upit.call("double", 10)
	upit.call("triple", 10)


!SLIDE smaller

#Erlang Anonymous functions

<br /><br />

	@@@ruby
	Triple = fun(X) -> 3 * X end.
	Triple(10).
	
	UpIt = fun({double, Num}) -> 2 * Num; ({triple, Num}) -> 3 * Num end.
	Upit({double, 10}).
	UpIt({triple, 10}).

	%more pattern matching

!SLIDE smaller

#Ruby Map/Collect

<br /><br />

	@@@ruby
	numbers = [1,2,3,4,5]
	numbers.map{|number| number * 2}

!SLIDE smaller

#Erlang Map and List Comprehension

<br /><br />

	@@@ruby
	Numbers = [1,2,3,4,5].

	%Built-in Function (BIF)
	lists:map(fun(Number) -> Number * 2 end, Numbers).

	%Use list comprehension
	[2 * Number || Number <- Numbers].
