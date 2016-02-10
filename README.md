# Elvish Project Ideas

[Elvish](https://github.com/elves/elvish/) is a new Unix shell. Its design emphasizes a small and expressive scripting language at the core, not restricting itself to the traditional syntax and semantics of Unix shell. It also tries to redesign and simplify the user interface of Unix shells, targeting a modern user base.

Elvish is implemented in [go](https://golang.org/) and BSD-licensed.

Each project consists of several subprojects, with growing difficulties (rated on a scale of 5). For very extensive projects, doing two of the subprojects can qualify as a Summer of Code project.

Note that elvish is pre-release software. This implies that it is unstable and incomplete, but it also means that we can make breaking changes wherever we see fit.

## Project: Graphical Interfaces

Although shells are traditionally used from the terminal, there is nothing preventing us from building graphical interfaces. The [terminal interface module](https://github.com/elves/elvish/tree/master/edit), called the line editor, is loosely coupled with the rest of elvish.

### Subproject: Reading lines from a web interface ★☆☆☆☆

To start with, the line editor has a very simple API: calling its `ReadLine` method returns a piece of code that the user just input. We can also get user input using a webpage, e.g. a textbox with a "submit" button. To achieve this, we need (besides building a webpage) to implement a HTTP server within elvish that can accept HTTP request, which is possible with the [net/http](https://golang.org/pkg/net/http/) package in the standard library.

### Subproject: Show command output in the web page ★★★☆☆

To use a shell fully from the web interface, we also need to see the output of commands besides providing input. Regarding the output of commands, there are three possibilities to consider:

1. Many useful programs, like `cat` and `grep` output simple text. Their output can be shown on the webpage as-is as long as it is properly escaped.

2. Elvish functions can output elvish values, which can be strings, lists, maps, function closures and so on. While elvish values all a string representation, it would be much nicer if they can inspected in an interactive, akin to how you can inspect values in the Wolfram web interface (LINK REQUIRED).

3. Other useful programs like `vim` asssumes that it is talking to a terminal, and will output special "escape sequences" to move the cursor, change the color of text, etc.. The easiest way to support such programs is by embedding a terminal emulator within the web interface. There are many JavaScript libraries that do this; google "javascript terminal emulation".

### Subproject: Implementing the line editor's user interface using web interface ★★★☆☆

Although the API of the line editor is deceptively simple, the line editor has a rich user interface. The user can use Tab to ask the shell how incomplete code may be completed - for instance, writing `echo $` and pressing Tab reveals a list of all variables. The user can also press Ctrl-N to enter "navigation mode", which mimics a file manager.

While it is possible for us to simply use the terminal emulation functionality in the previous subproject to show the line editor's user interface, it would be much nicer to reimplement using the web. For instance, an actual dropdown menu for the Tab completion list can look much more natural when using the shell from the web.

### Subproject: Native graphical interface ★★★★☆

## Project: Introspection

### Subproject: Expose the AST to elvish script ★★☆☆☆

### Subproject: Synatx-aware Tab completion in pure elvish ★★☆☆☆

### Subproject: Interactive debugger ★★★☆☆

## Project: Reinventing sed and awk

## Project: POSIX/bash/zsh Emulation

### Subproject: POSIX emulation ★★☆☆☆

### Subproject: Bash emulation ★★★★☆

### Subproject: Zsh emulation ★★★★★
