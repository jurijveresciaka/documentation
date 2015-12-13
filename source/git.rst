GIT
===

Prime sources
-------------

`Learn Git in a Month of Lunches <https://www.manning.com/books/learn-git-in-a-month-of-lunches>`_

General
-------

Commit often

GIT - distributed version control system.

A repository is a storage area for your files. Typically dir of project.

A commit is a saved change.

Branches are other paths, or lines of development.

Main branch === trunk === master

GIT main features
-----------------

Distributed repository

fast branching

Staging area

Parts
-----

working area

staging area

commit history

GIT commands
------------

.. code-block:: shell

    $ git --version
    $ git clone some-repository
    $ git ls-files
    $ git blame some-file
    $ Q # For quit.
    $ git log --oneline

.. code-block:: shell

    $ git config --global ... # Set configuration setting.
    $ git config ...          # Show configuration setting.
    $ git config --list       # Show all configuration.

Cursor movement links (linux)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

???

GIT command syntax
^^^^^^^^^^^^^^^^^^

git [switches] <command> [<args>]

git === git help

"--version" is switch

"-p" switch for pagination

.. code-block:: shell

    $ git help help # space - page down, b - page up.
    $ git help help # space - page down, b - page up.
    $ git help -a # All commands.
    $ git help glossary

.. code-block:: shell

    $ git help config
    $ git config --help
    $ git help command === git command --help

Theory
^^^^^^

A working directory is simply the place where you do your work.
The repository is the specialized storage area in which you can save versioned files.

.. code-block:: shell

    $ git help repository-layout


Workflow
^^^^^^^^

.. code-block:: shell

    $ git init                     # Create repository.
    $ git add file_name            # Add file to staging area.
    $ git commit -m "Some message" # Add file to repository.

View repository
^^^^^^^^^^^^^^^

.. code-block:: shell

    $ git log --stat # Show files that are a part of the commit.
    $ git ls-files   # Show all files in a repository.

GIT GUI
^^^^^^^

.. code-block:: shell

    $ git gui