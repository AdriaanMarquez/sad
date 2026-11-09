# Respuestas · Práctica 2 · Bodegas Atlántico

> Rellena este fichero en tu ordenador. Va en la entrega (`./lab.sh entregar`) y en la defensa te pueden preguntar por él.

## Bloque A · Piensa como un atacante (nmap)

Desde la calle: `./lab.sh cliente` y dentro `nmap -Pn -p 22,80,443,5432,8080 198.51.100.254`. Pega la salida:

```text
Starting Nmap 7.95 ( https://nmap.org ) at 2026-11-09 15:01 UTC
Nmap scan report for sad-p2-fw.sad-p2_calle (198.51.100.254)
Host is up (0.000062s latency).

PORT     STATE    SERVICE
22/tcp   filtered ssh
80/tcp   open     http
443/tcp  open     https
5432/tcp filtered postgresql
8080/tcp filtered http-proxy
MAC Address: 26:7E:E9:29:AD:3E (Unknown)

Nmap done: 1 IP address (1 host up) scanned in 1.30 seconds

```

## Bloque A · El contador

Después de `./lab.sh comprobar`, mira `./lab.sh ver`. ¿Cuántos paquetes lleva el contador de A6? ¿Quién los ha mandado?

>

## Bloque B · La prueba del cifrado

En el firewall (`./lab.sh fw`): `tcpdump -ni wan host 198.51.100.62 -c 6`. Mientras, en otra terminal, el comercial
(`./lab.sh comercial`) hace `curl http://172.16.10.20:8080`. Pega lo que sale en el firewall:

```text
tcpdump: verbose output suppressed, use -v[v]... for full protocol decode
listening on wan, link-type EN10MB (Ethernet), snapshot length 262144 bytes
15:52:28.951518 IP 198.51.100.62.53931 > 198.51.100.254.51820: UDP, length 96
15:52:28.951669 IP 198.51.100.254.51820 > 198.51.100.62.53931: UDP, length 96
15:52:28.951689 IP 198.51.100.62.53931 > 198.51.100.254.51820: UDP, length 148
15:52:28.951753 IP 198.51.100.62.53931 > 198.51.100.254.51820: UDP, length 96
15:52:28.951801 IP 198.51.100.62.53931 > 198.51.100.254.51820: UDP, length 176
15:52:28.951859 IP 198.51.100.254.51820 > 198.51.100.62.53931: UDP, length 96
6 packets captured
13 packets received by filter
0 packets dropped by kernel
```

En dos líneas: ¿qué se ve por la calle y qué NO se ve?

>Por la calle solo viaja tráfico cifrado UDP por el puerto 51820 entre las IPs públicas, sin dejar ver el contenido de los datos ni permitir accesos no autorizados gracias al filtrado estricto por la IP de cada túnel.

## Bloque C · Para la defensa (C4)

Del **mismo ataque** (la inyección a la web): ¿qué ve el vigilante de la red (el IDS) y qué ve el portero de la web? ¿Por
qué hacen falta los dos?

>

## Bloque D · La nota del servidor (D0 y D4)

Nota del análisis **antes** de bastionar (D0):

>

Nota **después** (D4). ¿Por qué no llega a 100? ¿Significa que el servidor sigue inseguro? Comenta un aviso que siga saliendo.

>
