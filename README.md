# zabbix

# 📊 Implementación de un Sistema de Monitorización con Zabbix

**Autor:** Alejandro  
**Proyecto:** Despliegue, configuración y puesta en marcha de un entorno de monitorización híbrido (Agente + SNMP).

---

## 🚀 1. Descripción del Proyecto
Este repositorio contiene la documentación y el guion de demostración para el despliegue de un servidor Zabbix. El objetivo principal es establecer un sistema capaz de monitorizar tanto servidores Linux (vía Zabbix Agent) como dispositivos de red (vía protocolo SNMP), garantizando la persistencia de datos a través de una base de datos relacional y priorizando la seguridad en las configuraciones.

### Entorno Técnico:
* **Sistema Operativo:** Ubuntu 22.04
* **Base de Datos:** MariaDB 10.6.22
* **Servidor Web:** Apache2
* **Motor de Monitorización:** Zabbix Server & Zabbix Agent

---

## 💻 2. Guion de la Demostración (Paso a Paso)

A continuación, se detalla el flujo de la demostración técnica en vivo:

### Fase 1: Verificación del Motor y Servicios (Terminal)
Para demostrar que el "back-end" está operativo, comprobamos el estado de los servicios críticos y los puertos de escucha:

1. **Estado de los servicios (Active/Running):**
   ```bash
   sudo systemctl status zabbix-server zabbix-agent apache2 mariadb
