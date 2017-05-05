Coquille
========

[![Build Status](https://travis-ci.org/the-lambda-church/coquille.svg?branch=pathogen-bundle)](https://travis-ci.org/the-lambda-church/coquille)

Coquille is a vim plugin aiming to bring the interactivity of CoqIDE into your
favorite editor.

Installation
------------

This repository is meant to be used as a [pathogen][1] bundle. If you don't
already use pathogen (or [some][2] [other][3] [plugin][4] [manager][5]), I strongly recommend that you start right now.

### Dependencies

Coquille depends on the [vimbufsync][6] package.
You will need to make this plugin available in your runtime path (it can be
installed as a pathogen bundle as well) if you want Coquille to work.

#### Python 2.x support

Coquille requires a build of Vim with Python 2.x support. This is notable for Debian and Ubuntu users, as those distributions have recently switched to shipping builds of Vim with Python 3.x support.

* On Ubuntu versions up to 15.10, and Debian versions up to Jessie, the default vim packages ship with Python 2.x support, and Coquille will work out of the box.
* On Ubuntu versions 16.04 and 16.10, the packages `vim-gtx3-py2` (GUI) and `vim-nox-py2` (CLI) provide versions of Vim with Python 2.x support.
* On Ubuntu version 17.04+, and Debian Stretch or later, no Vim packages with Python 2.x support are provided. You must build Vim from source. (This is far from ideal; [help is always appreciated.](#59))

You can check for this with the following command:

    vim --version | grep "+python"

If you see `+python`, then you're good to go. If you see `+python3`, 

### Installation steps

Installing Coquille is as simple as doing :

    cd ~/.vim/bundle
    git clone https://github.com/trefis/coquille.git

Not that by default, you will be in the `pathogen-bundle` branch, which also
ships Vincent Aravantinos [syntax][7] and [indent][8] scripts for Coq, as well
as an ftdetect script.
If you already have those in your vim config, then just switch to the master
branch.

Getting started
---------------

To launch Coquille on your Coq file, run `:CoqLaunch` which will make the
commands :

- CoqNext
- CoqToCursor
- CoqUndo
- CoqKill

available to you.

By default Coquille forces no mapping for these commands, however two sets of
mapping are already defined and you can activate them by adding :

    " Maps Coquille commands to CoqIDE default key bindings
    au FileType coq call coquille#CoqideMapping()

or

    " Maps Coquille commands to <F2> (Undo), <F3> (Next), <F4> (ToCursor)
    au FileType coq call coquille#FNMapping()

to your `.vimrc`.

Alternatively you can, of course, define your owns.

Running query commands
----------------------

You can run an arbitrary query command (that is `Check`, `Print`, etc.) by
calling `:Coq MyCommand foo bar baz.` and the result will be displayed in the
Infos panel.

Configuration
-------------

Note that the color of the "lock zone" is hard coded and might not be pretty in
your specific setup (depending on your terminal, colorscheme, etc).
To change it, you can overwrite the `CheckedByCoq` and `SentToCoq` highlight
groups (`:h hi` and `:h highlight-groups`) to colors that works better for you.
See [coquille.vim][9] for an example.

You can set the following variable to modify Coquille's behavior:

    g:coquille_auto_move            Set it to 'true' if you want Coquille to
        (default = 'false')         move your cursor to the end of the lock zone
                                    after calls to CoqNext or CoqUndo

Screenshots
------------

Because pictures are always the best sellers :

![Coquille at use](http://the-lambda-church.github.io/coquille/coquille.png)

[1]: https://github.com/tpope/vim-pathogen
[2]: https://github.com/VundleVim/Vundle.vim
[3]: https://github.com/junegunn/vim-plug
[4]: https://github.com/MarcWeber/vim-addon-manager
[5]: https://github.com/Shougo/dein.vim
[6]: https://github.com/def-lkb/vimbufsync
[7]: http://www.vim.org/scripts/script.php?script_id=2063 "coq syntax on vim.org"
[8]: http://www.vim.org/scripts/script.php?script_id=2079 "coq indent on vim.org"
[9]: https://github.com/the-lambda-church/coquille/blob/master/autoload/coquille.vim#L103
