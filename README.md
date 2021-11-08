# Toodle-O!

Plain text todo manager

![icon](./toodle-o.png)

Plain text is simple, easily created, easy to understand, and infinitely portable. It’s also dead simple to write tools for and cut and slice anywhichway you need.

## Effective Todo List Format

1. Every Todo item starts with a special character (`[]`, `*`, `-`, `+`, or `#`)
2. A ‘completed’ Todo can be deleted or marked with a starting `x`.
3. You can add tags `:tag1`, `:tag2` to any Todo.
4. Use the special tag `:later`  to mark Todo’s to be done later.
5. Todo’s  can be indented to make for easier entry/reading. Indented Todo’s inherit the tags of it’s ‘parent’ Todo.
6. Lines that don’t start with any todo markers are considered supporting notes or rough scribbles. Notes are associated with the previous todo item.

## Example

```
* Write a todo list
* Buy Eggs :shopping :joes
* Butter :shopping
* Cheese :shopping
* Release Toodle-O :toodle-o
x* Write Readme :toodle-o
* Implement :toodle-o
	* Write Parser
	* Write Command-Line Interface
* :supermarket
	* Pencils
	* Chicken
* :toodle-o
Write toodle-o's command line in python because it's pretty ideal for little utilites like this.
At some point port it to the web?
	* web-version :later:
```

## Setup

The `toodle-o` command-line script will first look for a `todo.txt` file in the current directory. Failing that, it will look for a `todo.txt` in your HOME directory.

You can also provide a `toodle-o.list` file which contains, one on each line, a list of `todo` files scattered across various directories.

## Usage

Let’s link our `toodle-o` command-line script to the short form `tt` for easy typing in the examples below. To add a new Todo, start with a `+`:

```sh
$> tt + add a new todo :project
$> tt + :shopping bread
```

If we provide a tag it will show us the list for those particular tags (without completed (`x`) and `:later` items).

```sh
$> tt -s :shopping
Buy Eggs
Butter
Cheese
Bread
$> tt -s :toodle-o
Release Toodle-O
Implement Toodle-O
	Write Parser
	Write Command-Line Interface
```

The nested elements are indented using tabs so they can be easily piped for further processing if you only want the top level etc.

We can see more details (including `later` and `done` entries along with the file name) with the verbose tag:

```sh
$> tt -v :shopping :supermarket
TODO	(shopping,joes)	Buy Eggs
TODO	(shopping)	Butter
TODO	(shopping)	Cheese
TODO	(supermarket)	Pencils
TODO	(supermarket)	Chicken
TODO	(shopping)	Bread
TODO	(shopping)	Bacon
TODO	(supermarket)	Rice

/my/shopping/list.txt
/my/todo/list.txt

$> tt -v :toodle-o
TODO	(toodle-o)	Release Toodle-O
DONE	(toodle-o)	Write Readme
TODO	(toodle-o)	Implement Toodle-O
TODO	(toodle-o)		Write Parser
TODO	(toodle-o)		Write Command-Line Interface
NOTE	(toodle-o)	Write toodle-o's command line in python because it's pretty ideal for little utilites like this.
NOTE	(toodle-o)	At some point port it to the web?
LATR	(toodle-o)	Web Version

/my/projects/toodle-o/todo.txt
```

To see everything:

```sh
$> tt -v
```

And to find items that do not have any tags:

```sh
$> tt -s :
Write a todo list
```

You can also just search for any matching word:

```sh
$> tt -s eggs
Buy Eggs
```

To get the list of tags:

```sh
$> tt -t
:shopping
:supermarket
:toodle-o
```

To mark matching items as completed:

```sh
$> tt -x :shopping eggs
x Buy Eggs
```



----

Enjoy