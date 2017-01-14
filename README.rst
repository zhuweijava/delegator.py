Delegator — Subprocesses for Humans 2.0
=======================================

**Delegator** is a simple library for dealing with subprocesses, inspired
by both envoy and pexpect (in fact, it depends on it!).

This module features two main functions ``delegator.run()`` and ``delegator.chain()``. One runs commands, blocking or non-blocking, and the other runs a chain of commands, seperated by the standard unix pipe operator: ``|``.

Basic Usage
-----------

Basic run functionality::

    >>> c = delegator.run('ls')
    >>> print c.out
    README.rst   delegator.py

    >>> c = delegator.run('long-running-process', block=False)
    >>> c.pid
    35199
    >>> c.block()
    >>> c.return_code
    0

Basic chain functionality::

   >>> c = delegator.chain('fortune | cowsay')
   >>> print c.out
     _______________________________________
    / Our swords shall play the orators for \
    | us.                                   |
    |                                       |
    \ -- Christopher Marlowe                /
     ---------------------------------------
            \   ^__^
             \  (oo)\_______
                (__)\       )\/\
                    ||----w |
                    ||     ||


Expect functionality is built-in too::

    >>> c.expect('Password:')
    >>> c.send('PASSWORD')
    >>> c.block()

Other functions::

    >>> c.kill()
    >>> c.err
    # only available when block=True, otherwise, use c.out