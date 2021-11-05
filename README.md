# Toodle-O!

Plain text todo manager

![icon](./toodle-o.png)

Plain text is simple, easily created, easy to understand, and infinitely portable. It’s also dead simple to write tools for and cut and slice anywhichway you need.

## Effective Todo List Format

1. Every Todo item starts with a special character (`[]`, `*`, `-`, `+`, or `#`)
2. A ‘completed’ Todo can be deleted or marked with a starting `x`.
3. You can add tags `:xxx` to any Todo.
4. You can add multiple tags to any item like this: `:tag1 :tag2`. 
5. You can associate tags by adding them together like this: `:tag1+tag2`. Now `tag1` and `tag2` are considered ‘linked’ - searching for one will search for the other as well.
6. The special tag `:later:` is used to mark Todo’s to be done later.
7. Lines that don’t start with any todo markers are considered supporting notes or rough scribbles. They are associated with the previous todo item found.
8. Indented Todo’s are associated with the previous outdented Todo and inherit all it’s tags.

## Example

```
* Write a todo list
* Buy Eggs :shopping :supermarket
* Butter :supermarket+shopping
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

You can provide a `toodle-o.list` file which contains, one on each line, a list of `todo` files scattered across various directories.

If no such file is found, we default to `todo.txt`.

## Usage

Let’s link our `toodle-o` command-line script to the short form `tt` for easy typing in the examples below. To add a new Todo, start with a `+`:

```sh
$> tt + add a new todo :project
$> tt + :shopping bread
```

If we provide a tag it will show us the list for that particular tag and all associated tags (without completed (`x`) and `:later:` items).

```sh
$> tt :shopping
Buy Eggs
Butter
Cheese
Pencils
Chicken
Bread
$> tt :toodle-o
Release Toodle-O
Implement Toodle-O
	Write Parser
	Write Command-Line Interface
```

The nested elements are indented using tabs so they can be easily piped for further processing if you only want the top level etc.

We can see more details (including `later` and `done` entries along with the file name) with the verbose tag:

```sh
$> tt -v :toodle-o
    	Release Toodle-O (toodle-o)
DONE	Write Readme (toodle-o)
    	Implement Toodle-O (toodle-o)
     		Write Parser (toodle-o)
     		Write Command-Line Interface (toodle-o)
    	Write toodle-o's command line in python because it's pretty ideal for little utilites like this.
    	At some point port it to the web?
LATER	Web Version (toodle-o)

/my/projects/toodle-o/todo.txt
$> tt -v :shopping
    	Buy Eggs (shopping,supermarket)
    	Butter (supermarket+shopping)
    	Cheese (shopping)
    	Pencils (supermarket)
    	Chicken (supermarket)
    	Bread (shopping)
    	Bacon (shopping)
    	Rice (supermarket)

/my/shopping/list.txt
/my/todo/list.txt
```

If you want not have any associated items, use the `:tag:` form to search:

```sh
$>tt :shopping:
Eggs
Butter
Cheese
Bread
```

And to find items without any tags:

```sh
$> tt :
Write a todo list
```

To get the list of tags:

```sh
$> tt -t
:shopping
:supermarket
:supermarket+shopping
:toodle-o
```

To mark matching items as completed:

```sh
$> tt -x :shopping eggs
x Eggs
```



----

Enjoy