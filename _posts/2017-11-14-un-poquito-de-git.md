---
layout: post
title: Un poquito de Git
tags: Git
---

Hola, hoy quiero traeros una recopilación de comandos relacionados con la función que realizan sobre un repositorio Git.

Con esta chuleta podremos recordar fácilmente que comandos deberíamos usar en cada caso en nuestra lucha con los repositorios.


<table class="table table-striped"> 
    <thead>
        <tr class="row-1 odd">
            <th class="column-1">Función</th>
            <th class="column-2">Comando</th>
        </tr>
    </thead>
    <tbody class="row-hover">
        <tr class="row-2 even">
            <td class="column-1">Inicializar Repositorio</td>
            <td class="column-2">git init</td>
        </tr>
        <tr class="row-3 odd">
            <td class="column-1">Añadir elemento</td>
            <td class="column-2">git add [fileName/folder/pattern]</td>
        </tr>
        <tr class="row-4 even">
            <td class="column-1">Añadir todos</td>
            <td class="column-2">git add . <b>or</b> --all</td>
        </tr>
        <tr class="row-5 odd">
            <td class="column-1">Add commit y comment</td>
            <td class="column-2">git commit -a -m "[Comment]"</td>
        </tr>
        <tr class="row-6 even">
            <td class="column-1">Añadir ficheros a un commit</td>
            <td class="column-2">git commit --amend -m "[newComment]"</td>
        </tr>
        <tr class="row-7 odd">
            <td class="column-1">Deshacer un commit pero guarda cambios</td>
            <td class="column-2">git reset --soft HEAD</td>
        </tr>
        <tr class="row-8 even">
            <td class="column-1">Deshacer un último commit</td>
            <td class="column-2">git reset --hard HEAD^</td>
        </tr>
        <tr class="row-9 odd">
            <td class="column-1">Deshacer los dos últimos commit</td>
            <td class="column-2">git reset --hard HEAD^^</td>
        </tr>
        <tr class="row-10 even">
            <td class="column-1">Borrar elemento</td>
            <td class="column-2">git rm [fileName/folder/pattern]</td>
        </tr>
        <tr class="row-11 odd">
            <td class="column-1">Añadir nuevo remotes</td>
            <td class="column-2">git remote add [name] [urlRemote]</td>
        </tr>
        <tr class="row-12 even">
            <td class="column-1">Borrar remote</td>
            <td class="column-2">git remote rm [name]</td>
        </tr>
        <tr class="row-13 odd">
            <td class="column-1">Push Remote</td>
            <td class="column-2">git push -u [remoteName] [branch]</td>
        </tr>
        <tr class="row-14 even">
            <td class="column-1">Ver remotes</td>
            <td class="column-2">git remote -v</td>
        </tr>
        <tr class="row-15 odd">
            <td class="column-1">Clonar Repo</td>
            <td class="column-2">git clone [urlRepository]</td>
        </tr>
        <tr class="row-16 even">
            <td class="column-1">Crear branch</td>
            <td class="column-2">git branch [branchName]</td>
        </tr>
        <tr class="row-17 odd">
            <td class="column-1">Borrar branch</td>
            <td class="column-2">git branch -d [branchName] // local</td>
        </tr>
        <tr class="row-18 even">
            <td class="column-1"></td>
            <td class="column-2">git push origin --delete [branchName] //remoteSituarse</td>
        </tr>
        <tr class="row-19 odd">
            <td class="column-1">En branch</td>
            <td class="column-2">git checkout [branchName]</td>
        </tr>
        <tr class="row-20 even">
            <td class="column-1">Crear y situarse</td>
            <td class="column-2">git branch -b [branchName]</td>
        </tr>
        <tr class="row-21 odd">
            <td class="column-1">Mergear branch</td>
            <td class="column-2">git checkout [branchName]</td>
        </tr>
        <tr class="row-22 even">
            <td class="column-1"></td>
            <td class="column-2">// usually master git merge or git merge [fileName]</td>
        </tr>
        <tr class="row-23 odd">
            <td class="column-1">Borrar branch</td>
            <td class="column-2">git branch -d [branchName]</td>
        </tr>
        <tr class="row-24 even">
            <td class="column-1">Ver log de commits</td>
            <td class="column-2">git logActualizar</td>
        </tr>
        <tr class="row-25 odd">
            <td class="column-1">Repositorio Local</td>
            <td class="column-2">git fetch</td>
        </tr>
        <tr class="row-26 even">
            <td class="column-1"></td>
            <td class="column-2">git merge origin/master</td>
        </tr>
        <tr class="row-27 odd">
            <td class="column-1"></td>
            <td class="column-2">git push</td>
        </tr>
        <tr class="row-28 even">
            <td class="column-1">Limpiar en Local remote borrados</td>
            <td class="column-2">git remote gitprune origin</td>
        </tr>
        <tr class="row-29 odd">
            <td class="column-1">Ver remotes locales</td>
            <td class="column-2">git remote show origin</td>
        </tr>
        <tr class="row-30 even">
            <td class="column-1">Push de rama local a rama remota</td>
            <td class="column-2">git push [remoteName] [localBranch remoteBranch]</td>
        </tr>
        <tr class="row-31 odd">
            <td class="column-1">Ver Tag</td>
            <td class="column-2">git tag list</td>
        </tr>
        <tr class="row-32 even">
            <td class="column-1">Borrar Rama Remota</td>
            <td class="column-2">git push origin [remoteBranchName]</td>
        </tr>
        <tr class="row-33 odd">
            <td class="column-1">Obtener Tag</td>
            <td class="column-2">git checkout [tagName]</td>
        </tr>
        <tr class="row-34 even">
            <td class="column-1">Añadir Tag</td>
            <td class="column-2"> git tag -a [tagName] -m "[comment]"</td>
        </tr>
        <tr class="row-35 odd">
            <td class="column-1">Push Tag</td>
            <td class="column-2">git push --tags</td>
        </tr>
        <tr class="row-36 even">
            <td class="column-1">Incluir commits en rama</td>
            <td class="column-2">git fetch git rebase</td>
        </tr>
        <tr class="row-37 odd">
            <td class="column-1"></td>
            <td class="column-2">*Si hay conflictos resolvemos y git rebase --continue</td>
        </tr>
        <tr class="row-38 even">
            <td class="column-1">Mejoras git log</td>
            <td class="column-2">git config --global color.ui true</td>
        </tr>
        <tr class="row-39 odd">
            <td class="column-1">Ver log en una linea</td>
            <td class="column-2">git log --pretty=onelineFormateo</td>
        </tr>
        <tr class="row-40 even">
            <td class="column-1"></td>
            <td class="column-2"> git log --pretty=format "%h %ad- %s "</td>
        </tr>
        <tr class="row-41 odd">
            <td class="column-1"></td>
            <td class="column-2">%ad author date</td>
        </tr>
        <tr class="row-42 even">
            <td class="column-1"></td>
            <td class="column-2">%an author name</td>
        </tr>
        <tr class="row-43 odd">
            <td class="column-1"></td>
            <td class="column-2">%h SHA hash</td>
        </tr>
        <tr class="row-44 even">
            <td class="column-1"></td>
            <td class="column-2">%s subject</td>
        </tr>
        <tr class="row-45 odd">
            <td class="column-1"></td>
            <td class="column-2">%d ref names</td>
        </tr>
        <tr class="row-46 even">
            <td class="column-1">Ver detalle modificaciones</td>
            <td class="column-2">git log --oneline -p</td>
        </tr>
        <tr class="row-47 odd">
            <td class="column-1">Ver inserciones Commit</td>
            <td class="column-2">git log --online --stat</td>
        </tr>
        <tr class="row-48 even">
            <td class="column-1">Ver grafico ramas</td>
            <td class="column-2">git log --oneline --graph</td>
        </tr>
        <tr class="row-49 odd">
            <td class="column-1">Ver rango de log</td>
            <td class="column-2">git log --until=1.minute.ago</td>
        </tr>
        <tr class="row-50 even">
            <td class="column-1"></td>
            <td class="column-2">git log --since=1.day.ago</td>
        </tr>
        <tr class="row-51 odd">
            <td class="column-1"></td>
            <td class="column-2">git log --since=2017-01-01 --until=2017-08-31</td>
        </tr>
        <tr class="row-52 even">
            <td class="column-1">Ver diferencias ultimo commit</td>
            <td class="column-2">git diff</td>
        </tr>
        <tr class="row-53 odd">
            <td class="column-1">Ver diferencias sin commit</td>
            <td class="column-2">git diff HEAD^ / HEAD^^/ HEAD~5</td>
        </tr>
        <tr class="row-54 even">
            <td class="column-1">Ver diferencias con un commit</td>
            <td class="column-2">git diff [hashCommit]</td>
        </tr>
        <tr class="row-55 odd">
            <td class="column-1">Ver diferencias entre Ramas</td>
            <td class="column-2">git diff [branchName] [branchName]</td>
        </tr>
        <tr class="row-56 even">
            <td class="column-1">Ver cambios de un fichero</td>
            <td class="column-2">git blame [fileName] --date short</td>
        </tr>
        <tr class="row-57 odd">
            <td class="column-1">Quitar tracking de cambios</td>
            <td class="column-2">git rm --cached [fileName <b>or</b> folder <b>or</b> pattern]</td>
        </tr>
        <tr class="row-58 even">
            <td class="column-1">Configurar nombre de usuario global</td>
            <td class="column-2"> git config --global user.name "[Name]"</td>
        </tr>
        <tr class="row-59 odd">
            <td class="column-1">Configurar nombre de email global</td>
            <td class="column-2"> git config --global user.email "[email]"</td>
        </tr>
        <tr class="row-60 even">
            <td class="column-1">Configurar nombre de usuario para repo</td>
            <td class="column-2"> git config user.name "[Name]"</td>
        </tr>
        <tr class="row-61 odd">
            <td class="column-1">Configurar nombre de email para repo</td>
            <td class="column-2"> git config user.email "[email]"</td>
        </tr>
        <tr class="row-62 even">
            <td class="column-1">Configurar log personal</td>
            <td class="column-2"> git config --global alias.mylog \\"log --graph [morelogTags]"</td>
        </tr>
        <tr class="row-63 odd">
            <td class="column-1">Alias de comandos</td>
            <td class="column-2">git config --global alias.[abreviatura] [gitCommand]</td>
        </tr>
        <tr class="row-64 even">
            <td class="column-1"></td>
            <td class="column-2">git config help para más configs</td>
        </tr>
        <tr class="row-65 odd">
            <td class="column-1">Rebase interactivo</td>
            <td class="column-2">git rebase -i [HEAD~numberHeadsToRebase]</td>
        </tr>
        <tr class="row-66 even">
            <td class="column-1">Rebase comment</td>
            <td class="column-2">change pick-&gt;reword [newComment]</td>
        </tr>
        <tr class="row-67 odd">
            <td class="column-1">Rebase con separación de commit</td>
            <td class="column-2">change pick-&gt; editRecommit git reset HEAD</td>
        </tr>
        <tr class="row-68 even">
            <td class="column-1">Squash merge commit</td>
            <td class="column-2">git rebase -i [HEAD~numberHeadsToRebase] pick -&gt; squash</td>
        </tr>
        <tr class="row-69 odd">
            <td class="column-1">Guardar temporalmente un trabajo</td>
            <td class="column-2">git stash save</td>
        </tr>
        <tr class="row-70 even">
            <td class="column-1">Recuperar un trabajo guardado temp</td>
            <td class="column-2">git stash apply</td>
        </tr>
        <tr class="row-71 odd">
            <td class="column-1"></td>
            <td class="column-2">git stash apply [stashName]</td>
        </tr>
        <tr class="row-72 even">
            <td class="column-1">Ver lista de stashes</td>
            <td class="column-2">git stash</td>
        </tr>
        <tr class="row-73 odd">
            <td class="column-1">Descartar stash</td>
            <td class="column-2">git stash drop
                <br>git stash drop [stashName]</td>
        </tr>
        <tr class="row-74 even">
            <td class="column-1">Recuperar y borrar</td>
            <td class="column-2">git stash pop</td>
        </tr>
        <tr class="row-75 odd">
            <td class="column-1">Recuperar stash sin staging</td>
            <td class="column-2">git stash save --keep-index</td>
        </tr>
    </tbody>
</table>

Saludos.