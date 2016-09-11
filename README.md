# Elvish Project Ideas

[Elvish](https://github.com/elves/elvish/) is a new Unix shell. Its design emphasizes an expressive scripting language as well as a polished user interface. It is implemented in [go](https://golang.org/) and BSD-licensed.

This page lists some ideas for a Summer of Code project for elvish. Each project consists of several subprojects, with increasing difficulties (rated on a scale of 5 starts). For projects consisting of more than two subprojects, doing two of the them is sufficient to qualify as a SoC project.

## Project: Graphical Interfaces

Although shells are traditionally used from the terminal, there is nothing preventing us from building graphical interfaces. The [terminal interface module](https://github.com/elves/elvish/tree/master/edit), called the line editor, is only loosely coupled with the rest of elvish.

### Reading lines from a web interface ★☆☆☆☆

To start with, the line editor has a very simple API: calling its `ReadLine` method promps the user for input and returns it. We can also get user input using a webpage, e.g. a textbox with a "submit" button. To achieve this, we need (besides building a webpage) to implement a HTTP server within elvish that can accept HTTP request, which is possible with the [net/http](https://golang.org/pkg/net/http/) package in the standard library.

### Show command output in the web page ★★★☆☆

Besides taking input from a web page, we also need to see the output of commands. Depending on the type of the command, seveal different strategies need to be implemented:

1. Many programs, like `cat` and `grep`, output simple text. Their output can be shown on the webpage as-is as long as it is properly escaped as HTML.

2. Elvish functions can output elvish values, which can be strings, lists, maps, function closures and so on. While elvish values all have a string representation, it is much nicer if they can inspected in an interactive way -- for instance, deeply nested lists are collapsed and may be expanded using mouse clicks.

3. Other useful programs like `vim` asssumes that it is talking to a terminal, and will output special "escape sequences" to move the cursor, change the color of text, etc.. The easiest way to support such programs is by embedding a terminal emulator within the web interface. There are many JavaScript libraries that do this; google "javascript terminal emulation".

### Implementing the line editor's user interface using web interface ★★★☆☆

While the API of the line editor is deceptively simple, the line editor has a rich user interface. For instance, the user can use Tab to ask the shell how incomplete code may be completed - writing `println $` and pressing Tab reveals a list of all variables. The user can also press Ctrl-N to enter "navigation mode", which mimics a file manager.

While it is possible for us to simply use the terminal emulation functionality in the previous subproject to show the line editor's user interface, it would be much nicer to reimplement such interfaces using web controls. For instance, an actual dropdown menu for the Tab completion list can look much more natural when using the shell from the web.

### Android app ★★★★☆

Android is based on Linux. While elvish can be run on Android within a terminal emulator, it is nice to implement various UI elements using native Android elements. This subproject is similar to the previous one but can require quite more design work.

## Project: Introspection

### Expose the AST to elvish script ★★☆☆☆

Implementing a `quote` special form which, instead of evaluating the arguments, return a AST for the arguments. The AST should be inspectable from elvish.

### Synatx-aware Tab completion in pure elvish ★★☆☆☆

### Interactive debugger ★★★☆☆

## Project: Reinventing sed and awk

## Project: POSIX/bash/zsh Emulation

### POSIX emulation ★★☆☆☆

This subproject serves as a preliminary to the following two subprojects, since both bash and zsh are mostly POSIX-conformant.

### Bash emulation ★★★★☆

Elvish is not compatible with bash. Bash emulation is useful from two aspects:

1. Users migrating from bash can simply use their old `.bashrc` file.

2. Some tools like [virtualenv](https://virtualenv.pypa.io/en/stable/) require you to `source` a (bash) script or `eval` a (bash) snippet from the shell, because they need to (for instance) modify environment variables or override builtin functions. Such tools cannot be used from elvish directly unless we have a bash emulation mode.


### Zsh emulation ★★★★★
