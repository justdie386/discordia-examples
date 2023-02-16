Get every user with a certain role (also works with onReady as an event)

.. code-block:: lua

  client:on("messageCreate", function(msg)
  for user in message.guild:iter() do
    if user:hasRole("id that you want") then
    print(user.name)
       end
    end
  end)

Make it ping someone which lasts even if the user leaves?

.. code-block:: lua

  client:on("messageCreate", function(msg)
  if msg.content == "nice" then
    msg:reply("<@"..msg.author.id">")
    end
  end)

send a message without replying

.. code-block:: lua

  client:on("messageCreate", function(msg)
    msg.channel:reply("this didn't ping now did it?")
  end)

split a message to get a value from it

.. code-block:: lua

  discordia.extensions --important!!
  client:on("messageCreate", function(msg)
  content = msg.content
  args = content:split()
  if args[1] == "test" --checks if the message that has been split starts with test
  print(args[2]) --this will give out the second string within the args value
  end)

Add reactions to your own messages (i know its basic but for ppl that are new to programmings and the concepts it comes with)

.. code-block:: lua

  client:on("messageCreate", function(msg)
    local myReply = msg:reply("nice")
      myReply:addReaction("copy past your emoji")
  end)
