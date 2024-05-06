# list of all running processes live

top -o cpu
top -o rsize

# only displaying terminal processes active under the current user

ps aux | more

# search for a specific process

ps aux | grep <PROG_NAME>
ps -ef | grep python

# Kill process

sudo kill 43841
kill -9 <PID>
pkill -f <PROG_NAME>
pkill -f python

# Find what is running on TCP

sudo lsof -nP -iTCP:1025 -sTCP:LISTEN
lsof -i tcp:1025

# Find on which port is running node

lsof -nPi | grep nod

# Mac OSX – Which app is using port 8081

To find out which app is listening on port 8081

```bash
$ lsof -i :8081 | grep LISTEN

node    90202 bojanmazej   21u  IPv6 0xeb80ba02b8b1cd55      0t0  TCP *:sunproxyadmin (LISTEN)
```

The name “node” doesn’t tell you anything, to get the detail, ps the node PID 90202 like this:

```
$ ps -ef 90202
```
