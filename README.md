# examendocker-dns
1.Explica métodos para 'abrir' una consola/shell a un contenedor que se está ejecutando

  1. Docker exec:
    Utiliza el comando docker exec para ejecutar un comando dentro de un contenedor en ejecución

  2. Podman exec:
    Si estás utilizando Podman en lugar de Docker, el proceso es similar al comando docker exec

  3. Docker attach:
    El comando docker attach conecta tu terminal al proceso principal del contenedor. Ten en cuenta que si el proceso principal del contenedor no es un shell interactivo, no podrás interactuar como si fuera una consola.

2. En el contenedor anterior con que opciones tiene que haber sido arrancado para poder interactuar con las entradas y salidas del contenedor

  1. Opción -i (Interactivo):
    Esta opción indica a Docker que mantenga STDIN abierto, incluso si no está conectado, lo que permite la interactividad. Se utiliza en conjunto con -t para asignar un pseudo-TTY.

  2. Opción -t (TTY):
    Asigna un pseudo-TTY, que es necesario para interactuar con la consola del contenedor.

  3. Opción --entrypoint (Punto de entrada):
    Si deseas especificar un comando diferente como punto de entrada (en lugar de utilizar el comando predeterminado definido en la imagen Docker), puedes usar --entrypoint.
  4. Redirección de STDIN, STDOUT, STDERR:
    Asegúrate de que STDIN, STDOUT y STDERR estén conectados. Esto debería ser manejado automáticamente cuando usas las opciones -i y -t.
