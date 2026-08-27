# Instalacion y configuracion de Wazuh

La siguiente guia es para la maquina Linux y Windows.

IP Linux: 192.168.1.78
IP Windows: 192.168.79

## Linux

Con los siguientes comandos nos traemos e instalamos el cliente

```text
curl -sO https://packages.wazuh.com/4.14/wazuh-install.sh
sudo bash ./wazuh-install.sh -a
```

Al finalizar la instalacion nos deberian de dejar unas credenciales para acceder
al panel.

Para acceder a la interfaz de Wazuh entramos por la ip de linux https://192.168.1.78/

Despues vamos a generar un agente que va a ser nuestra VM de Windows 10

```text
sudo /var/ossec/bin/manage_agents
```

La clave nos la guardamos para mas adelante al instalar wazuh en Windows

Una vez instalado verificamos el estado de los servicios que corre el programa

```text
sudo systemctl status wazuh-manager --no-pager
sudo systemctl status wazuh-indexer --no-pager
sudo systemctl status wazuh-dashboard --no-pager
```

En mi caso instale **Uncomplicated Firewall (ufw)** para la correcta comunicacion de los puertos e ips.

```text
sudo ufw allow 443/tcp         # HTTPS (Panel de wazuh y otros paneles)
sudo ufw allow 1514/tcp        # Agente de Wazuh
sudo ufw allow 1515/tcp        # Registro del agente
sudo ufw allow 55000/tcp       # API
sudo ufw allow 9200/tcp        # Wazuh Indexador
```

Editamos un archivo yaml fundamental para el indexador con los siguientes valores

```text
sudo nano /etc/wazuh-indexer/opensearch.yml
```

```text
network.host: "192.168.1.78"
http.port: 9200
```
## Windows

Descargamos el cliente en el siguiente enlace

```text
https://documentation.wazuh.com/current/installation-guide/wazuh-agent/wazuh-agent-package-windows.html
```

Al finalizar la instalacion, pegamos la clave del agente y abrimos el siguiente archivo de configuracion llamado **ossec** y pegamos la siguiente
linea con el directorio que nosotros queremos que sea monitorizada.

```text
<directories check_all="yes" report_changes="yes" realtime="yes" recursion_level="5">C:\Users\kapriel</directories>
```

```text check_all="yes"``` revisa permisos, dueño, fechas, tamaño, etc.

```text report_changes="yes"``` guarda y muestra que lineas cambiaron en archivos de texto.

```text realtime="yes"``` detecta cambios al instante.

```text recursion_level="0"``` solo vigila esa carpeta, no entra en subcarpetas.


## Conclusion y aclaraciones

Con esta serie de pasos tenemos instalado Wazuh en la maquina Debian que actua como servidor y anfitrion.
Y la maquina Windows como maquina de prueba para ser monitorizada. 

Si se quiere monitorear mas carpetas dentro del directorio de Windows deberiamos cambiar el parametro de recursion level
de un 0 a un numero mas elevado como 3, que escanearia a 3 subcarpetas hacia adentro, pero se debe de hacer con precaucion ya que esto consume recursos a niveles mas altos,
no se deberia de hacer con todos los directorios.
