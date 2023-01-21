Slash
=====

.. _Install:

Installation
------------

First off, you need to install the deps


``$ cd deps && git clone https://github.com/GitSparTV/discordia-slash  && git clone https://github.com/Bilal2453/discordia-interactions``

Import the discordia-slash
----------------
```
local discordia= require("discordia")
local dcmd = require("discordia-commands")
```

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


What this will do is that it will create a slash command with a text input

Get the data from the text input
----------------
```client:on("slashCommand", function(interaction, command, args)
print(args.from.person)
end)
```
This will print out the value that has been put in the text field from the slash command
The reason why it has a .from. is because there is the from subcomand between the value and the command, and the name of the value would be person as the name in the example above says
