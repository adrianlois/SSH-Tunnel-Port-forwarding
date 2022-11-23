# SSH-Tunnel-Port-forwarding
Tunnel SSH Port forwarding: Local, Remote, Dynamic

https://www.zonasystem.com/2019/01/tunel-ssh-port-forwarding-local-remote-dynamic.html

## SSH Tunnel: Local port forwarding 

Reenvía un puerto local a un host remoto. Ejemplo de conexión local port forwarding de escritorio remoto RDP realizando pivoting del servidor SSH a otro equipo de la misma red interna. 

Conexión SSH

    ssh -L <puerto-local-escucha>:<host-remoto>:<puerto-remoto> <servidor-ssh>
    ssh -L 9090:192.168.0.10:3389 mi.servidorssh.com

Si el servidor remoto SSH al que nos conectamos para realizar el pivoting del primer salto (mi.servidorssh.com) está expuesto por otro puerto que no sea el 22 por defecto, podemos especificarlo con el parámetro `-p <puerto-servidor-ssh>`.

Escenario:
- Cliente SSH (Red A): 172.16.0.20 
- Servidor SSH (Red B): 192.168.0.15 
- Host RDP (Red B): 192.168.0.10

<p align="center">
<img src="https://raw.githubusercontent.com/adrianlois/SSH-Tunnel-Port-forwarding/master/screenshots/ssh-tunneling-port-forward-local.png" width="740" />
</p>


## SSH Tunnel: Remote port forwarding 

Reenvía un puerto remoto a un host local (reverse port forwarding). Ejemplo de conexión remote port forwarding de escritorio remoto RDP.

Es necesario tener en el lado del servidor SSH habilitada la directiva "GatewayPorts" en /etc/ssh/sshd_config, para permitir que los hosts remotos pueden conectarse a los puertos reenviados para el cliente.

    GatewayPorts yes

Conexión SSH

    ssh -R <puerto-remoto-escucha>:<host-local>:<puerto-local> <servidor-ssh>

    ssh -R 9090:172.168.0.20:3389 mi.servidorssh.com
    o también
    ssh -R 9090:localhost:3389 mi.servidorssh.com

Si el servidor remoto SSH al que nos conectamos para realizar el pivoting del primer salto (mi.servidorssh.com) está expuesto por otro puerto que no sea el 22 por defecto, podemos especificarlo con el parámetro `-p <puerto-servidor-ssh>`.

Escenario:
- Cliente SSH y Host RDP (Red A): 172.16.0.20
- Servidor SSH (Red B): 192.168.0.15
- Client RDP (Red B): 192.168.0.10

<p align="center">
<img src="https://raw.githubusercontent.com/adrianlois/SSH-Tunnel-Port-forwarding/master/screenshots/ssh-tunneling-port-forward-remote.png" width="740" />
</p>


## SSH Tunnel: Dynamic port forwarding 

Utiliza SOCKS.

    ssh -D <puerto-origen-dinámico-escucha> <servidor-ssh>
    ssh -D 9090 mi.servidorssh.com

Si el servidor remoto SSH al que nos conectamos para realizar el pivoting del primer salto (mi.servidorssh.com) está expuesto por otro puerto que no sea el 22 por defecto, podemos especificarlo con el parámetro `-p <puerto-servidor-ssh>`.

Escenario:
- Cliente SSH (Red A): 172.16.0.20
- Servidor SSH (Red B): 192.168.0.15

<p align="center">
<img src="https://raw.githubusercontent.com/adrianlois/SSH-Tunnel-Port-forwarding/master/screenshots/ssh-tunneling-port-forward-dynamic.png" width="740" />
</p>


Configuración SOCKS en Navegador web (Mozilla Firefox).

<p align="center">
<img src="https://raw.githubusercontent.com/adrianlois/SSH-Tunnel-Port-forwarding/master/screenshots/webbrowser-tunel-ssh-dynamic-socks-web.png" width="610" />
</p>
