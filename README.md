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

2. **Comprobación de puertos (10050 y 10051):**
   ```bash
   sudo ss -tulpn | grep zabbix

### Fase 2: Arquitectura de Datos (MariaDB)

Zabbix depende de una estructura robusta para almacenar el histórico. Se demuestra la conexión y estructura de la base de datos:

    Acceso y verificación de tablas:

    sudo mysql -u root -p
    use zabbix;
    show tables;

### Fase 3: Monitorización Híbrida (Interfaz Web Zabbix)

Desde http://localhost/zabbix, pasamos a la gestión de la infraestructura en Data collection -> Hosts.

    Nodos por Agente (Verde / ZBX): Se muestran el Zabbix server y el Nodo-Secundario. El estado en verde confirma que el agente local responde correctamente por el puerto 10050 en tiempo        real.

    Nodos por Red (Rojo / SNMP): Se muestra el Router-Principal-SNMP. El estado rojo demuestra el correcto funcionamiento del sistema de alertas (Timeout), ya que verifica la inaccesibilidad     de un dispositivo de red configurado por el puerto 161 sin agente instalado.


### Fase 4: Seguridad y Visualización

    Gestión de Macros: Demostración de buenas prácticas de seguridad evitando contraseñas en texto plano. Uso de la macro global {$SNMP_COMMUNITY} con valor public para centralizar credenciales y facilitar la escalabilidad.

    Dashboards Dinámicos: Visualización del panel de control principal mostrando widgets de carga de CPU, uso de memoria y métricas del servidor web Apache, permitiendo la toma de decisiones basada en datos reales.


---

## Acción 1: Crear el Servidor de Monitorización (Con Apache)

 Data collection -> Hosts y le das al botón azul Create host.


    Host name:  Servidor-Principal-Demo.

    Templates: 
        Zabbix server health (Para monitorizar el motor interno).

        Linux by Zabbix agent (Para monitorizar la CPU/RAM del sistema operativo).

        Apache by HTTP (Para monitorizar el servicio web).

    Host groups:  Zabbix servers.

    Interfaces: Add -> Agent.

         IP 127.0.0.1 

        Deja el puerto en 10050.

    Haz clic en el botón azul Add.

## Acción 2: Crear el Nodo Normal (Relacionado)

Create host


    Host name: Escribe Nodo-Secundario-Demo.

    Templates: Linux by Zabbix agent. 

    Host groups: Linux servers.

    Interfaces: Add -> Agent.

      IP de tu red
      
      puerto en 10050.

    
