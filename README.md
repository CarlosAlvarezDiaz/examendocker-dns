# examendocker-dns
1.Explica métodos para 'abrir' una consola/shell a un contenedor que se está ejecutando

  1. Docker exec:
    Utiliza el comando docker exec para ejecutar un comando dentro de un contenedor en ejecución

  2.Podman exec:
    Si estás utilizando Podman en lugar de Docker, el proceso es similar al comando docker exec

  3. Docker attach:
    El comando docker attach conecta tu terminal al proceso principal del contenedor. Ten en cuenta que si el proceso principal del contenedor no es un shell interactivo, no podrás interactuar como si fuera una consola.

2. En el contenedor anterior con que opciones tiene que haber sido arrancado para poder interactuar con las entradas y salidas del contenedor

