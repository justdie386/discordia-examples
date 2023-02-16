Sqlite
=====
Here, you'll see how to use sqlite made for luvit

Examples
=================
Lets say i wanna make a db for me and my friends, so we each have our own amount of money, for whatever reason.
First, create the table data, with the collums id, money, and name
Create a database
^^^^^^^^^^^^
.. code-block:: lua
   conn:exec[[CREATE TABLE data (id REAL money REAL name REAL]]

This will put the value of math.randominto the collums id, money, name.
.. code-block:: lua

        client:on("messageCreate", function(message)
        if message.content == "create" then
               conn:exec[[INSERT OR IGNORE INTO data (id, name) VALUES('" .. message.member.id .. "','" .. message.member.name .. "')]]
                      end
                end)
    
Add money to a user after he has beeen created into the database
.. code-block:: lua

    client:on("messageCreate", function(message)
    if message.content == "getMoney" then
    conn:exec[[INSERT OR IGNORE INTO data (money) VALUES('" .. math.random(1, 10) .. "')]]
      end
    end)
    
get the value of a collum using a user's name
client:on("messageCreate", function(message)
if message.content == "balance" then
id = message.author.id
local money = conn:exec("SELECT money FROM data WHERE id = '" .. message.author.id .. "'")
if money ~ nil then --nil check just in case
print(money[1][1]
    end
  end
end)
