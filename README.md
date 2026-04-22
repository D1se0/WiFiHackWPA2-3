# WifiHackMixto - WiFi Password Extraction Tool

![Rust](https://img.shields.io/badge/Rust-1.70%2B-orange.svg)
![Windows](https://img.shields.io/badge/Windows-10%2F11-blue.svg)
![License](https://img.shields.io/badge/License-MIT-green.svg)
![Security](https://img.shields.io/badge/Security-WPA2%2FWPA3-red.svg)

## 📡 Descripción

**WifiHackMixto** es una herramienta de auditoría de seguridad escrita en Rust que permite extraer contraseñas de redes WiFi almacenadas en sistemas Windows. La herramienta utiliza la API nativa de Windows WLAN para acceder a los perfiles de red guardados, incluyendo credenciales de redes con seguridad **WPA2** y **WPA3**.

---

## ⚠️ Advertencia Legal

**Esta herramienta debe ser utilizada ÚNICAMENTE con fines educativos y de auditoría de seguridad en sistemas propios o con autorización explícita del propietario.**

El uso no autorizado de esta herramienta para acceder a redes WiFi ajenas es:
- **ILEGAL** en la mayoría de jurisdicciones
- Constituye un delito de acceso informático no autorizado
- Puede resultar en sanciones penales y civiles

**El desarrollador no se hace responsable del uso indebido de esta herramienta.**

---

## 🚀 Características

- ✅ Extracción de contraseñas WiFi en texto plano
- ✅ Soporte para redes WPA2-Personal y WPA2-Enterprise
- ✅ Compatibilidad con redes WPA3 (Modern Authentication)
- ✅ Múltiples interfaces de red inalámbrica
- ✅ Análisis de perfiles XML de configuración WiFi
- ✅ Sin dependencias externas (solo API nativa de Windows)
- ✅ Alto rendimiento y bajo consumo de recursos
- ✅ Código seguro gracias a Rust

---

## 📋 Requisitos

### Sistema Operativo
- Windows 10 (versión 1809 o superior)
- Windows 11
- Windows Server 2019/2022

### Software
- Rust 1.70 o superior (solo para compilación)
- Permisos de administrador para acceder a ciertos perfiles

### Hardware
- Adaptador de red inalámbrica con drivers instalados
- Al menos una red WiFi previamente conectada

---

## 🔧 Instalación

### Opción 1: Usar el binario compilado

```powershell
# Navegar al directorio del ejecutable
cd WiFiHackWPA2-3\target\release

# Ejecutar como administrador
.\wifiHack.exe
```

### Opción 2: Compilar desde el código fuente

```bash
# Clonar el repositorio
git clone https://github.com/D1se0/WiFiHackWPA2-3.git
cd WiFiHackWPA2-3

# Compilar en modo release
cargo build --release

# Ejecutar
.\target\release\wifiHack.exe
```

---

## 📖 Uso

Uso Básico

```powershell
# Ejecutar la herramienta (requiere permisos de administrador)
Run as Administrator > .\wifiHack.exe
```

Salida Esperada

```text
Wi-Fi Name: MiRedWiFi, Authentication: WPA2PSK, Password: MiContraseña123
Wi-Fi Name: Oficina-Corp, Authentication: WPA2, Password: CorpPass2024!
Wi-Fi Name: Casa-5G, Authentication: WPA3SAE, Password: SecurePass@2024
Wi-Fi Name: Biblioteca-Publica, Authentication: open, Password: <NOT FOUND>
```

---

## 🏗️ Estructura del Proyecto

```text
WifiHackMixto/
├── src/
│   └── main.rs           # Código fuente principal
├── target/
│   └── release/
│       ├── wifiHack.exe  # Ejecutable compilado
│       └── wifiHack.pdb  # Símbolos de depuración
├── Cargo.toml            # Configuración del proyecto Rust
└── Cargo.lock            # Versiones específicas de dependencias
```

---

## 🔍 Funcionamiento Técnico

Algoritmo de Extracción

1. Apertura del Handle WLAN

  - Inicializa la conexión con la API WLAN de Windows

  - Negocia la versión de API (2.0)

2. Enumeración de Interfaces

  - Detecta todas las interfaces inalámbricas disponibles

  - Obtiene GUID y descripción de cada interfaz

3. Obtención de Perfiles

  - Lista todos los perfiles WiFi guardados por interfaz

  - Accede a la configuración XML de cada red

4. Extracción de Credenciales

  - Solicita el perfil con flag WLAN_PROFILE_GET_PLAINTEXT_KEY

  - Parsea el XML para extraer:

    - Nombre de red (SSID)

    - Tipo de autenticación

    - Contraseña en texto plano (keyMaterial)

5. Visualización de Resultados

  - Muestra credenciales en formato legible

  - Indica cuando no se encuentra contraseña (redes abiertas)

---

## 🛡️ Consideraciones de Seguridad

Buenas Prácticas

- Ejecutar solo en sistemas propios

- No compartir las credenciales extraídas

- Usar en entornos controlados de prueba

- Eliminar los resultados después de la auditoría

Limitaciones

- No realiza ataques de fuerza bruta

- No crackea handshakes WiFi

- Solo extrae credenciales ya almacenadas en el sistema

- Requiere que el usuario se haya conectado previamente a la red

## 🔬 Casos de Uso Legítimos

1. Recuperación de Contraseñas Olvidadas

  - Recuperar acceso a redes propias configuradas previamente

2. Auditoría de Seguridad Empresarial

  - Verificar qué credenciales WiFi están almacenadas en equipos corporativos

3. Migración de Sistemas

  - Transferir configuraciones WiFi entre equipos

4. Educación en Ciberseguridad

  - Demostrar la importancia de proteger el acceso físico a los equipos

5. Pruebas de Penetración Autorizadas

  - Evaluar la exposición de credenciales en entornos controlados

---

## 📦 Dependencias

```toml
[dependencies]
windows = { version = "0.52", features = [
    "Win32_Foundation",
    "Win32_NetworkManagement_WiFi",
    "Data_Xml_Dom",
] }
```

---

## 🤝 Contribuciones

Las contribuciones son bienvenidas, siempre que se enfoquen en:

- Mejoras de rendimiento

- Corrección de bugs

- Documentación

- Compatibilidad con nuevas versiones de Windows

No se aceptarán contribuciones que:

- Añadan capacidades de ataque activo

- Implementen descifrado de handshakes

- Faciliten el uso malicioso de la herramienta

---

## 📜 Licencia

Este proyecto está licenciado bajo la MIT License - ver el archivo LICENSE para más detalles.

### ⚡ Descargo de Responsabilidad

```text
ESTA HERRAMIENTA ES PROPORCIONADA "TAL CUAL", SIN GARANTÍAS DE NINGÚN TIPO.
EL USUARIO ASUME TODA LA RESPONSABILIDAD POR EL USO DE ESTA HERRAMIENTA.

EL DESARROLLADOR NO SE HACE RESPONSABLE DE:
- USO NO AUTORIZADO DE REDES WIFI
- VIOLACIÓN DE LEYES LOCALES O INTERNACIONALES
- DAÑOS DIRECTOS O INDIRECTOS DERIVADOS DE SU USO
- ACCIONES LEGALES CONTRA LOS USUARIOS

EL USO DE ESTA HERRAMIENTA IMPLICA LA ACEPTACIÓN DE ESTOS TÉRMINOS.
```

---

## 📞 Contacto

Para consultas sobre uso legítimo, auditorías autorizadas o reportes de bugs:

- Crear un Issue en GitHub

> Recuerda: Con gran poder viene gran responsabilidad. Usa esta herramienta éticamente.
