things should be named well, because things are everywhere: variables, functions, arguments, classes, packages, files, directories, etc. all of them should be named well.

names should reveal intent, seriously, and that may take time. the name of a variable, function or class should answer these questions:
1. why does it exist;
2. what does it do;
3. how it is used;

if a name requires a comment, then it is not revealing its intent.

what is the purpose of this code?
```
public List<int[]> getThem() {
	List<int[]> list1 = new ArrayList<int[]>();
	for (int[] x : theList)
		if (x[0] == 4)
			list1.add(x);
	return list1;
}
```
it is well indented, it has no complex logics and yet you can't tell a single thing about this code when reading it. many questions arise upon it: what is the code supposed to `get`? what is `list1`? what objects are in `theList`? why is number `4` such an important number?

when writing code, simplicity may not always be the problem, but the implicity of it. the example above does not explicit context enough in the code itself, meaning its purpose is implicit to whom have written it.

maybe if we had enough context to tell this code belongs to a mine sweeper game, we could find out that the board is a list of cells called `theList`. we could rename it to `gameBoard` and achieve something more explicit and readable:

```
public List<int[]> getFlaggedCells() {
	List<int[]> flaggedCells = new ArrayList<int[]>();
	for (int[] cell : gameBoard)
		if (cell[STATUS_VALUE] == FLAGGED)
			flaggedCells.add(cell);
	return flaggedCells;
}
```

much better, and just simple name changes were made. no logic altered.

disinformation is another big enemy when naming things, the rule to avoid disinformation is to avoid words whose hidden meaning vary from the intended meaning. let's say we have a group of `Account` and we want to name it. we could say:

`Group<Account> accountList = new Group<Account>()`

well, that's disinformation. our group of `Account` is not a list and yet we are naming it as if it was. so `accountGroup` or just `accounts` would be better.

using names which vary in small ways is a dangerous habit too. a developer may take long to tell the difference between `StorageControllerForHandlingAbstractUserTransactions` and `StorageControllerForHandlingAbstractAdminTransactions`. nowadays the developer is likely to pick an object by pressing tab to auto complete without checking it twice or seeing your copious comments or even the list of methods supplied by each class.

sometimes, the compiler or interpreter may not let you name two different things with the same value. then, to satisfy it, you make a little change to one of these things. e.g.: `document` and `dokument`, simply because you couldn't create two `document` objects. well, that only make your code more confuse and meaningless.

noise words are another meaningless distinction. Imagine that you have a `Product`
class. if you have another called `ProductInfo` or `ProductData`, you have made the names different without making them mean anything different. `Info` and `Data` are indistinct noise words.

noise words are redundant. the word `variable` should never appear in a variable
name. the word `table` should never appear in a table name. how is `NameString` better than `Name`? would a name ever be a floating point number? If so, it breaks an earlier rule about disinformation.

programming is a social activity. when naming things, it should be not only meaningful but also readable. if something is not readable then it means other people can't read it properly and discuss it, thus failing on what programming is: a social activity.
```
class DtaRcrd102 {
	private Date genymdhms;
	private Date modymdhms;
	private final String pszqint = "102";
	/* ... */
};

to

class Customer {
	private Date generationTimestamp;
	private Date modificationTimestamp;;
	private final String recordId = "102";
	/* ... */
};
```

now people could read it and rise questions like: "hey, how come is the modification time stamp older than its generation stamp?". single letter names also fail on that since its pretty hard not only to spell but to search for a variable `gts` instead of `generationTimeStamp`.

if a variable or constant is used multiple times across code, then give it a search-friendly name.

when talking about interfaces and implementations, the author points that an interface name should not be encoded, but its implementation instead. e.g.: we'll build a factory for the creation of shapes. this factory will be an interface and it will be implemented by a concrete class. instead of calling the factory `IShapeFactory`, leave this encoding (prefixing `I` on it) to the implementation.

so, instead of encoding the factory, just name it `ShapeFactory` and then name the implementation something like `ShapeFactoryImplementation : ShapeFactory`.

**clarity is king**: classes and objects should have noun or noun phrase names like `Customer`, `Account` and `AddressParser`. a class should not be a verb, like `Parser`, `Processor` or `Shifter`. in the other hand, methods should have verb: `deletePage`, `retrieveAccountTransaction`, `setName` and similar are ok for method naming.

don't name things just to be cute or funny. don't write a method to clean up some object and name it after `whack()`, other people may not share the same sense of humor as you.  instead, just name it `kill()` or `cleanObject()`.

also, avoid using the same word for two purposes. using the same term for two different ideas may be considered as a pun for other developers, and they may not laugh off it.

say what you mean. mean what you say.

choosing one word per concept and sticking with it is also a good practice on naming things. instead of having different methods for different classes with `get`, `fetch` and `retrieve`, choose one and stick with throughout the entire codebase.

this avoids questions like "what class the `fetchDevice()` method belongs to and what class the `getDevice()` method belongs to?". choose one and stick with it.

one important thing to remember is that the people who read your code *will be programmers*. so making use of computer science terms, algorithm names, pattern names, math terms is completely fine.

when there is no “programmer-eese” for what you’re doing, use the name from the problem domain. at least the programmer who maintains your code can ask a domain expert what it means.

separating solution and problem domain concepts is part of the job of a good programmer and designer. the code that has more to do with problem domain concepts
should have names drawn from the problem domain.

Imagine that you have variables named `firstName`, `lastName`, `street`, `houseNumber`, `city`, `state`, and `zipcode`. taken together it’s pretty clear that they form an address. but what if you just saw the state variable being used alone in a method? would you automatically infer that it was part of an address?

you can add context by using prefixes: `addrFirstName`, `addrLastName`, `addrState`, and so on. at least readers will understand that these variables are part of a larger structure. of course, a better solution is to create a class named `Address`. then, even the compiler knows that the variables belong to a bigger concept.

last but not least, having fear of renaming things is something we can't have. fearing that other developers will object in renaming things will not be a concern when names change for the better.

you will probably end up surprising someone when you rename, just like you might with any other code improvement. don't let this fear stop you in your tracks.