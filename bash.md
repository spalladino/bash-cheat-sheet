# Comandos

Para saber qué estamos corriendo:

* `type`
* `which`
* `PATH`
* `help / man`

# Composición

`cat criticas-charla.txt > /dev/null`

`mysql agenda < agenda_140425.backup`

`ls /bin | wc -l`

### Otras formas útiles:

* secuencial 									`;`
* secuencial con cortocircuito (AND) `&&`
* secuencial con cortocircuito (OR)	`||`
* ejecución en subshell						`()`
* redirección con esteroides				`2>&1`

# Expansiones

```
rm *.log
cp minecraft.config{,.backup}
rm $(cat files_to_delete.txt)
```

# Quotes

```
>  VAR=Hola
>  echo “\”$VAR\””
“Hola”
>  echo ‘\’$VAR\’’
quote> ...
```

# Subshells y entorno

* `export`
* `unset`
* `exec`
* `source` ó `.`
* `env`
* `set`
* `(cd foo && make); pwd`
* `export PATH=$PATH:/usr/local/bin; run`
* `RAILS_ENV=production rake db:migrate`

# Job control

```
./ejecutable &
jobs
kill %1
```
```
Ctrl-Z
bg
fg
kill, ps, top, nice, renice
```

# History

Bash guarda nuestro historial de comandos:

```
>   history
...toda la historia de comandos
>   history -c
>   history
``` 

`HISTSIZE` y `HISTFILESIZE` controlan cuántos comandos se guardan

`HISTCONTROL=ignoredups` ignora entradas duplicadas en el history

También provee ciertos atajos

```
>   mv my-program /bin
mv my-program /bin: Permission denied
>   !!
mv my-program /bin: Permission denied
>   sudo !!
```

# Keyboard shortcuts


* Principio de línea `Ctrl - A`
* Fin de línea `Ctrl - E`
* Borrar linea entera `Ctrl - U`
* Borrar resto de línea `Ctrl - K`
* Borrar palabra `Ctrl - W`
* Limpiar pantalla `Ctrl - L`
* History search `Ctrl - R`

# Navegación directorios

* `pwd`
* `cd`
* `cd -`
* `pushd, popd, dirs* `

# Funciones

```
> function saludar {
   echo Hola $1
   return 0
}
> saludar Mati
Hola Mati
> saludar Mati && date
Hola Mati
```
## Pseudo variables

* `$0` Nombre de la función, shell o script
* `$1, $2, ...` Parámetros por posición
* `$*` ó `$@` Todos los parámetros: `$1 $2 $3...`
  * `"$*"` Lista de parámetros: `“$1” “$2” “$3”...`
  * `"$@"` Parámetros concatenados: `“$1 $2 $3…”`
* `$#` Cantidad de parámetros
* `$?` Último exit status
* `$$` PID del shell actual

## Control de flujo

```
if condition; then
	commands
else
	commands
fi
```

```
while condition; do
	commands
done
```

```
for var in elements
do
	commands with $var
done
```

# Customización

Archivos de inicialización:

* .bash_profile
* .bash_login
* .profile
* .bashrc

Pueden aprovecharlos para customizar prompt, aliases, y PATH.

### Ejemplo

```
[.bashrc]
…

PS1='\u@\h \w\a ’
PATH=$PATH:$HOME/bin

alias ll=’ls -l’
alias be=’bundle exec’
alias rr=’brew services restart rabbitmq’
```

# Utilidades

```
cp ~/Downloads/bashrc ~
mv ~/bashrc ~/.bashrc
rm ~/Downloads/bashrc
ln -s ~/.bashrc ~user2/.bashrc
touch new_file
```

```
cat foo.txt bar.txt > foobar.txt
cat - > foo.txt
tail -n 200 /var/log/messages
tail -f /var/log/messages
less /var/log/message
```

Shortcuts en less: ```Ctrl-F, Ctrl-B, q, F, /, ?, n, N, <space>, j, k, G, =```

```
cut -f1 -d : /etc/passwd | sort
for i in $(seq 1 10); do echo $i; done
wc -l /etc/passwd
```

### Find

```
find app -name ‘*.rb’ | xargs grep ‘def foo’
find . -name ‘*.bak’ -print0 | xargs -0 rm
find . -name ‘*.bak’ -exec rm {} \;
```

### Grep

```
grep foo *
grep -v foo *
grep -n foo *
grep -r foo *
git grep foo
cat f.txt | sed ‘s/hola/chau/g’
sed -i ‘s/hola/chau/g’ f.txt 
```

### HTTP

* **curl** cliente HTTP genérico

* **wget** GET requests, sigue redirects, descarga respuesta a un archivo

```
curl https://api.github.com/meta
wget http://manas.com.ar/

curl -X DELETE -u $USER:$PASS https://api.github.com/repos/$ORG/$REPO
```

### Compresión

* Comprimir archivos
`tar czf foo.tar.gz files`

* Listar archivos comprimidos
`tar tzf foo.tar.gz`

* Descomprimir
`tar xzf foo.tar.gz`

* Comprimir stdin
`tar cf - files | gzip -c - > foo.tar.gz`

### Netcat

* Gus hace
`nc -l 8989 > xp.vm`

* Mauri hace
`cat windows-xp-sp2-sqlserver.vm | nc bosatsu.local 8989`

### SSH

Login remoto:
`ssh bosatsu.local`

Port forwarding:

```
ssh staging -L 9201:localhost:9200
ssh public-host -R 9200:private-host:9201
```

X forwarding:

```
ssh hostname -X
google-chrome
```

### Lsof y Netstat

* Listar file descriptors abiertos por un proceso
`lsof -p PID`

* Listar conexiones TCP abiertas
`netstat -p tcp -a`

### Nohup y screen

Si quiero que mi comando no dependa del shell:
`nohup ./heavy-task`

Si quiero desligar la sesión de esta terminal y volver después: `screen`

### Otras

* `sleep`
* `true, false`
* `yes`
* `hash -r`
* `id`
* `groups`
* `whoami`
