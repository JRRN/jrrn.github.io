---
layout: post
title: Sin Servidor vs Contenedores
tags: Arquitectura
---

**¿Qué es sin servidor?**

Sin servidor (Serverless) es un enfoque de desarrollo que no basa su infraestructura en máquinas virtuales sino que como servicio Saas, demanda acceso para su ejecución y lo libera después de su uso.

Esto no quiere decir que por detrás de las aplicaciones sin servidor no exista una infraestructura, sino que esta es transparente para las aplicaciones sin servidor ya que es el proveedor el que administra estos servidores y no tienen porque estar en ejecución.

Por otro, esta infraestructura configura eventos que activan la ejecución de nuestras aplicaciones sin servidor hasta que finaliza, quedando en un estado de inactividad hasta la siguiente petición o evento.

**Ventajas de sin servidor**

- Sólo se paga por el tiempo de ejecución. Como se mencionó anteriormente, el servidor solo se ejecuta cuando un evento lo activa, por lo que solo pagará por el corto tiempo cuando el servidor está activo.

- Permite elasticidad. Se puede escalar automáticamente para muchas peticiones  concurrentes y volver a desescalar cuando éstas disminuyen.

- No necesita administrar servidores. El aprovisionamiento de la infraestructura corre a cuenta del proveedor Cloud (AWS, Azure, Google).

- Con lo que sumado al punto anterior, reducimos el tiempo de desarrollo, ya que nos focalizamos en desarrollar.

- Encaja muy bien con microservicios, donde los desarrolladores construyen partes más pequeñas e independientes de toda la arquitectura.

- No necesitan una ubicación, no necesitas conocer los servidores en la nube donde albergara nuestras aplicaciones.

**Inconvenientes de sin servidor**

- Tienen algo de latencia en las primeras peticiones si el servidor está inactivo.

- Desarrollar en un y para un Cloud específico, nos limita a ese proveedor.

- Esta enfocado a aplicaciones de corta duración, no más de 15 minutos.

- No hay control sobre el servidor que ejecuta la aplicación, podemos configurar el/los tipo/s de core/s, memoria, etc... pero no customizarlo.

- Las aplicaciones complejas pueden ser difíciles de construir usando una arquitectura sin servidor. Las dependencias entre aplicaciones deben estar muy bien coordinadas.

**¿Qué es un contenedor?**

Según Docker, la idea, es crear contenedores ligeros y portables para las aplicaciones software que puedan ejecutarse en cualquier máquina con Docker instalado, independientemente del sistema operativo que la máquina tenga por debajo, facilitando así también los despliegues.

Es decir, son aplicaciones que contienen todo lo necesarios para ejecutarse sin necesitar dependencias, ni librerías, etc...

**Ventajas de los contenedores**

- Portabilidad. Al tener todo lo necesario en un paquete es más fácil moverse entre proveedores Cloud.

- Se tiene control total sobre su aplicación. Puedes administrar todos los recursos, establecer todas las políticas, supervisar la seguridad y determinar cómo se implementa y se comporta su aplicación, etc...

- Pueden ser tan grandes y complejas como las necesite, ya que no hay limitaciones de memoria o de tiempo de ejecución como ocurre en serverless.

**Inconvenientes de contenedores**

- Requieren  más trabajo para configurar y administrar. Y en cada cambio de la aplicación hay que saber en que contenedor esta, redesplegarlo, etc...

- Necesitan una ubicación. Con los contenedores, se necesita una o varias instancias de servidor y se debe pagar por el uso del servidor aunque estén inactivos.

- Se pueden tener problemas de escalabilidad, ya que se escalan los contenedores y no las aplicaciones. El tener controlado, donde están exactamente, requiere monitorizarlos y dependiendo de nuestra arquitectura, es buscar una aguja en un pajar.

- No hay persistencia de datos cuando los contenedores se vuelven a configurar o se destruyen.

Con estas premisas, ya te puedes hacer una idea de cuando sí y cuando no, debes usar cada tecnología en tu arquitectura/infraestrucutura. Sin embargo, también puedes optar por algo híbrido, ya que puedes tener partes en contenedores y para en serverless, según las necesidades y complejidad de tu aplicación.

Realmente, son tecnologías complementarias más que enfrentadas.

Un saludo y hasta la próxima.
