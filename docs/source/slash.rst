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
local dia = require("discordia")
local dcmd = require("discordia-commands")
```

Create a slash command
----------------
```
local client = dia.Client():useApplicationCommands()

local function initializeCommands(guild)
    local command, err = client:createGuildApplicationCommand(guild.id, {
        type = commandType.chatInput,
        name = "Hey",
        description = " nice",
        options = {
            {
                type = optionType.subCommand,
                name = " from",
                description = "Enter the id",
                options = {
                    {
                        type = optionType.string, -- set optionType.user to make it select a member
                        name = "person",
                        description = "id",
                        required = true,
                        autocomplete = true,
                    },
                },
            },
        },
    })
    end```
What this will do is that it will create a slash command with a text input

Get the data from the text input
----------------
```client:on("slashCommand", function(interaction, command, args)
print(args.from.person)
end)
```
This will print out the value that has been put in the text field from the slash command
The reason why it has a .from. is because there is the from subcomand between the value and the command, and the name of the value would be person as the name in the example above says
