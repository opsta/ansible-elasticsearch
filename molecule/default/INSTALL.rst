*****************************
LXD driver installation guide
*****************************

Requirements
============

* Ansible 2.9
* LXD 4.4
* Molecule 3.0

Install
=======

.. code-block:: bash

    $ sudo snap install lxd
    $ newgrp lxd # Maybe you need to restart your computer
    $ lxc info # To check if we can run lxc command correctly
    $ python3 -m pip install 'ansible molecule ansible-lint flake8'

Run Test
========

.. code-block:: bash

    $ mol test
