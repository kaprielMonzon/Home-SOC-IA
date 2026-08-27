# Instalacion y configuracion de NetAlertX

Primero debemos instalar docker y crear un almacenamiento persistente

```text
sudo install -d -o 20211 -g 20211 -m 0750 /opt/netalertx/data
cd /opt/netalertx
sudo docker compose config
sudo docker compose up -d
```
