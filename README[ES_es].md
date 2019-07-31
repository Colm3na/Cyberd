<h1 align="center"> Cyberd </h1>

<p align="center"> 
<img src="./images/logo.png">
</p>


En este repositorio puedes encontrar algunos scripts para gestionar el nodo de [Cyberd](https://github.com/cybercongress/cyberd/blob/master/docs/cyberd.md) .

Si quieres saber algo más [este](https://github.com/cybercongress/cyberd) es su repositorio, [aquí](https://github.com/cybercongress/cyberd/tree/master/docs) puedes encontrar más documentación de Cyberd, [aquí](https://github.com/cybercongress/cyberd/blob/master/docs/run_validator.md) como ser validador en Cyberd, y este es su [hub oficial](https://hub.docker.com/r/cyberd/cyberd) de Docker.

[Este](https://t.me/fuckgoogle) es su grupo de telegram, [esta](https://twitter.com/cyber_devs) es su cuenta de Twitter y [esta](https://cybercongress.ai/) su web y el blog.

Con estos scripts puedes manejar el docker del validador.

> **Recuerda que necesitas cambiar los valores de los scripts por los tuyos**.

> **Si necesitas algún script y no esta en este repositorio, puedes hacer un PR o abrir una ISSUE con lo que necesites**.

> _Si tienes algún problema siempre puedes pasar por la [Colmena](https://www.coworkingcolmena.com) para preguntar y aprender lo que necesites_.


<sumary>
<h1 align="center"> Cómo usarlo: </h1>

</sumary>
<details>

- Necesitas instalar <a href="https://github.com/stedolan/jq/wiki"> jq</a>:

```
sudo apt install -y jq
```

- Clona el repositorio:

```
git clone https://github.com/Colm3na/Cyberd.git
```

- Dirígete a la carpeta [scripts](./scripts/), y dale permisos de ejecución:

```
cd scripts/
```

```
chmod +x *
```

- Usa el script que necesites:

```
./balance
```
</details>

<sumary>
<h2 align="center"> Crawler: </h1>

</sumary>
<details>

- <h3>Clona el repositorio:</h3>
```
git clone https://github.com/cybercongress/crawler
```

- Ya deberíamos tener Go 1.12+ instalado, necesitamos cyberd ya corriendo para usarlo con crawler.

---

<sumary>
  <h3 align="center">Instalación de Go y el nodo de IPFS</h3>

</sumary>
<details>
  
>Si necesitas instalar Go, puedes ir a [esta guía.](https://github.com/Colm3na/Cosmos/blob/master/testnets/Instalación%20de%20un%20nodo%20de%20Cosmos%20en%20Gaia-13004%5BES_es%5D.md#instalamos-la-última-versión-de-go)

>Para instalar un nodo de IPFS:

`sudo snap install ipfs`

>Iniciamos IPFS:

`ipfs init`

>Dejamos el demonio corriendo:

`ipfs daemon` 
</details>

---

- Para instalarlo hacemos:
```
cd crawler
go build -o crawler
```

- <h3>Requisitos:</h3>

Tal y como se especifica en el repositorio original, necesitamos 3 cosas para usar crawler:

1. El daemon de ipfs corriendo. Lo arrancamos con el comando `ipfs daemon`.

2. Descargarnos enwiki-latest-all-titles al directorio raíz del crawler:
```
ipfs get QmddV5QP87BZGiSUCf9x9hsqM73b83rsPC6AYMNqkjKMGx -o enwiki-latest-all-titles
```

3. Cyberd corriendo con una cuenta de la que tengamos la contraseña.

- <h3>Uso:</h3>

Crawler tiene dos funciones: parsear los títulos de la wiki y enviar links entre las palabras claves y las páginas de la wiki, y la segunda subir archivos o DURAS al nodo de IPFS local.

1. Para la primera función, simplemente abrimos un `tmux` y corremos este comando como sudo:
```
sudo ./crawler submit-links-to-cyber ./enwiki-latest-all-titles --home=<path-to-cyberdcli> --address=<account> --passphrase=<passphrase> --chunk=100
```
El parámetro `--home`, si hemos instalado nuestro cyberd siguiendo la guía oficial, será `--home=/cyberd/cli/`.

Desgraciadamente, nos obliga a escribir la contraseña en texto plano que encripta nuestra wallet de cyberd en `passphrase`.

2. Para la segunda función, igualmente en un `tmux`, ejecutamos:
```
./crawler upload-duras-to-ipfs enwiki-latest-all-titles
```

Para saber qué es un DURA, aquí encontraréis toda la información: https://github.com/cybercongress/cyb/blob/dev/docs/dura.md

- <h3>Bandwidth:</h3>

Crawler consume puntos de bandwidth para crear los links. Estos puntos se regeneran con el tiempo y también dependiendo de nuestra cantidad de CYBs.

Después de generar una serie de links, veremos el mensaje `Low bandwidth. Sleep for 14.081µs seconds`. Entonces sólo cabrá esperar o bien conseguir más CYBs.

</details>
