SPHINX
======

Prime sources
-------------

`<http://sphinx-doc.org/>`_

`<http://www.readthedocs.org/>`_

Install
-------

.. code-block:: shell

    $ pip install sphinx sphinx-autobuild

Create documentation project
----------------------------

.. note:: This is how this documentation was generated. Credit to `<https://youtu.be/oJsUvBQyHBs>`_

.. code-block:: shell

    $ sphinx-quickstart

    > Root path for the documentation [.]:
    > Separate source and build directories (y/n) [n]: y
    > Name prefix for templates and static dir [_]: n
    > Project name: documentation
    > Author name(s): Jurij Veresciaka
    > Project version: 0.0.1
    > Project release [0.0.1]:
    > Project language [en]:
    > Source file suffix [.rst]:
    > Name of your master document (without suffix) [index]:
    > Do you want to use the epub builder (y/n) [n]:
    > autodoc: automatically insert docstrings from modules (y/n) [n]: y
    > doctest: automatically test code snippets in doctest blocks (y/n) [n]:
    > intersphinx: link between Sphinx documentation of different projects (y/n) [n]:
    > todo: write "todo" entries that can be shown or hidden on build (y/n) [n]:
    > coverage: checks for documentation coverage (y/n) [n]:
    > pngmath: include math, rendered as PNG images (y/n) [n]:
    > mathjax: include math, rendered in the browser by MathJax (y/n) [n]:
    > ifconfig: conditional inclusion of content based on config values (y/n) [n]:
    > viewcode: include links to the source code of documented Python objects (y/n) [n]:
    > Create Makefile? (y/n) [y]:
    > Create Windows command file? (y/n) [y]:

Fine-tune
---------

.gitignore
^^^^^^^^^^

.. code-block:: shell

    .idea/
    *~
    build/

conf.py
^^^^^^^

Replace:

.. code-block:: python

    html_theme = 'alabaster'

With:

.. code-block:: python

    #html_theme = 'alabaster'

    # on_rtd is whether we are on readthedocs.org, this line of code grabbed from docs.readthedocs.org
    on_rtd = os.environ.get('READTHEDOCS', None) == 'True'

    if not on_rtd:  # only import and set the theme if we're building docs locally
        import sphinx_rtd_theme
        html_theme = 'sphinx_rtd_theme'
        html_theme_path = [sphinx_rtd_theme.get_html_theme_path()]

    # otherwise, readthedocs.org uses their theme by default, so no need to specify it

Generate html output
--------------------

.. code-block:: shell

    $ make html
