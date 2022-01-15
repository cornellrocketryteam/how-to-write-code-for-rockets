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

{% spoiler "Help! I didn't get that"%}
Uh oh. [Report the issue here](https://github.com/cornellrocketryteam/how-to-write-code-for-rockets/issues/new).
{% endspoiler %}
{% endspoiler %}

Cool! Let's disect that! Your command had a few parts.
* First, you typed `echo`. This is the name of the program you're runnning. Everything you type between the name of the program and when you press enter are parameters passed to the program.
* You passed the parameter `"hello world"` to the program, `echo`

Echo is one of the simplest programs on your computer. To find out what it does, we can use another program, `man`, short for `manual`. To learn about `echo`, we can read the manual for it. Type `man echo`, and press enter.

{% spoiler "Reveal" %}
You should get something like this:

```
ECHO(1)                            fish-shell                            ECHO(1)



NAME
       echo - display a line of text

SYNOPSIS

          echo [OPTIONS] [STRING]

DESCRIPTION
       echo displays a string of text.

       The following options are available:

       • -n, Do not output a newline
```
{% endspoiler %}

You can use the up and down arrow keys to scroll the document to learn about `echo`.

Echo takes in what ever you give it, and just repeats it back to you, similar to the echo if you were to stand in a cave and yell.