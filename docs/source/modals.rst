Modals
=====

.. _Install:

Installation
------------

You need to install those

``$ cd deps && git clone --branch dev https://github.com/Bilal2453/discordia-interactions && git clone https://github.com/Bilal2453/discordia-modals``

Import the discordia-modals
------------
.. code-block:: lua
   local discordia = require('discordia')
    require('discordia-components')
    local discordia_modals = require('discordia-modals')
    local interactionType = discordia.enums.interactionType
    
Create a modal
------------
.. code-block:: lua
   local textinput_component = discordia_modals.TextInput {
  id = "resolved",
  style = "paragraph",
  label = "dont_then",
}

local modal = discordia_modals.Modal {
  id = "modal_1",
  title = "the title",

  textinput_component,
}

So this i really can't explain how it works, it just works :/

Full code
------------
.. code-block:: lua
   local discordia = require('discordia')
require('discordia-components')
local discordia_modals = require('discordia-modals')
local interactionType = discordia.enums.interactionType

local client = discordia.Client()

local textinput_component = discordia_modals.TextInput {
  id = "resolved",
  style = "paragraph",
  label = "dont_then",
}

local modal = discordia_modals.Modal {
  id = "modal_1",
  title = "the title",

  textinput_component,
}

local btn = discordia.Button{
  id = 'btn',
  label = 'Click Here',
  style = 'danger',
}

client:on('messageCreate', function(msg)
  if msg.content == '>send' then
    msg:replyComponents('Here a button that opens a modal up!', btn)
  end
end)

client:on('interactionCreate', function(intr)
  if intr.type == interactionType.messageComponent and intr.data.custom_id == 'btn' then
    intr:modal(modal)
    local _, modal_intr = client:waitModal(modal.id)

    modal_intr:reply(
      ('modal got submitted!\n\nYour answers:\ntextinput_1 = "%s"\ntextinput_2 = "%s"'):format(
        modal_intr.data.components[1].components[1].value,
        modal_intr.data.components[2].components[1].value
      )
    )
  end
end)

So uhh yeah thats about it
