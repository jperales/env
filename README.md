# Settings and documentation of my working environment
Author: Javier Perales-Patón - @jperales

## IDE for programming   
### IDE in a nutshell
Programming at the cluster is not that straightforward since there is no graphical
 interface. In contrast, an IDE fully based in the terminal is a powerful tool
 for this task. In addition, important features of a good IDE includes a command-line
 console to run lines of code, and auto-complete sentences as long as you are
 programming.   
Herein it is explained how to set-up such an IDE, so you could develop your project
directly when logged-in the cluster.   
Unfortunately, terminal-based IDE are NOT friendly. It's highly recommended that
you have great expertise with the terminal, `tmux` (terminal client), and `vim` (plain text editor). Fortunately, there are good tutorials on the Internet
(e.g. [vim tutorial](http://www.openvim.com/)).

> **What is this IDE about?** You will have a terminal-based environment with the terminal split in two or three panels. First panel will allow you to program, second panel has an active command-line console session for the language interpreter
(`R`, `python`, `bash`, etc). Optionally, you can open this in a `tmux` panel ,
so you keep a third panel with `bash` terminal for `git`.

IDE for `R` and `python` below:
![IDE_python](https://cloud.githubusercontent.com/assets/891655/7090493/5fba2426-df71-11e4-8eb8-f17668d9361a.png)
![IDE_R](https://raw.githubusercontent.com/jalvesaq/Nvim-R/master/Nvim-R.gif)

### IDE Basics installation   
A pre-requisite is to have already set-up virtual enviroments powered by
miniconda. To do so, please visit [Setting up a virtual environment (env)](#Setting-up-a-virtual-environment-(env)).

Next, install the basics in your `base (virtual enviroment)` using:
```bash
conda install -c conda-forge tmux neovim
```
> Note: `neovim` is the package name, but to execute it just type `nvim`.

And start `nvim` for the first time:
```bash
conda activate base
nvim
# you can quit using ':q'
```
Finally, you will need to install some plugins for `nvim`. To initiate the
config of `nvim`, create the following directory if it does not exist yet:
```
if[ ! -e $HOME/.config/nvim ];then
  mkdir $HOME/.config/nvim
fi
```

### IDE command-line interpreters
The `nvim` interface (first panel) communicates with the command-line interpreter allocated in a second panel.

To start the command-line interpreter for any language, you have to install
certain ad-hoc plugins before.

#### R command-line interpreter
You have to install `vim-r`. More [info](https://github.com/jalvesaq/Nvim-R)

**Installation**   
Follow these instructions: https://gist.github.com/tgirke/7a7c197b443243937f68c422e5471899

**Usage**    
Open a `*.R` or `*.Rmd` file with `nvim` and intialize a connected R session with `\rf`. This command can be remapped to other key combinations, e.g. uncommenting lines 10-12 in `init.vim` will remap it to the `F2` key. Note, the resulting split window among Nvim and R behaves like a split viewport in `nvim` or `vim` meaning the usage of `Ctrl-w w` followed by `i` and `Esc` is important for navigation.

Important keybindings for nvim (vim):

- `\rf`: opens vim-connected R session
- `spacebar`: sends code from vim to R; here remapped in `init.vim` from default `\l`
- `:split` or `:vsplit`: splits viewport (similar to pane split in tmux)
- `gz`: maximizes size of viewport in normal mode (similar to Tmux's `Ctrl-a z` zoom utility)
- `Ctrl-w w`: jumps cursor to R viewport and back; toggle between insert (`i`) and command (`Esc`) mode is required for navigation and controlling the environment.
- `Ctrl-w r`: swaps viewports
- `Ctrl-w =`: resizes splits to equal size
- `Ctrl-w 5< or 5>`: resizes splits to left or right by 5 steps; change number as needed
- `Ctrl-w H` or `Ctrl-w K`: toggles between horizontal/vertical splits
- `Ctrl-spacebar`: omni completion for R objects/functions when nvim is in insert mode. Note, this has been remapped in `init.vim` from difficult to type default `Ctrl-x Ctrl-o`.
- `:h nvim-R`: opens nvim-R's user manual; navigation works the same as for any Vim/Nvim help document
- `:Rhelp fct_name`: opens help for a function from nvim's command mode with text completion support
- `Ctrl-s and Ctrl-x`: freezes/unfreezes vim (some systems)

#### python, bash, and other interpreters
You have to install `vimcmdline`. More [info](https://github.com/jalvesaq/vimcmdline).

**Installation**   
Copy the directories `ftplugin`, `plugin` and `syntax`to your `~/.config/nvim`
directory from this repository: https://github.com/jalvesaq/vimcmdline

**Usage**   
If you are editing one of the supported file types, in Normal mode do:

  - `\s` to start the interpreter.
  - `<Space>` to send the current line to the interpreter.
  - `\<Space>` to send the current line to the interpreter and keep the cursor on the current line.
  - `\q` to send the quit command to the interpreter.
For languages that can source chunks of code:
  - In Visual mode, press:
    - `<Space>` to send a selection of text to the interpreter.
  - And, in Normal mode, press:
    - `\p` to send from the line to the end of paragraph.
    - `\b` to send block of code between the two closest marks.
    - `\f` to send the entire file to the interpreter.


