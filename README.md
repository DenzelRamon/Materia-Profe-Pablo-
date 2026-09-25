# Citas Médicas App — Análisis y Selección de Stack

Aplicación móvil de **gestión de citas médicas** (agenda de turnos, recordatorios, historial de paciente) para **Android e iOS**. Este README resume la decisión de arquitectura; el análisis completo está en [`_T1_U1 Análisis técnico de stack móvil para proyecto real.pdf`](./_T1_U1 Análisis técnico de stack móvil para proyecto real.pdf).

# Stack final recomendado

| Componente | Elección |
|---|---|
| Framework | **Flutter 3.47** |
| Lenguaje | **Dart 3.13** |
| IDE | **Android Studio Quail 4** (o VS Code + plugins Flutter/Dart) |
| Backend / notificaciones | Firebase (Cloud Messaging, Auth) |
| Base de datos local | `sqflite` / `drift` |

# Por qué Flutter

- Una sola base de código para Android e iOS → menor tiempo y costo de desarrollo.
- Rendimiento nativo real gracias al motor **Impeller** (por defecto en todas las plataformas desde 2026).
- Ecosistema de plugins maduro para cámara, biometría, notificaciones push y almacenamiento local.
- Tipado seguro y `null-safety` en Dart, relevante al manejar datos clínicos sensibles.

Comparado con **React Native (Expo)**: se evita la capa de interoperabilidad JS–nativo para funciones sensibles como biometría y cifrado de datos.
Comparado con **Kotlin Multiplatform**: se evita duplicar la capa de UI en Swift/Compose, priorizando velocidad de entrega para un equipo reducido. KMP queda como alternativa válida a futuro.

# Hardware / permisos requeridos

| Sensor | Uso | Paquete |
|---|---|---|
| Cámara | Escaneo de QR / check-in, fotos de recetas | `mobile_scanner`, `camera` |
| Push | Recordatorios de citas | `firebase_messaging` |
| Almacenamiento local | Historial offline | `sqflite`, `drift`, `hive` |
| Biometría | Acceso seguro a datos clínicos | `local_auth` |
| GPS | Ubicación del centro de salud | `geolocator` |

# Instalación del entorno

1. Instalar [Android Studio Quail 4](https://developer.android.com/studio) con el Android SDK (API 34/35) y un emulador.
2. Instalar el plugin **Flutter** desde `Settings → Plugins → Marketplace` (incluye Dart automáticamente).
3. Verificar el entorno:
   ```bash
   flutter doctor
   ```
4. Clonar y ejecutar el proyecto:
   ```bash
   git clone <url-del-repo>
   cd citas_medicas_app
   flutter pub get
   flutter run
   ```

# Estructura del proyecto (propuesta)

```
citas_medicas_app/
├── lib/
│   ├── main.dart
│   ├── screens/       # Pantallas (agenda, historial, perfil)
│   ├── widgets/        # Componentes reutilizables
│   ├── models/         # Modelos de datos (Cita, Paciente, etc.)
│   └── services/       # Firebase, almacenamiento local, geolocalización
├── android/
├── ios/
├── pubspec.yaml
└── README.md
```

# Documento completo

Ver el análisis técnico detallado (comparativa de frameworks, justificación de lenguaje, configuración del entorno y análisis de hardware) en [`_T1_U1 Análisis técnico de stack móvil para proyecto real.pdf`](./_T1_U1 Análisis técnico de stack móvil para proyecto real.pdf).
