# ⁉ Que hace Ollama?

Ollama es la herramienta que nos permitira correr modelos de inteligencia artificial localmente, sin enviar datos a ninguna corporacion y de manera privada.
Lo que haremos es, usando el MCP Server con Wazuh con el index configurado de Grafana, hacer que pueda leer las alertas y eventos que ocurran en Wazuh y NetAlertx

# ⬇️ Instalacion y configuracion de Ollama

En linux Debian en mi caso use el gestor de paquetes APT para instalar Ollama, pero la manera mas practica es usar el comando proporcionado por ellos.  

```text
curl -fsSL https://ollama.com/install.sh | sh
```

Una vez instalado, tenemos la opcion de instalar varios modelos, estos tienen distintos requisitos. Para este caso, las peticiones que haremos no van a ser de una gran carga de recursos, como 
generacion de imagenes o tareas por el estilo, por lo que usaremos **llama3** para este proposito.

```text
ollama pull llama3
```

Lo siguiente sera configurar Wazuh para poder integrarlo.

```text
sudo nano /var/ossec/etc/ossec.conf
```

En el siguiente apartado de las siguientes lineas tienen que estar puestas en **yes**

```text
<global>
  <jsonout_output>yes</jsonout_output>
  <alerts_log>yes</alerts_log>
  <logall>yes</logall>
  <logall_json>yes</logall_json>
</global> 
```

Wazuh necesita almacenar todos los eventos en un archivo JSON, para que el script de IA pueda leerlos. Una vez hecho,
reiniciamos el manager de Wazuh.

```text
sudo systemctl restart wazuh-manager
```

Lo que sigue son algunas dependencias que vamos a necesitar para instalar el script de python que nos permitira hablar con la IA

```text
sudo apt update && sudo apt install python3 python3-pip -y
pip3 install langchain langchain-community langchain-ollama
```

Ahora debemos ir al siguiente directorio de Wazuh para descargar la integracion.

```text
cd /var/ossec/integrations/
git clone https://github.com/Catgarmara/wazuh-security-chat.git
```

Debemos instalar los requisitos de python

```text
pip3 install -r requirements.txt
```

En el archivo **config.py** debemos modificar los siguientes parametros

```text
WAZUH_HOST = "IP"          
WAZUH_PORT = 55000                
WAZUH_USER = "wazuh-wui"          
WAZUH_PASSWORD = "password"  

OLLAMA_HOST = "IP"         
OLLAMA_PORT = 11434               
OLLAMA_MODEL = "modeloDeIA"           

LOG_PATH = "/var/ossec/logs/archives/archives.json" 
```

Para ejecutarlo debemos darle permisos de ejecucion al archivo **run.sh**. Si el puerto que usa, esta ocupado podemos cambiarlo por otro, al ejecutarlo nos deberia abrir una interfaz web, que nos
brinda un chat para hacer las consultas.

## ⚠️ Conclusion y Aclaraciones

De esta manera junto el servidor MCP de Wazuh y Ollama, tenemos una IA que responde en tiempo real los eventos y ocurrencias de nuestra red domestica. Es privada, sin subida de datos a la nube y ligera.
Si se quieren cambiar los prompts para que la IA conteste de otra manera, se pueden modificar dentro del archivo **ai_handler.py**.


