User commands
=====
.. note::
   User commands are very similar to slash commands, as they are bundled in the same extension, no need to download the deps if you already have slash commands    setup 
.. _Install:

Installation
------------

You need to install those

``$ cd deps && git clone https://github.com/GitSparTV/discordia-slash  && git clone https://github.com/Bilal2453/discordia-interactions``

Import the discordia-slash
----------------

.. code-block:: lua
   
   
   local discordia= require("discordia")
   local dcmd = require("discordia-commands")
   
Create a user command
