---
layout: post
title: Docker Pills
tags: Docker
---
### Docker ###

Hola, nuevamente un recordatorio rápido de comandos docker para la lucha con contenedores.

Show Containers:
<code>docker container ls</code>

Execute Commands:
<code>docker container exec [containerId or containerName] [command]</code>

Console on Container:
<code>docker container exec -it [containerId or containerName] /bin/bash</code>

Run  Containers:
<code>docker container run [containerName] :[imageVersion]</code>
<code>docker container run -p [hostPort]:[containerPort][containerName]:[imageVersion]</code>

Background Run:
<code>docker container run --detach -p [hostPort]:[containerPort][containerName]:[imageVersion]</code>

Copiar archivos :
<code>docker container cp [file] elegant_noether:[path]</code>

Ejecutar DockerFile:
<code>docker image build --tag [containerName]:[setNumVersion] .</code>

Volumen:
<code>docker run -d -p [hostPort]:[containerPort] -v /[myVolumeName] :[patFolderOnContainerHost] [containerName]:[imageVersion]</code>

<code>
DockerFile FROM [imageName:imageVersion]
EXPOSE [port]
RUN [shellCommand]
COPY [file] [toPath]
LABEL [KeyPairValuem{maintainer=\"moby-dock@example.com\"}]
</code>

Saludos.