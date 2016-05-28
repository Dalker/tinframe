### tinframe - a framework for TinTin++ using tmux

* This project is a framework for using the [TinTin++](http://tintin.sourceforge.net/) mud client using the [tmux](https://tmux.github.io/) terminal multiplexer

* rationale: this framework provides a simple, stable environment for the "mud-hopper" who likes to "hop" from mud to mud, visiting various worlds. Each mud has its configuration stored in its own directory, where one can easily import pre-existing mud-specific scripts or create new ones.

* two layouts are provided, called by the shell scripts *tinframe* and *tinframe2*:
  * **tinframe** is meant for wider screens. In its main window the main pane receives mud output, with two lines reserved at the bottom for prompt information. On top of that a few lines with the same width are meant to receive copies of any chat lines (chat detection script to be configured per-mud based on a template). To the right, a fixed-width pane shows an automatic map (started with the 'newmap' alias), some logged information (connection/diconnection times, plus other information to be configured per-mud based on a template), and a third optional 'status' zone which may be configured mud-wise, e.g. to display some processed statistics information. A second tmux window is present in the background providing easy access to a terminal in the right directory for mud-specific scripting and/or note-taking (how to access it depends on local tmux keyboard configuration).
  * **tinframe2** is meant for smaller screens. The contents of tinframe's main tmux window are split between two tmux windows: the first one has the main mud output and chat zone, the second one has the map and everything else.
  * both of these scripts will look for the tinframe lib scripts at a location *../../lib* relative to the mud specific scripts, or at *$TFLIBDIR* if this environment variable exists; also, they assume mud-specific configuration is at *./muds*, unless *$TFMUDSDIR* variable environment exists

* login with **[F9]**, reload scripts with **[F12]**

* read TinFrame help within TinTin++ with **tfhelp** alias

* the character handler requires writing a small character file based on a template and specifying what the mud's log in screen expect if its anything else than *"$user;$pass"*. Logging in with the **loginas** alias will then ensure that the character's position on the map will be memorized between sessions, as well as any other information that can be optionally configured on a per-mud basis: **sessionhelp** for details

* the auto-mapper provides several aliases to help use TinTin++'s mapping capabilities: **maphelp** for details

* a status pane can be used to display flags, properties and buff status: **statushelp** for details

* various information is logged, some automatically, some manually: **loghelp** for details

* Easiest way to install and try TinFrame:
  1.  cd on a console to some convenient place for installation and

      > git clone https://github.com/dalker/tinframe
  2.  make a copy of the blank mud template: starting at the installation root:

      > cd muds

      > cp -ri blank testmud

      > cd testmud

  3. edit the three mandatory lines on the main.tt file that define the mud's name, address and port
  4. rename and edit the chars/samplechar.tt file to define a character for that mud
  5. cd back to the main installation directory and run from a console

     > ./tinframe testmud
