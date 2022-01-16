{% capture prereqs %}
* A UNIX shell installed (either macOS, Linux, or WSL)
{% endcapture %}
{% capture goals %}
* Become framiliar with the UNIX command line
* Learn how to use the version management system git.
{% endcapture %}
{% capture seealso %}
_None_
{% endcapture %}

# Getting started with git
Git is a popular version control system used by software engineers around the world. It's primary purpose is to maintain different versions of files, and to allow multiple engineers to work on the same thing at once.

Git was created by [Linus Torvalds](https://en.wikipedia.org/wiki/Linus_Torvalds), who was the main author of the [Linux Kernel](https://en.wikipedia.org/wiki/Linux_Kernel), the base of many modern operating systems (including every linux distribution, and Andorid). When he was working on the kernel with others, he ran into issues with collaboration (think emailing code back and forth). He wrote git as a solution.

{% include lesson-header.md prereqs=prereqs goals=goals seealso=seealso %}

## An introduction to the command line
Git is a program, the same way that Firefox or Word is, but there is a catch. Firefox and Word both provide graphical user interfaces (GUIs). We have a window where we can click buttons or type into text boxes. Git is run from the command line, and provides only a text interface. You type a text command to git, and it gives you back text.

To use a program like this, you need to learn how to control your computer with text.

* **On macOS:** open the "Terminal" app
* **On Linux:** open the terminal emulator for your distribution
* **On Windows:** open the Linux distribution that you installed when you installed WSL.

Once you've opened your terminal, you'll get a _shell_, a special type of program that allows you to control your operating system. It's okay if that doesn't make sense, it's not very important in what we're doing. (and you can learn more about it in [CS4410](https://classes.cornell.edu/browse/roster/SP22/class/CS/4410)).

You should get something that looks vaguely like this (but with your name, and your computer's name):

```
williambarkoff@willsmacbookpro ~ %
```

The is called a _prompt_, because it's prompting you to type something. We won't go into what each of the parts of the prompt mean, because it varies greatly depending on your configuration.

There is one part of it that is pretty important, and that's the last character. It's usually `$` or `%`. When you see that, it means that the shell is ready for your next command.

Let's try typing a command. After the prompt, type:

```sh
echo "hello world"
```
When you're finished, press enter. The computer should say something back!

<small>Pstt! When you see a little triangle like this, click it to show more!</small>

{% spoiler "Reveal" %}
```sh
williambarkoff@willsmacbookpro ~ % echo "hello world"
hello world
```
{% include help-i-didnt-get-that.md %}
{% endspoiler %}

Cool! Let's disect that! Your command had a few parts.
* First, you typed `echo`. This is the name of the program you're runnning. Everything you type between the name of the program and when you press enter are parameters passed to the program.
* You passed the parameter `"hello world"` to the program, `echo`

Echo is one of the simplest programs on your computer. To find out what it does, we can use another program, `man`, short for `manual`. To learn about `echo`, we can read the manual for it. Type `man echo`, and press enter.

You should get a page that teaches you how to use `echo`. You can use the up and down arrow keys to scroll the document to learn about `echo`.

Echo takes in what ever you give it, and just repeats it back to you, similar to the [echo](https://en.wikipedia.org/wiki/Echo) you would hear in a cave.

There are a bunch of other important commands, so let's run through them, but first, let's talk about how your computer is organized. You might be used to a structure that looks similar to this:

<div class="text-center">
<div style="max-width: 800px">
<img alt="A screenshot showing a file explorer window open" src="/img/intro-git/directory-example.png">
</div>
</div>

Notice how we have two fundamental structures, _files_ and _folders_. Files are our base unit, and folders contain more files and folders. When discussing the command line, we call folders _directories_. Let's talk about how to navigate through different directories via the command line.

Whne you open the command line, you generally start in your _home directory_, denoted `~` (there are a few exceptions). Let's see what files we have in our home directory. We can do this with `ls`. Try typing `ls` at the prompt.

{% spoiler "Reveal" %}

You should get something that looks like this:
```sh
williambarkoff@willsmacbookpro ~ % ls
Applications  IdeaProjects  OneDrive      bin           Desktop
Library       Pictures      certs         go            Documents
Movies        Public        Downloads     Music         
```

The names of the directories might be different, and you might have more or less files, and they might be different colors, but none of that _really_ matters.

{% include help-i-didnt-get-that.md %}
{% endspoiler %}

`ls` is short for "list" becuase it lists the contents of a directory. I reccomend checking out the man page for `ls` at some point, because there are a lot of important options. Notably, `ls -l` will use the "long" format and show more information, `ls -s` will show the size of each file, and `ls -a` will show hidden files.

Arguments that start with `-` or `--` are usally called _flags_, and are a special type of argument that changes a setting for the command. Usually you can combine single character flags, so if you want to use `ls` with the `-l`, `-a`, and `-s` flags, you can type `ls -las`.

### Make a directory

Let's make a new directory to work in for the remainder of this chapter. We'll call it `intro-git`. To do this, we'll use a new command, called `mkdir`, short for "make directory."

After the prompt, type:
```sh
mkdir intro-git
```

And.... nothing happens. But that's okay! that means that our directory was created!

{% include help-i-didnt-get-that.md %}

Now list the contents of the current directory again with `ls`. You should now see a shiny new directory, `intro-git`.

### Enter a directory
Now, let's enter the directory that we just created. To do that, we can use `cd`, short for "change directory." To change into our new directory, we type `cd intro-git`.

There are a few important things to note. Remember how earlier I said that `~` refers to your home directory? There are a few other special things like this!

* `/` (forward slash) refers to the _root directory_, the top-most directory on your computer
* `.` (period) refers to the _working directory_, the directory that you're currently in.
* `..` (period period) refers to the _parent directory_, the directory that contains your working directory
* `~` (tilde) refers to your _home directory_.

For some more practice, let's make another few directories. Type:
```sh
mkdir -p ./outer/middle/inner outer/middle-2/hello/smaller
```

The `-p` flag tells `mkdir` to make nested directories if needed. Now, we should have this structure:

```
intro-git/
└── outer
    ├── middle
    │   └── inner
    └── middle-2
        └── hello
            └── smaller

6 directories, 0 files
```

To move into the directory called `smaller`, we can type
```sh
cd outer/middle-2/hello/smaller
```

Now, to move from smaller to inner, we can type:
```sh
cd ../../../middle/inner/
```

Notice how we must treverse up 3 directories first. We can also do this in several steps, as long as we move from left to right:
```sh
		# start inside smaller
cd .. 		# move from smaller -> hello
cd ..		# move from hello -> middle-2
cd ..		# move from middle-2 -> outer
cd middle	# move from outer -> middle
cd inner	# move from middle -> inner
```

{% spoiler "Now that you're inside `inner`, try to move to `hello` (click to reveal answer)" %}
```sh
cd ../../middle-2/hello/
```
{% endspoiler %}

Try playing around by traversing through the directories in this example.

Now, try the following:
1. At the prompt, type `cd ~/`, but **don't press enter**.
2. Now, type `int`
3. Press <kbd>tab</kbd>.

The terminal should auto-complete to `intro-git`, the directory we've been working in! If it didn't, press tab again to cycle through other matches. You can press tab to autocomplete in many contexts, and I highly reccomend trying it at random times throught this guide.

The command we just executed was `cd ~/intro-git`. We changed the directory to the one called `intro-git` inside our home directory.

Now that we're done playing with directories, let's clean up :broom:.

### Deleting things

We use the `rmdir` command to delete directories. Try `rmdir outer` to delete the directory that we were playing in before.

{% spoiler "Reveal" %}
Uh oh... we got an error.
```sh
williambarkoff@willsmacbookpro intro-git % rmdir outer
rmdir: outer: Directory not empty
```
{% endspoiler %}

We can't delete this directory because it's not empty. To **override this and force the directory to be deleted**.

Let's go and delete one of our empty inner directories. We can keep doing this until we end up with no more directories!
```sh
cd outer/middle
rmdir inner
```

Now if we use `ls`, we get nothing! Our directory has been deleted. But this seems pretty inefficent for deleting big directory structures, like what we currently have.

Let's `cd` back into `intro-git`. Here's a reminder of what that directory looks like:
```
intro-git
└── outer
    ├── middle
    └── middle-2
        └── hello
            └── smaller

5 directories, 0 files
```

To delete this structure, we can use `rm` (short for remove), a command that deletes files. Type:

```sh
rm -r outer
```

We use the `-r` flag to tell it to behave _recursively_, delete all directories and files in the directory that we give it. Remember, if you're not sure what something does, you can always check the man page: `man rm`.

### Working with files

We've done a lot of work with directories, but you might be wondering, how do we work with files? Let's do it!

To make a new file, you can use `touch`. Touch is called `touch` becuase it updates the access time for a file, and if it doesn't exist, it creates it, so it's actally a side effect that it creates files; however, that's the biggest use case.

Let's make a new file, and call it `hello.txt`:

```sh
touch hello.txt
```

Now if we run `ls`, we should see our new file!
```sh
williambarkoff@willsmacbookpro intro-git % ls
hello.txt
```

Let's write something into our file. In most cases, one would do this with the text editor of their choice (I like [Visual Studio Code](https://code.visualstudio.com/)), but another

## Summary

* First, we learned about the command line, and what a prompt and a shell are.
	* A _shell_ is a special program that lets you talkto the operating system
	* A _prompt_ is the shell's way of telling you that it is ready for your next command
* We also learned about how computers are organized
	* They have _directories_ and _files_, and directories can hold both directories and files.
* Next, we learned about how commands are structured
	* We type the name of the command, then the parameters. For example in, `rm -r my-dir`, `rm` is the command, and `-r my-dir` are the parameters.
* We then learned a bunch of commands
	* `ls` lists the contents of a directory
	* `mkdir` makes a new directory
	* `cd` changes directories
	* `pwd` prints the working directory
	* `rm` deletes a file, and `rmdir` deletes a directory
	* `touch` creates a file
	* 