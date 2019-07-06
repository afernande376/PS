
Los documentos los he hecho en local utilizando un editor de Markdown en mi equipo sobre un repositorio sincronizado con Github. Al finalizar los documentos los actualizo mediante comandos git en mi equipo. Aquí está la lista de pasos que he seguido. 

> Reflexión posterior: quizás sea mejor escribir la documentanción en la Wiki del repositorio, y meter el código en <>Code, en este caso, los scripts de powershell que genere?

[Guía rápida MarkDown](https://rogerdudler.github.io/git-guide/index.es.html)

Los pasos a seguir para subir documentos a GitHub es la siguiente:


1.	Crear un repositorio en GitHub a través de la web. 

2.	Crear una carpeta en el PC local que será la que va a estar sincronizada con Github:

```
mkdir repositorio
cd repositorio
```
3.	Inicializar el repositorio para que Github tome control de él. `git init`

4.	Clonar el repositorio remoto en el local (esto lo ves cuando creas el repositorio en la web).
`git remote add origin git@github.com:afernande376/PS.git`

5.	Crear en el repositorio local los ficheros que queramos, crear carpetas, hacer modificaciones. 

6.	Añadir los ficheros que queramos subir al servidor. Si queremos todos ponemos “*”
`git add *`

7.	Hacer un commit para ponermos en “posición de salida”. 
`git commit -m "updated"`

8.	Por último hacer un push del origen (nuestro PC) a la rama remota que queramos. En nuestro caso será master pues no estamos trabajando en grupo ni con releases de software. 
`git push -u origin master`
