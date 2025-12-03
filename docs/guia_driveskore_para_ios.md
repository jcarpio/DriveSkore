# Guía Completa: Compilar DriveSkore para iOS

## 📋 Tabla de Contenidos

1. [Requisitos Previos](#requisitos-previos)
2. [Configuración del Entorno](#configuración-del-entorno)
3. [Clonar y Configurar el Proyecto](#clonar-y-configurar-el-proyecto)
4. [Configuración de Firebase para iOS](#configuración-de-firebase-para-ios)
5. [Compilación del Proyecto](#compilación-del-proyecto)
6. [Configuración en Xcode](#configuración-en-xcode)
7. [Instalación en iPhone](#instalación-en-iphone)
8. [Solución de Problemas](#solución-de-problemas)
9. [Distribución con TestFlight](#distribución-con-testflight)

---

## Requisitos Previos

### Hardware
- **Mac** con chip Apple Silicon (M1/M2/M3/M4/M5) o Intel
- **iPhone SE (2022)** o cualquier iPhone con iOS 15.1+
- **Cable USB-C a Lightning** (o USB-A a Lightning según tu Mac)

### Software
- **macOS Sequoia 15.6+** (o macOS Ventura 14.0+)
- **Xcode 16.1+** (disponible en App Store)
- **Apple ID** (cuenta gratuita para desarrollo)

### Conocimientos
- Uso básico de Terminal
- Conceptos básicos de Git
- Familiaridad con Xcode (deseable)

---

## Configuración del Entorno

### 1. Instalar Xcode

1. Abre **App Store**
2. Busca **"Xcode"**
3. Instala Xcode (puede tardar 30-60 minutos, ~7-10 GB)
4. Una vez instalado, abre Xcode y acepta los términos

```bash
# Verificar instalación
xcodebuild -version
# Debería mostrar: Xcode 16.1 o superior
```

5. Instalar Command Line Tools:

```bash
sudo xcode-select --install
```

---

### 2. Instalar Homebrew

Homebrew es el gestor de paquetes para macOS.

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

**Importante:** Al finalizar, Homebrew te mostrará 2-3 comandos para añadirlo al PATH. Cópialos y ejecútalos. Serán algo como:

```bash
echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> ~/.zprofile
eval "$(/opt/homebrew/bin/brew shellenv)"
```

Verificar instalación:

```bash
brew --version
```

---

### 3. Instalar Ruby con rbenv

macOS incluye Ruby, pero necesitamos una versión más reciente.

```bash
# Instalar rbenv y ruby-build
brew install rbenv ruby-build

# Instalar Ruby 3.1.4
rbenv install 3.1.4
rbenv global 3.1.4

# Configurar shell
echo 'eval "$(rbenv init - zsh)"' >> ~/.zshrc
source ~/.zshrc

# Verificar
ruby --version
# Debería mostrar: ruby 3.1.4
```

---

### 4. Instalar CocoaPods

CocoaPods es el gestor de dependencias para iOS.

```bash
gem install cocoapods

# Verificar
pod --version
# Debería mostrar: 1.16.2 o superior
```

---

### 5. Instalar Node.js

```bash
brew install node

# Verificar
node --version  # Debería mostrar v20.x o superior
npm --version   # Debería mostrar 10.x o superior
```

---

## Clonar y Configurar el Proyecto

### 1. Clonar el Repositorio

```bash
cd ~/Documents
git clone https://github.com/gamalielms92/driveskore.git
cd driveskore
```

---

### 2. Instalar Dependencias Node

```bash
npm install
```

Este proceso puede tardar 2-5 minutos e instalará ~1100 paquetes.

**Nota:** Los warnings en amarillo son normales y no afectan la compilación.

---

## Configuración de Firebase para iOS

### 1. Obtener GoogleService-Info.plist

Contacta al administrador del proyecto Firebase (Gamaliel) para obtener el archivo `GoogleService-Info.plist` para iOS.

**O descárgalo tú mismo:**
1. Ir a [Firebase Console](https://console.firebase.google.com)
2. Seleccionar proyecto DriveSkore
3. Configuración del proyecto → Tus apps → iOS
4. Descargar `GoogleService-Info.plist`

---

### 2. Colocar el Archivo

Copia el archivo a la raíz del proyecto:

```bash
# Si está en Downloads:
cp ~/Downloads/GoogleService-Info.plist ~/Documents/driveskore/

# Verificar
ls -la GoogleService-Info.plist
```

---

### 3. Configurar app.json

Edita el archivo de configuración:

```bash
nano app.json
```

Busca la sección `"ios"` y añade la configuración de Firebase después de `"bundleIdentifier"`:

```json
"ios": {
  "supportsTablet": true,
  "bundleIdentifier": "com.driveskore.app",
  "googleServicesFile": "./GoogleService-Info.plist",
  "infoPlist": {
    ...
  }
}
```

Guardar: `Ctrl+O`, `Enter`, `Ctrl+X`

---

## Compilación del Proyecto

### 1. Generar Proyecto iOS

```bash
npx expo prebuild --platform ios --clean
```

**Importante:** Si aparece el mensaje "Continue with uncommitted changes?", responde **yes**.

Este proceso:
- Crea la carpeta `ios/`
- Genera el proyecto de Xcode
- Configura dependencias nativas

---

### 2. Editar Podfile

El archivo Podfile necesita una línea adicional para Firebase:

```bash
nano ios/Podfile
```

Busca la línea que dice `prepare_react_native_project!` (alrededor de la línea 18-20).

**Justo después** de esa línea, añade:

```ruby
use_modular_headers!
```

Debería quedar así:

```ruby
platform :ios, podfile_properties['ios.deploymentTarget'] || '15.1'
prepare_react_native_project!
use_modular_headers!

target 'DriveSkore' do
```

Guardar: `Ctrl+O`, `Enter`, `Ctrl+X`

---

### 3. Instalar Dependencias iOS (Pods)

```bash
cd ios
pod install
cd ..
```

Este proceso puede tardar 5-10 minutos la primera vez.

**Resultado esperado:**
```
Pod installation complete! There are 118 dependencies from the Podfile and 140 total pods installed.
```

Los warnings en amarillo son normales.

---

## Configuración en Xcode

### 1. Abrir el Proyecto

```bash
open ios/DriveSkore.xcworkspace
```

**⚠️ IMPORTANTE:** Abre el archivo `.xcworkspace`, **NO** el `.xcodeproj`

---

### 2. Añadir Apple ID

1. Ve a **Xcode → Settings** (o Preferences)
2. Pestaña **Accounts**
3. Click en **+** (abajo izquierda)
4. Selecciona **Apple ID**
5. Introduce tu Apple ID y contraseña
6. Completa autenticación de dos factores si es necesario

---

### 3. Configurar Signing & Capabilities

**a) Seleccionar el proyecto:**
- En el panel izquierdo, click en el proyecto **DriveSkore** (icono azul arriba)
- Selecciona el target **DriveSkore** en la sección TARGETS

**b) Configurar Signing:**
- Pestaña **Signing & Capabilities**
- Marca **"Automatically manage signing"**
- En **Team**: selecciona tu Apple ID (aparecerá como "Personal Team" o tu nombre)

**c) Cambiar Bundle Identifier:**

El Bundle ID `com.driveskore.app` ya está registrado. Necesitas uno único:

- Cambia `com.driveskore.app` a `com.tuapellido.driveskore`
- Ejemplo: `com.josecarpio.driveskore`

**d) Eliminar Push Notifications:**

Las cuentas personales gratuitas no soportan Push Notifications:

- En la misma pantalla, busca **Push Notifications**
- Click en el botón de **basura** 🗑️ a la derecha
- Esto elimina la capability

**Resultado esperado:**
- ✅ Team: Tu nombre (Personal Team)
- ✅ Signing Certificate: Apple Development
- ✅ Sin errores ni warnings

---

## Instalación en iPhone

### 1. Preparar iPhone

**a) Activar Modo Desarrollador:**

En el iPhone:
1. Ve a **Ajustes → Privacidad y seguridad → Modo desarrollador**
2. Activa el interruptor
3. **Reinicia el iPhone**
4. Después del reinicio, vuelve a activar el Modo desarrollador

**b) Conectar al Mac:**

1. Conecta el iPhone al Mac con cable USB
2. **Desbloquea el iPhone** (no puede estar en pantalla de bloqueo)
3. Si aparece "¿Confiar en este ordenador?" → Toca **Confiar**
4. Introduce tu código del iPhone

**Nota:** Si no aparece el mensaje de confiar, intenta:
- Desconectar y reconectar el cable
- Sacudir suavemente el iPhone
- Usar otro puerto USB del Mac

---

### 2. Confiar en Keychain (primera vez)

Al compilar por primera vez, aparecerá un mensaje pidiendo acceso al keychain:

```
codesign wants to access key "Apple Development: ..." in your keychain.
```

- Introduce la **contraseña de tu usuario del Mac** (no la de Apple ID)
- Click en **"Always Allow"**

---

### 3. Compilar e Instalar

**a) Seleccionar dispositivo:**

En la barra superior de Xcode, al lado del botón ▶️:
- Click en el menú desplegable de dispositivos
- Selecciona tu **iPhone SE** (no un simulador)

**b) Compilar:**

- Click en el botón **▶️ (Play)** o presiona **Cmd+R**
- La primera compilación tarda 5-10 minutos

**Progreso visible:**
```
Building... → Compiling... → Linking... → Installing...
```

---

### 4. Confiar en Certificado de Desarrollador

La primera vez que instales una app con tu certificado, iOS la bloqueará:

**En el iPhone:**
1. Aparecerá: "The application could not be launched because the Developer App Certificate is not trusted"
2. Ve a **Ajustes → General → VPN y gestión de dispositivos**
3. Verás una sección con tu email
4. Toca en tu nombre/email
5. Toca **"Confiar en [tu nombre]"**
6. Confirma en el popup

**Solo necesitas hacer esto una vez.**

---

### 5. Iniciar Servidor de Desarrollo

En una **nueva terminal** (no cierres Xcode):

```bash
cd ~/Documents/driveskore
npx expo start
```

Verás:
```
Metro waiting on exp+driveskore://192.168.1.XXX:8081
```

**Importante:** Anota la dirección IP que aparece (por ejemplo: `192.168.1.109`)

---

### 6. Conectar la App al Servidor

**En el iPhone:**

1. Abre la app **DriveSkore**
2. Verás: "No development servers found"
3. Toca **"Enter URL manually"**
4. Introduce: `http://192.168.1.XXX:8081` (usa la IP de tu Mac)
5. Presiona Enter

**⚠️ Requisito:** iPhone y Mac deben estar en la **misma red WiFi**

---

### 7. ¡Listo!

**¡La app DriveSkore debería cargar correctamente en tu iPhone!** 🎉

---

## Solución de Problemas

### Problema: iPhone no detectado por Xcode

**Síntomas:**
- Finder no muestra el iPhone
- Xcode no lo lista en dispositivos

**Soluciones:**

1. **Reiniciar servicios USB:**

```bash
sudo pkill usbmuxd
sudo launchctl stop com.apple.usbmuxd
sudo launchctl start com.apple.usbmuxd
```

2. **Verificar en Xcode:**
   - **Window → Devices and Simulators** (Shift+Cmd+2)
   - ¿Aparece tu iPhone en la pestaña "Devices"?

3. **Verificar cable:**
   - Usa cable original de Apple
   - Algunos cables solo cargan, no transfieren datos
   - Prueba con otro puerto USB

4. **iPhone desbloqueado:**
   - El iPhone debe estar desbloqueado al conectarlo

---

### Problema: Error "pod install failed"

**Síntomas:**
```
The following Swift pods cannot yet be integrated as static libraries
```

**Solución:**

Asegúrate de haber añadido `use_modular_headers!` en el Podfile:

```bash
nano ios/Podfile
```

Después de `prepare_react_native_project!`:
```ruby
use_modular_headers!
```

Luego:
```bash
cd ios
rm -rf Pods Podfile.lock
pod install
cd ..
```

---

### Problema: Errores de compilación en Xcode

**Síntomas:**
- Muchos errores rojos en Firebase o React Native

**Soluciones:**

1. **Limpiar build:**
   - Xcode → Product → Clean Build Folder (Shift+Cmd+K)

2. **Regenerar proyecto:**
```bash
cd ~/Documents/driveskore
rm -rf ios
npx expo prebuild --platform ios --clean
cd ios
pod install
```

3. **Verificar Xcode:**
   - Debe ser versión 16.1+
   - macOS debe ser Sequoia 15.6+

---

### Problema: App se cierra inmediatamente

**Causa:** Certificado de desarrollador no confiado

**Solución:**

En el iPhone:
1. **Ajustes → General → VPN y gestión de dispositivos**
2. Toca tu email
3. Toca **"Confiar"**

---

### Problema: "No development servers found"

**Causa:** App no se conecta al servidor Metro

**Soluciones:**

1. **Verificar servidor corriendo:**
```bash
npx expo start
```

2. **Verificar misma WiFi:**
   - Mac y iPhone en la misma red

3. **Introducir URL manualmente:**
   - En la app: "Enter URL manually"
   - Usar: `http://[IP_DEL_MAC]:8081`

4. **Encontrar IP del Mac:**
```bash
ipconfig getifaddr en0
```

5. **Alternativa - Usar túnel:**
```bash
npx expo start --tunnel
```
(Funciona en cualquier red)

---

### Problema: Error OCR_API_KEY

**Síntomas:**
```
OCR_API_KEY no está configurada
```

**Causa:** Falta configurar la clave de la API de OCR

**Solución temporal:**

El OCR es opcional. Puedes:
1. Hacer clic en "Dismiss" y usar la app sin escaneo de matrículas
2. Pedirle la clave a Gamaliel
3. Configurar archivo `.env`:

```bash
nano .env
```

Añadir:
```
EXPO_PUBLIC_OCR_API_KEY=tu_clave_aqui
```

---

## Distribución con TestFlight

### Requisitos

- **Apple Developer Program** ($99/año)
- Cuenta aprobada (tarda 24-48 horas)

### Proceso

1. **Enrollarse en Apple Developer:**
   - https://developer.apple.com/programs/enroll/
   - Seleccionar "Individual" para aprobación rápida
   - Pagar $99 USD

2. **Esperar aprobación:**
   - Normalmente 24-48 horas
   - Revisar email de confirmación

3. **Configurar App Store Connect:**
   - https://appstoreconnect.apple.com
   - Crear nueva app "DriveSkore"
   - Bundle ID: `com.driveskore.app` (o el que uses)

4. **Crear build con EAS:**

```bash
# Instalar EAS CLI
npm install -g eas-cli

# Login
eas login

# Configurar proyecto
eas build:configure

# Crear build para iOS
eas build --platform ios
```

5. **Subir a TestFlight:**
   - El build aparecerá automáticamente en TestFlight
   - Añadir información de prueba
   - Invitar testers (hasta 10,000 usuarios externos)

6. **Invitar usuarios del campus:**
   - App Store Connect → TestFlight → Agregar testers
   - Enviar invitaciones por email
   - Los usuarios instalan TestFlight y aceptan invitación

---

## Comandos Útiles de Referencia

### Desarrollo Diario

```bash
# Iniciar servidor Metro
npx expo start

# Limpiar caché
npx expo start -c

# Ver en simulador
npx expo run:ios

# Ver en dispositivo físico
npx expo run:ios --device
```

### Reinstalar dependencias

```bash
# Node
rm -rf node_modules package-lock.json
npm install

# iOS
cd ios
rm -rf Pods Podfile.lock
pod install
cd ..
```

### Regenerar proyecto completo

```bash
rm -rf ios
npx expo prebuild --platform ios --clean
cd ios
pod install
```

---

## Información Adicional

### Duración del Certificado Personal

Las apps instaladas con certificado personal (gratuito):
- ⏰ Duran **7 días**
- 🔄 Se pueden reinstalar fácilmente
- 📱 Máximo **3 dispositivos** simultáneos

Para distribución profesional, necesitas Apple Developer Program ($99/año).

---

### Estructura del Proyecto

```
driveskore/
├── src/                    # Código React Native
│   ├── screens/
│   ├── components/
│   └── services/
├── ios/                    # Proyecto iOS (generado)
│   ├── DriveSkore.xcworkspace  ← Abrir este
│   ├── Podfile
│   └── Pods/
├── android/                # Proyecto Android
├── app.json               # Configuración Expo
├── package.json           # Dependencias Node
└── GoogleService-Info.plist  # Firebase iOS
```

---

## Recursos

- **Documentación Expo:** https://docs.expo.dev
- **React Native:** https://reactnative.dev
- **Apple Developer:** https://developer.apple.com
- **CocoaPods:** https://cocoapods.org
- **Firebase iOS:** https://firebase.google.com/docs/ios/setup

---

## Créditos

**Desarrollado por:**
- Gamaliel Moreno Sánchez (Desarrollador Principal)
- José Carpio Cañada (Mentor)

**Universidad:** Universidad de Huelva  
**Proyecto:** Trabajo Fin de Máster - Ingeniería Informática  
**Fecha:** Diciembre 2025

---

## Licencia

Este documento es parte del proyecto DriveSkore y está destinado para uso interno del equipo de desarrollo y pruebas del campus universitario.

---

**¿Dudas o problemas?** Contacta al equipo de desarrollo.

**¡Buena suerte con el piloto del campus! 🚗📱**
