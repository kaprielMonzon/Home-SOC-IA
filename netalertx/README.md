# ⁉️ Que hace NetAlertX?

Es un escáner de red que monitorea todos los dispositivos conectados a tu red local, es un buen complemento para Wazuh, ya que NetAlertX identifica por
direccion MAC, Ip, Fabricante y nombre, se le pueden asignar varios campos. Detecta nuevos dispositivos y lanza alertas si aparece uno nuevo.

---

## ⬇️ Instalacion y configuracion de NetAlertX

## ⚠️️ Aviso 

En el contenedor antes de levantarlo deberian revisar si la interfaz es la misma **eth0**, sino remplazarla con la que
ya tienen. Una vez aclarado debemos instalar docker.

```text
cd /docker/netalertx
sudo docker compose config
sudo docker compose up -d
```

Para ingresar a la interfaz web se accede a traves del puerto 20211, al entrar veran una lista de dispositivos conectados, que pertenecen
a su red local, para integrarlo junto a Wazuh debemos instalar Grafana.
