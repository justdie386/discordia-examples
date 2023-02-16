Create the table data, with the collums id, money, and name
conn:exec[[CREATE TABLE data (id REAL money REAL name REAL]]
This will put the value of math.randominto the collums id, money, name.
conn:exec[[INSERT OR IGNORE INTO data (id, money, name) VALUES('" .. id .. "','" .. math.random(1, 10) .. "','" .. name .. "')]]
get the value of a collum using a user's name
id = message.author.id
local money = conn:exec("SELECT money FROM data WHERE id = '" .. id .. "'")
