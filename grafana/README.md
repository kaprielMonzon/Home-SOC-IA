# ⁉️ Que funcion cumple Grafana?

Ayuda a fusionar varios paneles en uno aca, tendremos acceso a los logs de Wazuh y las alertas e ids de NetAlertX.

# ⬇️ Instalacion y configuracion de Grafana

```text
cd /docker/grafana
docker compose up -d
```

El acceso a la interfaz web se hace desde el puerto 3000.

Una vez instalado debemos ingresar a Wazuh e ir al siguiente apartado.

**Security → Internal users → Createinternaluser**

Creamos un usuario para Grafana y un rol

**Security → Roles → Createrole**

Debe tener los siguientes permisos.

**Cluster permissions**

```text
cluster_composite_ops_ro
    
cluster_monitor
```
**Index permissions**

Index patterns: ```text wazuh-* ```

Allowed actions: ```text read ```

Luego debemos asignar rol al usuario

**Security → Roles → grafana_wazuh → Managemapping**

En Users:

```text 
grafana_rol 
```

Configurar el Data Source en Grafana:

1. Connections → Data sources
2. Add data source
3. Seleccionar **elasticsearch**

Configuración:

1. URL: https://IP:9200

2. Auth: Basic

3. User: grafana_rol

4. Password: su contraseña

Lo guardamos y reiniciamos todos los servicios. Con esta configuracion ya tendriamos grafana configurado en solo lectura y con un dashboard configurado.

## ⚠️ Aclaraciones

Esta configuracion hace que Grafana consulte los datos de Wazuh y los muestre en paneles, sin modificar o borrar informacion. Es necesario aclarar que el usuario de **grafana_rol** en Wazuh sea el mismo que
coloquemos en elasticsearch ya que asi podra heredar todas las metricas y permisos que le dimos.

En el apartado de dashboard consegui un modelo personalizado muy bueno en formado json que esta en el repositorio.
