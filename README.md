# bash-tricks
Random bash command or scripting commands I find useful, and a place to quickly lookup stuff I don't do all the time. A great resource to learn, or as a refresher is: https://ryanstutorials.net/bash-scripting-tutorial/

# shortcuts
 * `!!` - repeats last command
  * usage: `sudo !!` to repeat a command that needs sudo

# scripting
## shebang
 * `#!/usr/bin/env bash` - shebang line that is more portable

## variables
 * `varname=value` - setting our own values
  * usage: `foo=bar && echo $foo` (basic)
  * quotes: `greeting='hello world' && echo $greeting` (literal)
  * quotes: `intro="well $greeting" && echo $intro` (substitution)
  * commands: `lines=$(cat somefile | wc -l)` (command substitution)
  * export: `export var=value` (export to shell so accessible in other scripts)
  * length: `${#varname}` (prints number of characters in varname)
 * `$0` - name of script
 * `$1-9` - first 9 arguments passed to script
  * usage: `echo $1`
 * `$@` - all arguments passed to script
 * `$_` - prints target of last command (like folder created)
  * usage: `mkdir somefolder && cd $_`
 * `$#` - counts number of arguments
  * usage: `if [$# -lt 2] then echo "missing required args" exit fi`
 * `$$` - current process ID
 * `$!` - background process ID
 * `$?` - exit status of last executed process
 * `$USER` - username of user running script
 * `$HOSTNAME` - hostname of machine script is running on
 * `$SECONDS` - number of seconds since script was started
 * `$RANDOM` - returns different random number each time
  * usage `echo $RANDOM`
 * `$LINENO` - returns current line number in bash script

## input
 * `read varname` - waits for user input and assigns value to `$varname`
  * usage: `echo "What is your name?" && read firstname && echo -e "Hello, $firstname"`
 * `read var1 var2 var3` - allows user to input multiple values
  * usage: `echo "3 favorite colors?" && read col1 col2 col3 && echo -e "You like $col1, $col2, $col3"`
 * `read -p 'Prompt: ' varname` - prompts for input
  * usage: `read -p 'Username: ' uservar && echo -e "Hello, $uservar"`
 * `read -sp 'Prompt: ' varname` - prompt for input with hidden values
  * usage: `read -sp 'Password: ' passvar && echo -e 'Your password is updated!'`

## arithmetic
 * `let var = 5 + 3` - assigns result to var
 * `expr 5 + 3` - prints result
 * `$(( 5 + 3 ))` - returns result

## conditional
If: 
```
if [ $1 -ge 18 ] && ( [ $USER == 'bob' ] || [ $USER == 'andy' ] )
then
  echo You may go to the party.
elif [ $2 == 'yes' ]
then
  echo You may go to the party but be back before midnight.
else
  echo You may not go to the party.
fi
```

Case:
```
case $1 in
  start)
    echo starting
    ;;
  stop)
    echo stoping
    ;;
  restart)
    echo restarting
    ;;
  *)
    echo don\'t know
    ;;
esac
```

## tests
| Operator	| Description |
|----------|-------------|
| ! EXPRESSION	| The EXPRESSION is false. |
| -n STRING	| The length of STRING is greater than zero. |
| -z STRING	| The lengh of STRING is zero (ie it is empty). |
| STRING1 = STRING2	| STRING1 is equal to STRING2 |
| STRING1 != STRING2	| STRING1 is not equal to STRING2 |
| INTEGER1 -eq INTEGER2	| INTEGER1 is numerically equal to INTEGER2 |
| INTEGER1 -gt INTEGER2	| INTEGER1 is numerically greater than INTEGER2 |
| INTEGER1 -lt INTEGER2	| INTEGER1 is numerically less than INTEGER2 |
| -d FILE	| FILE exists and is a directory. |
| -e FILE	| FILE exists. |
| -r FILE	| FILE exists and the read permission is granted. |
| -s FILE	| FILE exists and it's size is greater than zero (ie. it is not empty). |
| -w FILE	| FILE exists and the write permission is granted. |
| -x FILE	| FILE exists and the execute permission is granted. |

## loops
 * You can use `break` and `continue` within loop

While:
```
counter=1
while [ $counter -le 10 ]
do
  echo $counter
  ((counter++))
done
echo All done
```

Until:
```
counter=1
until [ $counter -gt 10 ]
do
  echo $counter
  ((counter++))
done

echo All done
```

For:
```
names='Stan Kyle Cartman'
for name in $names
do
  echo $name
done

echo All done
```

Select: (useful for simple menus)
```
names='Kyle Cartman Stan Quit'
PS3='Select character: '

select name in $names
do
  if [ $name == 'Quit' ]
  then
    break
  fi
  echo Hello $name
done

echo Bye
```
