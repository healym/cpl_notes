Lecture 2 - Python
==================

version
-using 3.5.2
- on lab boxes
- diff 2<->3
- unicode support
- backward incompatible changes to syntax and default libraries

quick facts
-----------

+ comments - lines start with #

+ print()
	- prints a value to console over stdout
	- same as cout

declare and assign in a single step
	x = 5, **not** int x; x = 5;

no compile step

Types
-----

Numbers
	Int (Integer) - 5,6,7,etc
	Float (Floating point) - 5.6

Boolean
	True
	False

str - String
	single or double quotes
		"frog", 'frog'
		'',""
		"frog's leg" <-- double quotes good for apostrophe
	Iterable
	**no** character type, just single-char strings

None
	None

Built-in Data Structures
------------------------

List (list)

	Iterable
	Mutable sequence of elements
		x=[1]
		x.append(2) -- x==[1,2]

	Elements may be of differing types
	Ex:
		[1,2,3]
		[1,2,3,"frog"]
		[]

	Indexing
		begins at 0
		index must be an Int

	slices
		x[0:2] [included(0):**excluded**]
		returns a **shallow** copy
		start copying at the first slice index
		stop before end
		x[3:1] --[], needs other parameter to step backwards
		x[3:3] --[], evaluation stops before including first element

	Negative indexing
		counts from end of list
		x[-1] --last element


Tuple (tuple)

	Iterable
	immutable sequence of elements
	elements *can* have different types
	(x,) -- comma **required**
	() -- valid tuple, for some reason
	tuples can contain other tuples
	lists in tuples can be modified

	slicing
		works the same as a list

	Negative indexing


Dictionary (dict)
	heavily abused

	Iterable(key by default)

	maps keys to values
		both keys and values can vary in type

	_**not**_ a sequence
		cannot depend on keys in any order

	examples:
		x={'a':'frog','b':'giraffe','c':'apple'}
		x['a'] -- "frog"
		x['nope'] -- KeyError


Custom Types

	they exist
	Python has class-based objects


Assignment
----------

	Variables are _dynamically_ typed
		It'll let you do this
		It'll work
			Until it doesn't.


Unpacking
---------

	multiple assignments on one line
	ex
		(a,b) = (1,2)
		a,b = 1,2
		a,b = [1,2]
		a,b = b,a

	numbers need to match
		a,b,c = 1,2 --PROBLEM
