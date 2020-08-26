## Lista de comando GIT, desde que iniciamos a usar el 'Sistema de Control de Versiones'.

### Configuración inicial de Git:

$ **git config --global user.name ". . ."**: Estamos conectando GIT con nuestro perfil. (Esto ayudará a tener un mejor control para la linea de tiempo de cambio, porque nos indicarán que persona lo está haciendo).

$ **git config --global user.email ". . ."**: Estamos conectando GIT con nuestro perfil. (Esto ayudará a tener un mejor control para la linea de tiempo de cambio, porque nos indicarán que persona lo está haciendo).

### Creando una repo local:

$ **git init**: Con este comando estaremos inicializando el repositorio, según la carpeta en la que te encuentres.

### Primero comandos para interactuar con tu repo:

$ **git status**: Nos muestra cual es la situación de nuestro repositorio segpun lo que vamos avanzando.

$ **git add [nombre de archivo || .]**: Añadir archivos a un stage.

$ **git rm --cached [name_file]**: Eliminar el archivo añadido solo al stage (esto se encuentra en la memoria RAM).

$ **git rm --forced [name_file]**: Elimina el archivo desde raiz, es decir, no se mostrará ni en el stage, ni en el disco.

> **PROTIP**: Git siempre guarda todo, asi que en un extremo caso si sería posible recuperar esos archivos eliminados, con comandos aún mas avanzados.

$ **git commit -m ". . ."**: Guardar los archivos que estan en el stage, hacia el repositorio local.

$ **git show**: Muestra un listado de todos los commits en la lineas de tiempo de un archivo.

$ **git log**: Hace una función similar al git show, donde muestra la linea de tiempo de commits dentro de un repositorio.

$ **git diff [hash_anteior hash_nuevo]**: Esto muestra en consola todos los cambios realizados directamente en el archivo identificado con un hash. 

### Úsese en caso de emergencia: 😉

$ **git reset [hash_number] --soft**: Con este comando estaremos volviendo a un punto en el tiempo, pero sin eliminar cambios, solamente generando una nueva linea del tiempo, y manteniendo aquellos archivos que hayan sido añadidos al stage hasta ese entonces.

$ **git reset [hash_number] --hard**: Con este comando estaremos forzando a volver todos los cambios hasta tal punto, que elimine todos los archivos añadidos al stage. Sin dejar rastro alguno de cambios.

$ **git reset HEAD**: Este comando no eliminará ningún archivo o cambio, solo quitará archivos que estén en el staging para poder unirlos a uno nuevo y posteriormemtne a un nuevo commit.

### Introduciendonos a fundamentos de Git Flow:

⛓ [GitFlow - Atlassian](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow)  
⛓ [GitFlow - CheatSheet](https://danielkummer.github.io/git-flow-cheatsheet/)

$ **git branch**: Hace un listado de las ramas actuales, existentes, dentro del repositorio.

$ **git branch [new_branch]**: Este comando nos creará una nueva rama, con el nombre que querramos.

$ **git checkout [name_branch]**: Este comando nos servirá para poder cambiar entre ramas ya existentes dentro del repositorio.

$ **git checkout -b [name_branch]**: Este comando une dos funcionalidades, la de crear una nueva rama, y a su vez saltarse hacia esa rama.

$ **git checkout [hash_number]**: Por otro lado, este comando nos permite 'hechar una ojeada' a los cambios en cierto punto del tiempo, sin tener que alterar nada o modificar archivos. 

> **PROTIP**: Procura que al hacer uso de este comando, solo sea para ver cambios "git diff"; y no execute un 'add' o un 'commit', ya que esto hará que se vuelva por completo una nueva modificación y lo anterior desaparezca.

### Combinando ramas y solucionando conflictos:

$ **git merge [name_branch]**: Este comando hará una fusión desde donde se le indique con el nombre de la rama, todo esto en el local.

> **PROTIP**: Para una fusión adecuada, debes asegurarte de estar en la rama a la que quieres que todo se fusione (git checkout [name_branch]). Recuerda que la fusión se realiza desde la rama a la que apuntas hacia donde estás ubicada.

    Cuando tengas confictos, NO DESESPERES!!:

    ✅ Primero asegurate de cuales fueron los cambios en conflicto.
    ✅ Identifica cuales son los cambios que validarás.
    ✅ Si usas [VS Code](vscode.com), este editor te ayudará a solucionarlo de manera más rápida.
      *Solo asegurate de cumplir los primero pasos*.
    ✅ Acepta los cambios que necesites, Y LISTO!!. 

### Conectando a remoto (GitHub):

$ **git remote add origin master [URL_de_Repo]**: Con este comando podremos enlazar nuestro proyecto con un repositorio en la nube.

$ **git remote -v**: Si en caso necesitamos ver, que repositorios tenemos enlazado como remoto.

$ **git pull origin [branch_name]**: Este comando nos ayuda a traer repositorios remotos, hacia nuestro local.

    Si en caso se tienen archivos en la nube, que no están en nuestro local,
    necesariamente se debe traerlos y fusionarlos.

$ **git push origin [branch_name]**: Con este comando podremos subir todo nuestro proyecto hacia un repositorio remoto enlazado previamente.

> **PROTIP**: Si por algún motivo, al enlazar los repositorios remotos con locales, tienes un Warning!, de seguro el remoto tiene archivos que el local no, aquí tienes los pasos que debes realizar para lograr un buen 'git pull'.

    ✅ primero se debe traer esos cambios (git pull origin [branch_name]).
    ✅ Fusionarlos con la repo local, y solucionar conflictos, si es que la hay.
    ✅ Y finalmente pushear todo el proyecto, hacia la nube.

$ **git pull origin master --allow-unrelated-histories**: Si te quieres ahorrar todos los pasos anteriores, consideras que no hay conflictos graves, y todo debería unirse de manera forzada, ejecuta este comando.

### Configuracion de llave SSH en local:

* *Primero debes configurar Git con el gmail que usas generalmente tu username.*

$ **ssh-keygen -t rsa -b 4096 -C "loloy.laurencio@gmail.com"**: este comando generará un llave SSH pública y privada para tu local.

$ **eval $(ssh-agent -s)**: Comprobar que el servidor de llaves SSH esté encendido. (Este comando devolverá el ID del proceso).

$ **ssh-add ~/.ssh/id_rsa**: Agregar  la llave pública a tu entorno local, es decir, confirmar que exista.

### Conexión de llave SSH local con GitHub:

*Creamos una llave SSH desde GitHub - Settings - Generate SHH Key.*

Necesitamos la URL que GitHub nos dá, en versión SSH. Y pasamos a configurar Git en nuestro local.

$ **git remote set-url origin [git@github.com:username/repository.git]**: De esta manera estaremos dando un nuevo valor a la conexión remota que antes configuramos. 

    (Verifica esto con 'git remote -v')
    Luego de haber hecho esto, ya podraś realizar cambios, subirlos a github, y de igual manera bajarlos a tu local.

### Creando etiquetas para un mejor versionamiento:

> *Debes tener copiado el hash del commit, al que quieres agreagrle un tag*

$ **git tag -a [version] -m "nombre_de_tag" [hash_commit]**: Crear etiquetas de versión hacia un commit, el que se le indique y con el nombre que nosotros le indiquemos. *Ejm: (v0.1)*

$ **git show-ref --tags**: Para poder ver todos los tags que se han creado.

$ **git tag**: De igual manera, nos muestra todas las etiquetas que se tienen creadas.

> **PROTIP**: Como buena práctica es traer nuevamente los cambios guardados en la nube de GitHub (git pull origin master).

Y luego vovler a enviar los cambios del local.

$ **git push origin --tags**: Esto cargará los tags creados hacia GitHub.

$ **git tag -d [nombre_de_tag]**: Con este comando podrás eliminar el tag que se le indiques, solo en nuestro local.

> **PROTIP**: Como te indiqué, como buena práctica deben traer los cambios,*(git pull origin master)*.

$ **git push origin :refs/tags/[nombre_de_tag]**: Este comando, eliminará en GitHub al 100%, la etiqueta indicada. *(Ten cuidado al usarlo)*

### Subir otras ramas a nuestro repositorio en GitHub:

$ **git show-branch --all**: Mostrar las ramas, con información adicional sobre su historia.

> **PROTIP**: Al crear una rama, ten en cuenta que desde la rama donde estés, se creará una versión alterna. Procura estar en la rama donde todos los cambios estén actualizados. *(Ejm: master)* Utiliza **git checkout [nombre_rama]** para moverte a la rama más actualizada.

$ **git push origin [nombre_otra_rama]**: Subir los cambios desde la rama que acabas de crear e hiciste cambios *(en caso sea diferente a **master**)*.

### Configurando nuevos colaboradores al flujo de trabajo:

> Primero debemos incluir a una nueva persona desde las configuraciones de GitHub. Ya sea por su correo o su username en la plataforma.

[WIP]. . .

### Buenas prácticas de trabajo con Git y GitHub:

> **PROTIP**: Evitar cargar archivos binarios dentro de los repositorios (imágenes, etc). Aquí hay una solución.

$ **touch .gitignore**: Debes crear un archivo con este nombre exacto. Y agregar todos los archivos, por lo general binarios, y entre otros que no son necesarios subir al repositorio, porque aumentan el tamaño y en general,es una muy mala práctica.

$ **touch README.md**: Este archivo nos permitirá hacer nuestra repo, mucho más explicita para las personas que lo visitan, esto debe contener información fundamental respecto de que trata el repositorio (titulos, enlaces, imágenes, tablas, etc, etc).

$ **username.github.io**: Al crear un repositorio con este nombre, estaremos haciendo uso de un servicio de hosting gratuito que nos brinda GitHub, para poder alojar nuestro proyecto Open Source en internet.

> **PROTIP**: Los GH-Pages, lo activas desde el apartado *Settings/gh-pages* de nuestro repositorio que queremos liberar hacia el mundo. Solo recuerda que el nombre que debe tener este repositorio, debe ser el mismo que te muestro anteriormente.

### Alterando la historia de manera silenciosa:

> **PROTIP**: Este comando se debe usar solamente en local, para modificar cambios que sean realmente necesarios. De otro modo no debemos usar el **rebase** para la historia de nuestros repositorio, y mucho menos llevarlos a GitHub sin haberlos terminado. 
> 
> Recuerda que el reporitorio remoto debe mantenerse lo más limpia posible de ramas, conflictos, alteraciones de historias.

*Ejm: Hemos hecho cambios a ramas MASTER y FIX al mismo tiempo, (estos cambios pueden ser en el mismo archivo y mismas lineas). Lo que hará **git rebase** será juntar ambas ramas, **sin borrar ningún cambio**, es decir "reescribir la historia", y hacer como si está separación de ramas nunca hubiese existido, una vez subidos al repositorio remoto || GitHub.*

$ **git rebase [master]**: Ubicandonos primero en la rama FIX *(git checkout fix)*, haremos uso de este comando para unir la rama MASTER. (primero se hace el **rebase** a la rama que quiero desaparecer de la historia).

$ **git rebase [fix]** Luego debemos ubicarnos en la rama MASTER *(git checkout master)*, para unir la rama master hacia FIX, como buena práctica.

Procura que esto sea hecho en el orden correcto (la que te indiqué atrás). De otra manera podrías generar conflictos inesperados, que tendrías que solucionar usando *git reset*, que es algo que no queremos.

$ **git branch -D [fix]**: Pasamos a eliminar esta rama, que solo nos debía servir para solucionar errores.

$ **git pull origin master**: Traemos cambios, como buena práctica.

$ **git push origin master**: Subimos los cambios realizados a remoto. Te daraś cuenta que jamás existió una rama tal, y la historia se mantiene en orden.

### Un almacenamiento temporal que te puede salvar la vida:

$ **git stash**: Esto es un espacio temporal, que utilizaremos para guardar los últimos cambios (que no hayan sido añadidos ni commiteados al stage), y que puedas hacer commit en otra rama.

$ **git stash pop**: Una vez ubicado en otra rama, necesitas ejecutar este comando, para que esos cambios almacenados en una memoria temporal sean puestos a la disposición de esta rama. Una vez hecho esto, podremos ser libre de commitear los cambios.

$ **git stash list**: Este comando nos muestra todos los cambios que almacenamos en el espacio temporal.

$ **git stash drop**: En este caso eliminarás los cambios almacenados en el temporal, para revertir hasta el último commit realizado.

### Haciendo limpieza de lo innecesario:

$ **git clea --dry-run**: Nos mostrará que archivos es capaz de eliminar

$ **git clean -f**: Eliminará aquellos archivos que GIT considerará innecesarios.

> **PROTIP**: Si bien es cierto que este comando elimina de manera certera archivos innecesarios, debes tener en cuenta que no borrará archivos que están **trackeados** por git, o archivos que se encuentren dentro del **.gitignore**.

$ **git clean -df**: Este comando si borrará archivos duplicados, aún así estén trackeados.

### Recontruyendo commits:

$ **git commit --amend**: Este comando será de mucha utilidad, en el momento en el que hayamos hecho un commit, pero luego se nos olvidó que ese commit debía tener otro cambio adicional. Asi que primero realizamos ese cambio, lo añadimos al stage, y al momento de hacer commit, hacemos uso del **--amend** para que el último commit se reescriba en si mismo con todo éste último cambio.

### Reseteando errores trágicos!:

$ **git reflog**: Muestra la historia de todos, TODOS, los cambios que se hicieron en GIT. **(GIT nunca elimina nada)**

$ **git reset --HARD [hash_number]**: resetear todos los commits realizados hatsa cierto punto, indicado por el numero de hash (o hash del commit).

### Buscando dentro de nuestra repo:

$ **git grep [word]**: Bucar dentro de los archivos, alguna palabra indicada..

$ **git grep -n [word]**: Buscar en que linea usé la plaabra indicada

$ **git grep -c [word]**: Buscar la cantidad de veces usada la palabra indicada.

$ **git grep -c "[tag]"**: Buscar por etiquetas, o dentro del código.

$ **git log -S "[word]"**: Buscar dentro del historial de la repo, la palabra indicada.

### Y algunos HACKS para GIT: (Harry Roberts)

$ **git shortlog -sn --all**: Muestra la cantidad de commits realizados, por usuario colaborador dentro de la repo.

$ **git shortlog -sn --all --no-merges**: Muestra la cantidad de commits, sin contabilizar los commit de merge.

> **PROTIP**: Vamos a darle un alias a todo este último comando.

$ **git config --global alias.stats "shortlog -sn --all --no-merges"**: Estamos creando un alias global para todo este comando de estadisticas de commits.

$ **git blame -c [name_file]**: Este comando nos muestra 'quien hizo que cambios' dentro del archivo indicado.

$ **git blame -c [name_file] -L[N1,N2] -c**: Este comando nos muestra lo mismo que el comando anterior, pero dandole el limite de lineas de código dentro del archivo indicado.

$ **git branch -r**: Ver las ramas remotas.

$ **git branch -a**: Ver todas las ramas, locales y remotos.

Te recomiendo revisar los insights de tus repositorios en GitHub, asi como de otros repositorios, para inspiración. 😉