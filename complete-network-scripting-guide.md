# Guía Completa de Scripting de Red y Librerías Python

## Índice General
1. [Fundamentos de Redes](#1-fundamentos-de-redes)
2. [Programación con Python](#2-programación-con-python)
3. [Librerías Python para Networking](#3-librerías-python-para-networking)
4. [Técnicas de Scripting](#4-técnicas-de-scripting)
5. [Mejores Prácticas y Seguridad](#5-mejores-prácticas-y-seguridad)

## 1. Fundamentos de Redes

### 1.1. Modelo OSI
El modelo OSI (Open Systems Interconnection) es un marco conceptual que estandariza las funciones de un sistema de telecomunicaciones en siete capas distintas:

1. Física
2. Enlace de Datos
3. Red
4. Transporte
5. Sesión
6. Presentación
7. Aplicación

Cada capa tiene funciones específicas y protocolos asociados que son fundamentales para comprender cómo funcionan las redes.

### 1.2. Protocolo TCP/IP
TCP/IP es el protocolo fundamental de Internet. Principales características:

- TCP (Transmission Control Protocol):
  - Orientado a conexión
  - Garantiza la entrega de paquetes
  - Control de flujo
  - Ordenamiento de paquetes

- IP (Internet Protocol):
  - Direccionamiento
  - Enrutamiento
  - Fragmentación de paquetes

### 1.3. Direccionamiento IP
Comprensión fundamental de:
- IPv4 vs IPv6
- Clases de direcciones IP
- Direcciones públicas vs privadas
- NAT (Network Address Translation)

### 1.4. Subnetting
- Máscaras de red
- CIDR notation
- Cálculo de subredes
- Planificación de direccionamiento

## 2. Programación con Python

### 2.1. Configuración del Entorno
```python
# Instalación de dependencias necesarias
pip install socket requests scapy paramiko python-nmap

# Importaciones comunes
import socket
import requests
from scapy.all import *
import paramiko
import nmap
```

### 2.2. Conceptos Básicos
Fundamentos de programación Python necesarios para scripting de red:
- Variables y tipos de datos
- Estructuras de control
- Funciones y módulos
- Manejo de excepciones
- Programación orientada a objetos

## 3. Librerías Python para Networking

### 3.1. Socket
#### Descripción
La librería `socket` es fundamental para la programación de red en Python, proporcionando una interfaz de bajo nivel.

#### Funcionalidades Principales
- Creación de conexiones TCP/UDP
- Comunicación cliente-servidor
- Manipulación de direcciones IP y puertos

#### Ejemplos Prácticos
```python
def crear_socket_tcp():
    try:
        s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
        return s
    except socket.error as e:
        print(f"Error al crear socket: {e}")
        return None

def banner_grabbing(host, puerto):
    try:
        s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
        s.settimeout(2)
        s.connect((host, puerto))
        banner = s.recv(1024).decode().strip()
        s.close()
        return banner
    except:
        return None
```

### 3.2. Requests
#### Descripción
Librería de alto nivel para realizar peticiones HTTP/HTTPS de forma sencilla.

#### Funcionalidades Principales
- Peticiones HTTP (GET, POST, PUT, DELETE)
- Manejo de sesiones
- Autenticación
- Manipulación de cookies

#### Ejemplos Prácticos
```python
def analizar_http(url):
    try:
        response = requests.get(url)
        return {
            'status_code': response.status_code,
            'headers': dict(response.headers),
            'server': response.headers.get('Server'),
            'content_type': response.headers.get('Content-Type')
        }
    except requests.exceptions.RequestException as e:
        return {'error': str(e)}

def enviar_datos_post():
    datos = {'usuario': 'ejemplo', 'password': 'secreto'}
    response = requests.post('https://api.ejemplo.com/login', 
                           json=datos,
                           headers={'Content-Type': 'application/json'})
    return response.status_code
```

### 3.3. Scapy
#### Descripción
Potente librería para manipulación y análisis de paquetes de red.

#### Funcionalidades Principales
- Creación de paquetes personalizados
- Captura de tráfico
- Análisis de protocolos
- Escaneo de red

#### Ejemplos Prácticos
```python
def escaneo_tcp_syn(objetivo, puertos):
    resultados = []
    for puerto in puertos:
        resp = sr1(IP(dst=objetivo)/TCP(dport=puerto,flags="S"), timeout=1, verbose=0)
        if resp and resp.haslayer(TCP):
            if resp[TCP].flags == 0x12:  # SYN-ACK
                resultados.append(puerto)
    return resultados

def capturar_paquetes(interfaz):
    def callback(paquete):
        if IP in paquete:
            print(f"IP src: {paquete[IP].src} -> dst: {paquete[IP].dst}")
    
    sniff(iface=interfaz, prn=callback, count=10)
```

### 3.4. Paramiko
#### Descripción
Implementación del protocolo SSH v2 en Python.

#### Funcionalidades Principales
- Conexiones SSH
- Transferencia de archivos SFTP
- Ejecución remota de comandos

#### Ejemplos Prácticos
```python
def conexion_ssh(host, usuario, password):
    cliente = paramiko.SSHClient()
    cliente.set_missing_host_key_policy(paramiko.AutoAddPolicy())
    try:
        cliente.connect(host, username=usuario, password=password)
        return cliente
    except Exception as e:
        print(f"Error SSH: {e}")
        return None

def ejecutar_comando_remoto(cliente, comando):
    stdin, stdout, stderr = cliente.exec_command(comando)
    return stdout.read().decode()
```

### 3.5. Python-nmap
#### Descripción
Interfaz Python para el escáner de puertos Nmap.

#### Funcionalidades Principales
- Escaneo de puertos
- Detección de servicios
- Identificación de sistemas operativos

#### Ejemplos Prácticos
```python
def escanear_host(objetivo):
    scanner = nmap.PortScanner()
    scanner.scan(objetivo, '1-1024')
    return scanner[objetivo].all_tcp()

def detectar_servicios(objetivo, puertos):
    scanner = nmap.PortScanner()
    scanner.scan(objetivo, puertos)
    return scanner[objetivo]['tcp']
```

## 4. Técnicas de Scripting

### 4.1. Escaneo de Puertos
```python
def escaneo_completo(objetivo, rango_puertos):
    puertos_abiertos = []
    for puerto in range(rango_puertos[0], rango_puertos[1] + 1):
        sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
        sock.settimeout(1)
        resultado = sock.connect_ex((objetivo, puerto))
        if resultado == 0:
            puertos_abiertos.append(puerto)
        sock.close()
    return puertos_abiertos
```

### 4.2. Enumeración de Servicios
```python
def enumerar_servicios(host, puertos_abiertos):
    servicios = {}
    for puerto in puertos_abiertos:
        try:
            nombre_servicio = socket.getservbyport(puerto)
            banner = banner_grabbing(host, puerto)
            servicios[puerto] = {
                'servicio': nombre_servicio,
                'banner': banner
            }
        except:
            servicios[puerto] = {
                'servicio': 'desconocido',
                'banner': None
            }
    return servicios
```

## 5. Mejores Prácticas y Seguridad

### 5.1. Consideraciones Éticas
- Obtener siempre autorización previa
- Documentar todas las acciones
- Respetar la privacidad y confidencialidad
- Reportar vulnerabilidades responsablemente

### 5.2. Marco Legal
- Conocer las leyes de ciberseguridad locales
- Entender las implicaciones legales
- Mantener registros de autorizaciones
- Cumplir con regulaciones de privacidad

### 5.3. Documentación
- Mantener documentación detallada de scripts
- Comentar el código adecuadamente
- Registrar cambios y versiones
- Documentar dependencias y requisitos

### 5.4. Testing
- Realizar pruebas en entornos controlados
- Validar resultados
- Implementar manejo de errores
- Mantener logs de actividades

## Conclusión

Esta guía proporciona una base completa para el scripting de red en Python, cubriendo tanto los fundamentos teóricos como las herramientas prácticas necesarias. Recuerda:

1. Comenzar con los fundamentos de redes
2. Dominar las librerías básicas antes de pasar a las avanzadas
3. Practicar en entornos controlados
4. Seguir las mejores prácticas de seguridad
5. Mantener actualizado el conocimiento de herramientas y técnicas

Las habilidades de scripting de red son valiosas para:
- Administración de sistemas
- Seguridad informática
- Automatización de tareas
- Análisis de red
- Desarrollo de herramientas personalizadas

