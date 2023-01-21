Slash
=====

.. _Install:

Installation
------------

First off, you need to install the deps


``$ cd deps && git clone https://github.com/GitSparTV/discordia-slash  && git clone https://github.com/Bilal2453/discordia-interactions``

Import the discordia-slash
----------------
.. code-block:: lua

   local discordia= require("discordia")
   local dcmd = require("discordia-slash")

Create a slash command
----------------
.. code-block:: lua

   local client = discordia.Client():useApplicationCommands()

   local function initializeCommands(guild)
    local command, err = client:createGuildApplicationCommand(guild.id, {
        type = commandType.chatInput,
        name = "get-users",
        description = " nice",
        options = {
            {
                type = optionType.subCommand,
                name = " from",
                description = "Enter the id",
                options = {
                    {
                        type = optionType.string,
                        name = "role",
                        description = "id",
                        required = true,
                        autocomplete = true,
                    },
                },
            },
        },
    })
    end
    client:on("ready", function()
        for guild in client.guilds:iter() do
             --for some reason we need to use this to actually load the slash command or smt otherwise it won't create itself
            initializeCommands(guild)
      end
   end)


What this will do is that it will create a slash command with a text input and the client:on("ready") will initialize the command onto the server, note that there are other way to initialize the command but i use that one.

Get the data from the text input
----------------
.. code-block:: lua

   client:on("slashCommand", function(interaction, command, args)
      print(args.from.person)
   end)
   
This will print out the value that has been put in the text field from the slash command
The reason why it has a .from. is because there is the from subcomand between the value and the command, and the name of the value would be person as the name in the example above says.

Full code
----------------
.. code-block:: lua

   local discordia= require("discordia")
   local dcmd = require("discordia-slash")
     local client = discordia.Client():useApplicationCommands()

 local function initializeCommands(guild)
    local command, err = client:createGuildApplicationCommand(guild.id, {
        type = commandType.chatInput,
        name = "get-users",
        description = " nice",
        options = {
            {
                type = optionType.subCommand,
                name = " from",
                description = "Enter the id",
                options = {
                    {
                        type = optionType.string,
                        name = "role",
                        description = "id",
                        required = true, --put false if you want it to be optional
                        autocomplete = true, --won't change anything if the optionType is a .string, will autocomplete with users if it is a optionType.user
                    },
                },
            },
        },
    })
    end
    client:on("ready", function()
        for guild in client.guilds:iter() do
            initializeCommands(guild) --there are other way to initialize it but it is the only way i know
      end
   end)
   client:on("slashCommand", function(interaction, command, args)
      print(args.from.person)
      interaction:reply("Success!")
   end)
   client:run("Bot your token")

This will create a slash command, and will print the inputed value when running the slash command.
