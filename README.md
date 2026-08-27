# 🛡️ SOC hogareño con detecciones en tiempo real y asistente local

---

Este proyecto consiste de un Centro de Operaciones de Seguridad escanea toda la red de mi casa. 

Alerta los cambios como que dispositivos entran y salen, centraliza varios servicios en uno,
pudiendo bloquear ips o aislar hosts.

Documenta a traves de LOGS los movimientos de los usuarios de una maquina y 
todo esto pudiendo ser consultado a un asistente de IA local.

El objetivo es experimentar con mas cercania lo que es un entorno mas realista 
y comprender la utilidad de cada servicio e integracion de ellos

Cada servicio, componente de este proyecto esta documentado y estructurado para su instalacion.

---

## 📋 Objetivos

- Utilizar contenedores Docker.
- Virtualizacion de Windows y Debian.
- Usar IA local y automatizacion .
- Configurar scripts y servicios.
- Documentar todo lo aprendido.

---

## 🧰 Herramientas

- 🐧 Debian 13 
- 🪟 Windows 10 
- 🐦‍⬛ QEMU y VirtManager
- 🐳 Docker y Docker Compose
- 🐍 Python 3
- 🖥️ Bash
- 🖥️ Powershell
- 🐺 Wazuh (Manager + Indexador + Dashboard + MCP Server|)
- 🛜 NetAlertX 
- 🟠 Grafana 
- 🦙 Ollama

---

## 🖥️ Componentes

| Componente | Especificación |
|------------|----------------|
| **CPU** | AMD Ryzen 5 4600G |
| **Memoria RAM** | 16 GB DDR4 |
| **GPU** | AMD Radeon RX 590 8GB |
| **Placa Madre** | MSI B450M A PRO MAX 2 |
| **Almacenamiento** | 1x M.2 1TB |
| **Hipervisor** | QEMU y VirtManager |

## 🗄️ Maquinas Virtuales

| Característica |     Debian 13    |       Windows 10     |
|----------------|------------------|----------------------|
| **Función** | Máquina Host (servidor) | Máquina de pruebas (agente) |
| **Núcleos CPU** | 4 | 4 |
| **Memoria RAM** | 6 GB | 4 GB |
| **Almacenamiento** | 100 GB | 100 GB |

---

## 🔓 Puertos Libres

Wazuh: 55000 (API), 9200 (Indexer), 443 (Dashboard)

NetAlertX: 2020

Grafana: 3000

Ollama: 11434

MCP Server: 3001

---

## 📁 Estructura del repositorio

```
Home-SOC-IA/
├── wazuh/
│ └── README.md
├── netalertx/
│ └── README.md
├── grafana/
│ └── README.md
├── wazuh-mcp-server/
│ └── README.md
├── ollama/
│ └── README.md
└── README.md
```







 
