Sqlite
=====
Here, you'll see how to use sqlite made for luvit

Installation
^^^^^^^^^^^^
If on linux, install sqlite3 from your package manager, for mac and windows, download the `precompiled binary <https://www.sqlite.org/download.html>`_ for your plateform and put the file into your script's folder
Finally, run this

``./lit install SinisterRectus/sqlite3``

Examples
^^^^^^^^^^^^
Lets say i wanna make a database for me and my friends, so we each have our own amount of money, for whatever reason.
First, create the table data, with the collums id, money, and name

Create the database
^^^^^^^^^^^^
.. code-block:: lua

   local sql = require "sqlite3"
   local conn = sql.open("./data.sqlite")
   conn:exec[[CREATE TABLE data (id REAL money REAL name REAL]]


Add a user
^^^^^^^^^^^^
.. code-block:: lua

        client:on("messageCreate", function(message)
        if message.content == "create" then
               conn:exec[[INSERT OR IGNORE INTO data (id, name) VALUES('" .. message.member.id .. "','" .. message.member.name .. "')]]
                      end
                end)
    
Add money to a user after he has beeen created into the database

Give a value
^^^^^^^^^^^^
.. code-block:: lua

    client:on("messageCreate", function(message)
    if message.content == "getMoney" then
    conn:exec[[INSERT OR IGNORE INTO data (money) VALUES('" .. math.random(1, 10) .. "')]]
      end
    end)
    
This gives a random amount of money to the author of the message

Read a value
^^^^^^^^^^^^
.. code-block:: lua

      client:on("messageCreate", function(message)
      if message.content == "balance" then
      id = message.author.id
      local money = conn:exec[[SELECT money FROM data WHERE id = '" .. message.author.id .. "']]
      if money ~ nil then --nil check just in case
      print(money[1][1]) --why [1][1]? not sure but it won't work otherwise
          end
        end
      end)
      
And that gets the amount of money the author has.

More docs/examples
^^^^^^^^^^^^

For additional documentation https://scilua.org/ljsqlite3.html
