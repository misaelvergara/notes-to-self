_**`PIPE`**_ Pipes let you use (very simple, I insist) the output of a program as the input of another one.
 ``` bash
#this is a pipe
echo "password" | adduser userName
#outputs "password" to the adduser command
#hence, adduser does not prompt for a password
 ```
> `Reference`: http://tldp.org/HOWTO/Bash-Prog-Intro-HOWTO-4.html

---
**`result = $( <commands> )`** is the syntax that makes storing command output to a variable possible
>`Reference`:https://stackoverflow.com/questions/19951369/how-to-store-grep-command-result-in-some-variable-in-shell


The `SED` Command
---
> `Reference`: https://terminalroot.com.br/2015/07/30-exemplos-do-comando-sed-com-regex.html

The Streamline Editor makes it possible to search and replace any kind of printable output in your system's command line terminal.

``` bash
	sed '/server\_name/! s/.*//' text.txt | sed 's/^.*server\_name\(.*\)\;$/\1/' | sed '/^$/d' | sed 's/[[:space:]]//'
```

```bash
# Loops through the files found in the sites-enabled
# directory, executing the scoped commands below for
# each file.
# The mentioned commands matches every occurence of
# "server_name" and then prints its matches to the
# console.

cd /etc/nginx/sites-enabled/

for i in `ls`;
do
sed '/server\_name/! s/.*//' $i | sed '/^$/d' | sed 's/[[:space:]]*//' | sed 's/.*server\_name\s\(.*\)\;/\1/'
done

# sed '/server\_name/! s/.*//'
# > matches everything ".*" that's not 'server_name'
# > and makes it empty "//"

# sed '/^$/d'
# > removes empty lines

# sed 's/[[:space:]]*//'
# > removes empty space

# sed 's/.*server\_name\s\(.*\)\;/\1/'
# matches server_name (.*) and replaces it with the
# first capture group
```
Regex and Bash
---
**`=~`** is a built in regex comparison operator
**`$echo {a..z}`** | **`for n in  {1..100}`**   built-in ranges

```bash
digit="1982190"
if  [[ $digit =~  [0-9]  ]];
then 
	echo "$digit is a digit"
	else
		echo "oops"
fi
```


Variables
---
You cannot have spaces around the `=` assignment operator. Variables should be declares as follows:
```bash
variable="value"
``` 
> `Reference`: https://stackoverflow.com/questions/2268104/command-not-found-error-in-bash-variable-assignment

# notime

https://stackoverflow.com/questions/19328561/bash-script-how-to-find-every-file-in-folder-and-run-command-on-it

https://stackoverflow.com/questions/105212/recursively-list-all-files-in-a-directory-including-files-in-symlink-directories

https://www.meetup.com/pt-BR/GDG-Londrina/photos/

- very important
https://unix.stackexchange.com/questions/181180/replace-multiline-string-in-files

<!--stackedit_data:
eyJoaXN0b3J5IjpbMTIwOTU5OSwyMzAyODcxMjEsLTIwNjI1Nj
kwODcsMTAzNzAyMTE0NSwtMTk2NzkyODc3MV19
-->