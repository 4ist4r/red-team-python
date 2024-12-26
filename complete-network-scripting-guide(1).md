[Contenido anterior del documento se mantiene igual hasta la Conclusión...]

## 6. Ejercicios Prácticos

### 6.1. Nivel Principiante

#### Ejercicio 1: Socket Básico
**Objetivo**: Crear un cliente TCP simple que se conecte a un servidor web.
```python
# Tarea: Completa el siguiente código para:
# 1. Conectarte a www.ejemplo.com en el puerto 80
# 2. Enviar una petición HTTP GET básica
# 3. Recibir y mostrar la respuesta

import socket

def cliente_web_simple():
    # Tu código aquí
    pass

# Bonus: Añade manejo de errores básico
```

#### Ejercicio 2: Requests Inicial
**Objetivo**: Crear un verificador de estado de sitios web.
```python
# Tarea: Crea un script que:
# 1. Tome una lista de URLs
# 2. Verifique si cada sitio está activo
# 3. Muestre el código de estado HTTP de cada uno

import requests

def verificar_sitios(urls):
    # Tu código aquí
    pass

# Bonus: Añade timeouts y manejo de excepciones
```

#### Ejercicio 3: Paramiko Simple
**Objetivo**: Conectarse a un servidor SSH y ejecutar comandos básicos.
```python
# Tarea: Desarrolla un script que:
# 1. Se conecte a un servidor SSH local
# 2. Ejecute el comando 'ls'
# 3. Muestre el resultado

import paramiko

def ssh_basico():
    # Tu código aquí
    pass

# Bonus: Implementa la lectura de credenciales desde un archivo
```

### 6.2. Nivel Intermedio

#### Ejercicio 4: Scanner de Puertos Multihilo
**Objetivo**: Crear un scanner de puertos que utilice threading para mayor velocidad.
```python
# Tarea: Implementa un scanner que:
# 1. Utilice múltiples hilos
# 2. Escanee un rango de puertos
# 3. Identifique servicios comunes
# 4. Muestre el progreso en tiempo real

import socket
import threading
import queue

def port_scanner_thread():
    # Tu código aquí
    pass

# Bonus: Añade detección de banner y gestión de timeouts
```

#### Ejercicio 5: Monitor de Red con Scapy
**Objetivo**: Crear un monitor de tráfico de red básico.
```python
# Tarea: Desarrolla un script que:
# 1. Capture paquetes en tiempo real
# 2. Filtre por protocolo (TCP/UDP/ICMP)
# 3. Muestre estadísticas básicas
# 4. Guarde los resultados en un archivo

from scapy.all import *

def monitor_red():
    # Tu código aquí
    pass

# Bonus: Añade detección de patrones de tráfico sospechoso
```

#### Ejercicio 6: Automatización SSH Masiva
**Objetivo**: Gestionar múltiples servidores SSH simultáneamente.
```python
# Tarea: Crea un script que:
# 1. Lea una lista de servidores desde un archivo
# 2. Se conecte a cada uno
# 3. Ejecute una serie de comandos
# 4. Recopile los resultados

import paramiko
import concurrent.futures

def gestion_masiva_ssh():
    # Tu código aquí
    pass

# Bonus: Implementa verificación de cambios y rollback
```

### 6.3. Nivel Avanzado

#### Ejercicio 7: Sistema de Detección de Intrusos
**Objetivo**: Crear un IDS básico usando Scapy.
```python
# Tarea: Implementa un sistema que:
# 1. Monitoree el tráfico de red
# 2. Detecte patrones de ataque conocidos
# 3. Genere alertas
# 4. Mantenga un log de eventos
# 5. Permita configurar reglas personalizadas

from scapy.all import *
import logging
import yaml

class IDS:
    def __init__(self):
        # Tu código aquí
        pass

    def cargar_reglas(self):
        # Tu código aquí
        pass

    def analizar_paquete(self, paquete):
        # Tu código aquí
        pass

# Bonus: Añade machine learning para detección de anomalías
```

#### Ejercicio 8: Framework de Pruebas de Penetración
**Objetivo**: Crear un framework modular para pruebas de seguridad.
```python
# Tarea: Desarrolla un framework que:
# 1. Realice reconocimiento automático
# 2. Ejecute pruebas de vulnerabilidades comunes
# 3. Genere reportes detallados
# 4. Permita añadir módulos personalizados

class PenTestFramework:
    def __init__(self):
        # Tu código aquí
        pass

    def reconocimiento(self):
        # Tu código aquí
        pass

    def escanear_vulnerabilidades(self):
        # Tu código aquí
        pass

    def generar_reporte(self):
        # Tu código aquí
        pass

# Bonus: Implementa integración con bases de datos de vulnerabilidades
```

#### Ejercicio 9: Orquestador de Red
**Objetivo**: Crear un sistema de gestión y monitoreo de red completo.
```python
# Tarea: Implementa un sistema que:
# 1. Descubra dispositivos automáticamente
# 2. Monitoree servicios y recursos
# 3. Configure dispositivos automáticamente
# 4. Proporcione una API REST
# 5. Incluya una interfaz web básica

from flask import Flask, jsonify
import nmap
import paramiko
import threading

class NetworkOrchestrator:
    def __init__(self):
        # Tu código aquí
        pass

    def descubrir_dispositivos(self):
        # Tu código aquí
        pass

    def monitorear_servicios(self):
        # Tu código aquí
        pass

    def configurar_dispositivo(self):
        # Tu código aquí
        pass

# Bonus: Añade soporte para contenedores y virtualización
```

### 6.4. Pautas para los Ejercicios

1. **Desarrollo Progresivo**:
   - Comienza con la funcionalidad básica
   - Añade características adicionales gradualmente
   - Prueba cada componente por separado
   - Integra los componentes de forma incremental

2. **Consideraciones de Seguridad**:
   - Implementa siempre validación de entrada
   - Utiliza prácticas seguras de manejo de credenciales
   - Documenta las limitaciones de seguridad
   - Incluye logging apropiado

3. **Mejores Prácticas**:
   - Sigue PEP 8 para el estilo de código
   - Documenta el código adecuadamente
   - Implementa manejo de errores robusto
   - Escribe pruebas unitarias

4. **Entorno de Práctica**:
   - Usa máquinas virtuales para pruebas
   - Configura una red de laboratorio aislada
   - Mantén copias de seguridad
   - Documenta la configuración del entorno

### 6.5. Recursos Adicionales

1. **Entornos de Prueba**:
   - VirtualBox con múltiples VMs
   - Docker para contenedores
   - GNS3 para simulación de red
   - Packet Tracer para conceptos básicos

2. **Documentación**:
   - Documentación oficial de Python
   - Manuales de las librerías
   - RFC relevantes
   - Recursos de seguridad

3. **Herramientas Complementarias**:
   - Wireshark para análisis de paquetes
   - Postman para pruebas de API
   - Git para control de versiones
   - IDE con soporte de debugging

[El resto del documento se mantiene igual...]

