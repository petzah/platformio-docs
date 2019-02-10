..  Copyright (c) 2014-present PlatformIO <contact@platformio.org>
    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at
       http://www.apache.org/licenses/LICENSE-2.0
    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.

.. _ide_vim:

VIM
===

`VIM <http://www.vim.org/>`_ is an open-source, powerful and configurable text
editor. Vim is designed for use both from a command-line interface and as a
standalone application in a graphical user interface.

.. image:: ../_static/images/ide/vim/ide-platformio-vim.png

.. contents::

Integration
-----------

Integration process consists of these steps:

1. Open system Terminal and install :ref:`piocore`
2. Create new folder for your project and change directory (``cd``) to it
3. Generate a project using PIO Core Project Generator (:option:`platformio init --ide`)
4. Import project in IDE.

"Neomake-PlatformIO" Plugin
^^^^^^^^^^^^^^^^^^^^^^^^^^^

Please visit `neomake-platformio <https://github.com/coddingtonbear/neomake-platformio>`_
for the further installation steps and documentation.

Project Generator
^^^^^^^^^^^^^^^^^

Choose board ``ID`` using :ref:`cmd_boards` or `Embedded Boards Explorer <https://platformio.org/boards>`_
command and generate project via :option:`platformio init --ide` command:

.. code-block:: shell

    platformio init --ide vim --board <ID>

Recommended bundles:

* Syntax highlight - `Arduino-syntax-file <https://github.com/vim-scripts/Arduino-syntax-file>`_
* Code Completion - `YouCompleteMe <https://github.com/Valloric/YouCompleteMe>`_ (see configuration example by **Anthony Ford** `PlatformIO/YouCompleteMe Integration <https://gist.github.com/ajford/f551b2b6fd4d6b6e1ef2>`_)
* Syntax checking - `Syntastic <https://github.com/scrooloose/syntastic>`_

Put to the project directory ``Makefile`` wrapper with contents:

.. code-block:: make

    # Uncomment lines below if you have problems with $PATH
    #SHELL := /bin/bash
    #PATH := /usr/local/bin:$(PATH)

    all:
        platformio -f -c vim run

    upload:
        platformio -f -c vim run --target upload

    clean:
        platformio -f -c vim run --target clean

    program:
        platformio -f -c vim run --target program

    uploadfs:
        platformio -f -c vim run --target uploadfs

    update:
        platformio -f -c vim update


Pre-defined targets:

+ ``Build`` - Build project without auto-uploading
+ ``Clean`` - Clean compiled objects.
+ ``Upload`` - Build and upload (if no errors)
+ ``Upload using Programmer`` see :ref:`atmelavr_upload_via_programmer`
+ ``Upload SPIFFS image`` see :ref:`platform_espressif_uploadfs`
+ ``Update platforms and libraries`` - Update installed platforms and libraries via :ref:`cmd_update`.


Now, in VIM ``cd /path/to/this/project`` and press ``Ctrl+B`` or ``Cmd+B``
(Mac). *PlatformIO* should compile your source code from the ``src`` directory,
make firmware and upload it.

.. note::
    If hotkey doesn't work for you, try to add this line
    ``nnoremap <C-b> :make<CR>`` to ``~/.vimrc``

Articles / Manuals
------------------

* `コマンドラインでArduino開発 : vim + platformio (Arduino development at the command line: VIM + PlatformIO, Japanese) <http://qiita.com/caad1229/items/7b5fb47f034ae6e0baf2>`_

See a full list with :ref:`articles`.
