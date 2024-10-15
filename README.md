<h1>Docker network</h1>


<h2>1-Crear unha rede en docker</h2>

    docker network create mired

Isto crea unha rede chamada mired.


<h2>2-Crear dous contenedores unidos a esa rede</h2>

    docker run -dit --name c1 --network mired ubuntu

    docker run -dit --name c2 --network mired ubuntu
    
Con estes comandos crearemos dous contenedores chamados c1 e c2 respectivamente e estaran unidos a rede que creamos antes.


<h2>3-Comprobar que os contenedores están na rede</h2>

    docker network inspect mired

O comando mostra a configuracion de rede, incluidos o contenedores unidos.


<h2>4-Comprobar que os contenedores poden verse entre eles</h2>

    docker exec c1 ping -c 3 c2

Con este comando c1 e c2 mandaranse 3 paquetes para ver se fan ping.

<h2>5-Listar os contenedores conectados á rede</h2>

     docker network inspect mired
     
O comando mostra a configuracion de rede, incluidos o contenedores unidos.

<h2>6-Listar as propiedades da rede</h2>

    docker network inspect mired
     
O comando mostra a configuracion de rede, incluidos o contenedores unidos.

<h2>7-Crea outra rede</h2>

    docker network create mired2

Isto crea unha rede chamada mired2.

<h2>8-Lanza dous contenedores novos conectados a esa nova rede</h2>

    docker run -dit --name c3 --network mired2 ubuntu

    docker run -dit --name c4 --network mired2 ubuntu
    
Con estes comandos crearemos dous contenedores chamados c3 e c4 respectivamente e estaran unidos a rede que creamos antes.

<h2>9-Comproba as posibles conexións entre os 4 contenedores</h2>

    docker exec c1 ping -c 3 c2
    
Con este comando veremos se c1 e c2 fan ping, cousa que xa vimos anteriormente.

    docker exec c3 ping -c 3 c4

Con este comando veremos se c3 e c4 fan ping.

    docker exec c1 ping -c 3 c4
    
Con este comando veremos se c1 e c4 fan ping. Como xa vimos antes c1 e c2 haran ping xa que estan na mesma rede, isto pasase igual con c3 e c4, pero c1 e c4 non daran ping debido a que estan en redes distintas.


<h1>Docker compose:</h1>


<h2>Segue os pasos da guía de iniciación de docker-compose, e explica coas túas palabras os pasos que segues e qué fan</h2>

<h2>Paso 1: Configuración inicial</h2>
<p class="bold">Crear un directorio para o proxecto:</p>
<ul>
    <li>Créase unha carpeta chamada composetest para almacenar os arquivos do proxecto.</li>
    <li>Crear o arquivo app.py:
        <ul>
            <li>Este arquivo contén o código dunha aplicación web en Python usando Flask.</li>
            <li>A aplicación ten un contador que conta cantas veces se accedeu á páxina, almacenando este dato nun servizo Redis.</li>
            <li>Redis é un almacén de datos en memoria que se usará para gardar o número de visitas.</li>
        </ul>
    </li>
    <li>Crear o arquivo requirements.txt:
        <ul>
            <li>Este arquivo lista as dependencias que necesita a aplicación (flask e redis), as cales se instalarán máis adiante.</li>
        </ul>
    </li>
    <li>Crear un Dockerfile:
        <ul>
            <li>Especifica como construir a imaxe de Docker para a aplicación.</li>
            <li>Inclúe pasos como copiar os arquivos ao contedor, instalar dependencias, expoñer un porto para a aplicación e configurar o comando para executar a aplicación.</li>
        </ul>
    </li>
</ul>

<h2>Paso 2: Definir os servizos nun arquivo Compose</h2>
<p class="bold">Crear o arquivo compose.yaml:</p>
<ul>
    <li>Este arquivo define os servizos que se executarán con Docker Compose.</li>
    <li>Inclúe dous servizos:
        <ul>
            <li>Web: A aplicación web que se constrúe a partir do Dockerfile.</li>
            <li>Redis: Utiliza unha imaxe de Redis preconstruída dende Docker Hub.</li>
        </ul>
    </li>
</ul>

<h2>Paso 3: Construír e executar a aplicación con Compose</h2>
<p class="bold">Executar docker compose up:</p>
<ul>
    <li>Con un só comando, créanse e iníciase os servizos definidos en <strong>compose.yaml</strong>.</li>
    <li>Isto inclúe a creación dunha rede predeterminada para a comunicación entre os servizos.</li>
</ul>

<h2>Paso 4: Editar o arquivo Compose para usar "Compose Watch"</h2>
<p class="bold">Engadir soporte para "watch" no arquivo compose.yaml:</p>
<ul>
    <li>Isto permite que os cambios nos arquivos se sincronicen automáticamente co contedor, sen necesidade de reiniciar manualmente.</li>
</ul>

<h2>Paso 5: Volver a construir e executar a aplicación</h2>
<p class="bold">Usar docker compose watch ou docker compose up --watch:</p>
<ul>
    <li>Executa a aplicación e habilita a sincronización automática de arquivos, o que facilita o desenvolvemento.</li>
</ul>

<h2>Paso 6: Actualizar a aplicación</h2>
<p class="bold">Modificar o mensaxe en app.py e gardar os cambios:</p>
<ul>
    <li>Cando se garda o arquivo, a aplicación actualízase automáticamente no contedor, grazas á sincronización habilitada.</li>
</ul>

<h2>Paso 7: Dividir os servizos en varios arquivos Compose</h2>
<p class="bold">Crear un novo arquivo infra.yaml:</p>
<ul>
    <li>Mover o servizo Redis a este arquivo para modularizar a configuración.</li>
    <li>Actualízase compose.yaml para incluír o novo arquivo.</li>
</ul>

<h2>Paso 8: Experimentar con outros comandos</h2>
<p class="bold">Correr os servizos en modo "detached" -d:</p>
<ul>
    <li>Isto permite executar os servizos en segundo plano.</li>
    <li>Usar docker compose ps para ver os servizos en execución.</li>
    <li>Deter os servizos con docker compose stop ou eliminalos con docker compose down.</li>
</ul>


<h2>Agora que sabes algo máis de docker-compose, crea un arquivo (ou varios arquivos) de configuración que ó ser lanzados cun docker-compose up, resulten nunha rede docker á que estean conectados 3 contenedores, explica os parámetros do .yaml usado</h2>

Versión: Isto indica a versión de Docker Compose que estou utilizando.

Servizos: Esta sección define os diferentes contedores que se executarán. No meu caso, definín tres servizos: web1, web2 e web3.

web1, web2, web3: Cada un destes é un servizo que representa un contedor de Nginx.

imagen: nginx Utilizo a imaxe oficial de Nginx.

container_name: nome do contedor

redes: Indica as redes ás que se conectará o contedor.

ports: Mapea un porto do host ao porto do contedor.

restart: always: Este parámetro indica que o contedor reiniciarase automáticamente se se detén.

volumes: Monta un directorio do host nun directorio do contedor.

redes: Aquí define as redes que usarán os contedores.

mi_red: É o nome da rede que creei. O driver bridge é o predeterminado e permite a comunicación entre contedores na mesma rede.

<h2>Busca e proba 4 parámetros e configuracións diferentes que podes incluir no arquivo compose, explica qué fan. (por exemplo diferentes cousas que facer coa opción RUN)</h2>

Environment: Establece variables de entorno que poden ser utilizadas pola aplicación dentro do contedor.

depends_on: Este parámetro especifica que un servizo depende doutro, garantindo que se inicie na orde correcta.

build: Se necesitas crear unha imaxe personalizada, podes especificar o contexto de construción.

healthcheck: Podes definir un control de saúde para monitorizar o estado do contedor.

