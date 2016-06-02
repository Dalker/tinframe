## TinFrame - a framework for TinTin++ using tmux

### What is TinFrame?

This project is a framework for using the [TinTin++](http://tintin.sourceforge.net/) mud client with the [tmux](https://tmux.github.io/) terminal multiplexer

* **rationale**: this framework provides a simple, stable environment for the "mud-hopper" who likes to "hop" from mud to mud, visiting various worlds. Each mud has its configuration stored in its own directory, where one can easily import pre-existing mud-specific scripts or create new ones.

* **requirements**: [TinTin++](http://tintin.sourceforge.net/), [tmux](https://tmux.github.io/) 

* **used by default**: [zsh](http://zsh.sourceforge.net/) - 
  `zsh` can probably be replaced by `bash` or some other shell - this requires editing the [shebangs](https://en.wikipedia.org/wiki/Shebang_%28Unix%29#Examples) and direct calls to zsh in the `tinframe` and `tinframe2` shell scripts

* Here's what it can look like:

![screenshot](screenshot.png?raw=true "Screenshot of TinFrame")

### Easiest way to install and try TinFrame:
  1.  cd on a console to some convenient place for installation and

      > git clone https://github.com/dalker/tinframe
  2.  make a copy of the blank mud template: starting at the installation root:

      > cd muds

      > cp -ri blank testmud

      > cd testmud

  3. edit the three mandatory lines on the `main.tt` file that define the mud's name, address and port
  4. rename and edit the chars/samplechar.tt file to define a character for that mud
  5. cd back to the main installation directory and run from a console

     > ./tinframe testmud
  6. read TinFrame help within TinTin++ with the `tfhelp` alias
  7. login with **[F9]**

### Some extra details

* **session handling** works best if a small character file is written based on a provided template. The minimum it must contain is a definition of the variable `$user` and `$pass` for that character, and possibly some minor adaptations of the mud's `main.tt` regarding the login sequence expected by the mud. The character's status and map location will be automatically saved between sessions. Type `sessionhelp` within a TinFrame session ofTinTin++ for more details

* the **auto-mapper** provides several aliases to help use TinTin++'s mapping capabilities: `maphelp` for details

* a **status pan**e can be used to display flags, properties and buff status: `statushelp` for details

* **logging** of various information is peformed, some automatically, some manually: `loghelp` for details

* **alternate layouts** are provided, called by the shell scripts *tinframe* and *tinframe2*:
  * `tinframe` is meant for wider screens. In its main window the main pane receives mud output, with two lines reserved at the bottom for prompt information. On top of that a few lines with the same width are meant to receive copies of any chat lines (chat detection script to be configured per-mud based on a template). To the right, a fixed-width pane shows an automatic map (started with the `newmap` alias), some logged information (connection/diconnection times, plus other information to be configured per-mud based on a template), and a third optional 'status' zone which may be configured mud-wise, e.g. to display buff status. A second tmux window is present in the background providing easy access to a terminal in the right directory for mud-specific scripting and/or note-taking (how to access it depends on local tmux keyboard configuration).
  * `tinframe2` is meant for smaller screens. The contents of tinframe's main tmux window are split between two tmux windows: the first one has the main mud output and chat zone, the second one has the map and everything else.
  * `multiframe` is meant for wider screens when handling two characters in one mud, for those muds that allow multiplaying (no generic library handling for multiplaying provided yet)
  * all of these scripts will look for the tinframe lib scripts at a location `../../lib` relative to the mud specific scripts, or at `$TFLIBDIR` if this environment variable exists; also, they assume mud-specific configuration is at `./muds`, unless `$TFMUDSDIR` variable environment exists

* notice that all scripts have comment markers for folding in [vim](http://www.vim.org/), but can obviously be edited with any text editor
