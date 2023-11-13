# examendocker-dns
1.Explica métodos para 'abrir' una consola/shell a un contenedor que se está ejecutando

  a. Docker exec:
    Utiliza el comando docker exec para ejecutar un comando dentro de un contenedor en ejecución

  b. Podman exec:
    Si estás utilizando Podman en lugar de Docker, el proceso es similar al comando docker exec

  c. Docker attach:
    El comando docker attach conecta tu terminal al proceso principal del contenedor. Ten en cuenta que si el proceso principal del contenedor no es un shell interactivo, no podrás interactuar como si fuera una consola.

2. En el contenedor anterior con que opciones tiene que haber sido arrancado para poder interactuar con las entradas y salidas del contenedor

  a. Opción -i (Interactivo):
    Esta opción indica a Docker que mantenga STDIN abierto, incluso si no está conectado, lo que permite la interactividad. Se utiliza en conjunto con -t para asignar un pseudo-TTY.

  b. Opción -t (TTY):
    Asigna un pseudo-TTY, que es necesario para interactuar con la consola del contenedor.

  c. Opción --entrypoint (Punto de entrada):
    Si deseas especificar un comando diferente como punto de entrada (en lugar de utilizar el comando predeterminado definido en la imagen Docker), puedes usar --entrypoint.
    
  d. Redirección de STDIN, STDOUT, STDERR:
    Asegúrate de que STDIN, STDOUT y STDERR estén conectados. Esto debería ser manejado automáticamente cuando usas las opciones -i y -t.

3. ¿Cómo sería un fichero docker-compose para que dos contenedores se comuniquen entre si en una red solo de ellos?

  version: '3'

services:
  servicio1:
    image: nombre_de_imagen_servicio1
    networks:
      - red_privada

  servicio2:
    image: nombre_de_imagen_servicio2
    networks:
      - red_privada

networks:
  red_privada:
    driver: bridge

  Se definen dos servicios (servicio1 y servicio2) que utilizan imágenes específicas (nombre_de_imagen_servicio1 y nombre_de_imagen_servicio2). Puedes reemplazar estos nombres con las imágenes que estás utilizando.

  Ambos servicios están conectados a una red llamada red_privada mediante la clave networks.

  La red red_privada se define al final del archivo y utiliza el controlador de red bridge. Esto crea una red privada a la que solo los servicios especificados tienen acceso.

4. ¿Qué hay que añadir al fichero anterior para que un contenedor tenga la IP fija?

   version: '3'

services:
  servicio1:
    image: nombre_de_imagen_servicio1
    networks:
      red_privada:
        ipv4_address: 172.16.0.2

  servicio2:
    image: nombre_de_imagen_servicio2
    networks:
      red_privada:
        ipv4_address: 172.16.0.3

networks:
  red_privada:
    driver: bridge
    ipam:
      driver: default
      config:
        - subnet: 172.16.0.0/24


  En el servicio servicio1, se ha añadido la clave ipv4_address dentro de la sección networks. Esto asigna la dirección IP 172.16.0.2 al contenedor servicio1.

  Similarmente, en el servicio servicio2, se ha añadido la clave ipv4_address para asignar la dirección IP 172.16.0.3.

  En la sección networks, se utiliza ipam (IP Address Management) para configurar el rango de direcciones IP disponibles. En este caso, se ha especificado la subred 172.16.0.0/24.

5. ¿Que comando de consola puedo usar para saber las ips de los contenedores anteriores? Filtra todo lo que puedas la salida. El comando no es "ip a", tiene que ser desde fuera del contenedor.

  docker inspect --format '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' nombre_del_contenedor

  Para saber la ip de el contenedor que quieres debes cambiar 'nombre_del_contenedor' por el nombre de dicho contenedor que desees usar.

6. ¿Cual es la funcionalidad del apartado "ports" en docker compose?

   La sección ports en un archivo Docker Compose se utiliza para especificar la exposición de puertos del contenedor al host. Permite mapear puertos del contenedor a puertos específicos en el host, lo que facilita el acceso a los servicios que se
   ejecutan dentro del contenedor desde el exterior.

7. ¿Para que sirve el registro CNAME? Pon un ejemplo

     El registro CNAME (Canonical Name) se utiliza en el sistema de nombres de dominio (DNS) para asociar un nombre de dominio con otro. Básicamente, un CNAME actúa como un alias de otro nombre de dominio, permitiendo que un nombre de dominio se
     refiera a otro dominio sin tener que duplicar la información de resolución de nombres.

     www.ejemplo.com     IN   A      192.168.1.1
     blog.ejemplo.com    IN   CNAME  www.ejemplo.com

     En este ejemplo:

     www.ejemplo.com tiene una dirección IP directa (A record) asociada con ella.
     blog.ejemplo.com se configura como un alias (CNAME) de www.ejemplo.com.

8. ¿Como puedo hacer para que la configuración de un contenedor DNS no se borre si creo otro contenedor?

   Para persistir la configuración de un contenedor DNS entre diferentes instancias o reinicios, puedes utilizar volúmenes en Docker. Los volúmenes son una forma de almacenar y compartir datos entre contenedores y con el sistema host.

9.logs ![imagen](https://github.com/CarlosAlvarezDiaz/examendocker-dns/assets/144815112/257b9672-5930-46ea-9956-8c99a2c298eb)

dig ![imagen](https://github.com/CarlosAlvarezDiaz/examendocker-dns/assets/144815112/237f5593-7eb3-46a5-9535-e577e3b8ccaa)


