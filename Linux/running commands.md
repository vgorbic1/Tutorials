## Running Commands
The following commads may help if you need to run a satack of commands.
To run commands one by one:
```
onecommand; nextcommand
```
To run next command only if the previous has completed successfully (exited with 0):
```
onecommand && nextcommand
```
To run next command only if the previous has failed:
```
onecommand || nextcommand
```
To plug the output of a command into another command:
```
mkdir $(date "+%Y-%m-%d")
```
In this example, ```date "+%Y-%m-%d"``` is run first, and then the output of the command ```2017-11-24``` is used by mkdir as
the name of the new directory.

