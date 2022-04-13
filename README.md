# BLUETAB_AWS_CLOUDF_S3_LAMBDA


El repositorio va a contener el codigo bien, .py como .yaml de los codigos usados para crear la función lambda, invocada por medio de CloudFunction, que se encuentra en un Bucket de S3.

Videotutorial: https://drive.google.com/file/d/1vssFoBJGpjf5ld0fok8rhuV426e2_nle/view?usp=sharing


# Descripción del repositorio

En el repositorio se encuetran dos ficheros: 

1. hola.py <- un script de pyton con un esqueleto que imita ya el funcionamietno de un lambda function. 

2. lambdabucket.yalml <- un archivo yalm donde se indica como se va a invocar la funcion hola.py comprimida desde un bucket de S3 de AWS y como se va a ejecutar. 

En el mismo archivo se indican los permisos necesarios para realizar la operación. 

# Pasos para el desarrollo. 

## 1. Creacion de un Bucket en S3: 

Primero de todo necesitamos levantar un entorno donde vamos a alojar el archivo hola.zip (el archivo zipeado de hola.py), por lo que lo creamos. 

A la hora de levantarlo, importante indicar la región de la función, debería de ser la misma de nuestro interés de ejecucción de la función Lambda.

Activamos el versionado del bucket para mantener diferentes variantes del mismo archivo por sea caso y no sobrescribir.

Una vez creado el Bucket, vamos a incluir el archivo zip en el bucket. 

## 2. Creación del CloudFormation: 

Buscamos el servicio de CloudFormation en AWS y levantamos un Stack, vamos a crear un stack with new resources; por lo que a la hora de preparar el template, le indicaremos que el template ya está preparado. 

Es decir, en  nuestro caso lo vamos  a subir desde local. 

Luego, en el template, le indicamos efectivamnte que lo vamos a subir y importamos el archivo 'lambdabucket.yaml'.

Después, a la hora de especificar los detalles: 

1. Stack name: invocamos un nombre específico para nuestro stack. 

2. Parametros: 

A) S3BUCKETPARAM: es el nombre del bucket que acabamos de crear. 

B) S3KEYPARAM: es el nombre "string" + tipoarchivo del archivo que hemos subido al BUCKET de S3 recien creado. En nuestro caso: "hola.zip". 

C) S3OBJECTVERSIONPARAM: es la versión del objeto "hola.zip", para obtenerlo, hacemo click en dicho objeto, vamos a "Version" y copiamos la version ACTUAL. 


Siguiendo con la configuración es posible que tengamos que especificar algunos permisos de IAM, por lo que los activamos con un click. Y esperamos a que el Stack esté preparado, aparecera en verde. 

## 3. Ejecución de Lambda: 

Vamos a los servicios de lambda functions, y actualizamos la pestaña entera. Una vez que se nos refresque tendremos una nueva función creada  hace un tiempo breve. Entramos y la ejecutamos, si todo va bien, nos debería de salir por pantalla el mensaje configurado en hola.py.

:)


