User commands
=====
.. note::
   User commands are very similar to slash commands, as they are bundled in the same extension, no need to download the deps if you already have slash        commands setup
   Message commands are also possible but aren't documented here.
.. _Install:

Installation
------------

You need to install those

``$ cd deps && git clone https://github.com/GitSparTV/discordia-slash  && git clone https://github.com/Bilal2453/discordia-interactions``

Import the discordia-slash
----------------

.. code-block:: lua
   
   local discordia= require("discordia")
   local dcmd = require("discordia-slash")
   
   
Create a user command
------------
.. code-block:: lua

    local client = discordia.Client:useApplicationCommands()
    client:enableAllIntents()

       local function initializeCommands(guild)
        local command, err = client:createGuildApplicationCommand(guild.id, {
            type = dia.enums.appCommandType.user, --putting .message could create a message app instead of a user app, but i haven't tested it
            name = "role",
        })
        end
    client:on("ready", function()
            for guild in client.guilds:iter() do
                initializeCommands(guild)
          end
    end)

It is pretty much the same as slash commands but you can't put a description, will break otherwise

Get data
------------
.. code-block:: lua

   client:on("userCommand", function(interaction, command, args)
   print(args)
   end)

So here since it is a user command, no one can really input data so args would be the user it was used on

Full code
------------

.. code-block:: lua

   local discordia= require("discordia")
   local dcmd = require("discordia-slash")
   local client = discordia.Client:useApplicationCommands()
   local discordia_modals = require('discordia-modals')
   local interactionType = discordia.enums.interactionType
   local optionType = discordia.enums.appCommandOptionType
   client:enableAllIntents()
   
   local function initializeCommands(guild)
        local command, err = client:createGuildApplicationCommand(guild.id, {
            type = dia.enums.appCommandType.user, --putting .message could create a message app instead of a user app, but i haven't tested it
            name = "role",
        })
        end
    client:on("ready", function()
            for guild in client.guilds:iter() do
                initializeCommands(guild)
          end
    end)
       client:on("userCommand", function(interaction, command, args)
   print(args)
   end)
   client:run("Bot your token")
