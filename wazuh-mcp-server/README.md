## ⁉️ En que consiste Wazuh MCP-Server

Es un servidor MCP (protocolo de contexto para modelos) sirve como puente de nuestro centro de seguridad Wazuh y
la IA local que tengamos instalada. 

## ⚙️ Instalacion y configuracion de Wazuh MCP-Server

Primero nos clonamos este repositorio

```text
git clone https://github.com/adi5353/wazuh-mcp.git
cd wazuh-mcp
```

## ⚠️ Aviso

Deben tener a mano las credenciales de su usuario admin del indexer y de la API, en caso de no conseguir las de la API
deberian estar en esta ubicacion dentro del servidor.

```text
/usr/share/wazuh-dashboard/data/wazuh/config/wazuh.yml
```

Instalamos las dependencias 

```text
pip install -r requirements.txt
```

Modificamos las variables de entorno con nuestros usuarios y contraseñas

```text
cp env.example .env
nano .env
```

Finalmente levantamos el contenedor

```text
docker compose up -d
```

## 🧠 Conclusion 

Con el MCP ya configurado, tenemos acceso al indexer (elasticsearch) y a la api de wazuh, podriamos finalizar con la instalacion de Ollama, un modelo ligero de IA, para despues hacer un script
para las posibles consultas de alguna ip o evento que se haya hecho en la red y este nos hara un resumen de lo ocurrido en tiempo real.

