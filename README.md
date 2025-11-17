# FlipFall - Juego en Jack (Nand2Tetris)

## Tabla de Contenidos

1. [Descripción](#descripción)
2. [Características del Juego](#características-del-juego)
   - [Mecánicas Principales](#mecánicas-principales)
   - [Objetos del Juego](#objetos-del-juego)
3. [Controles](#controles)
4. [Arquitectura del Proyecto](#arquitectura-del-proyecto)
   - [Estructura de Archivos](#estructura-de-archivos)
   - [Clases y Responsabilidades](#clases-y-responsabilidades)
5. [Sistema de Puntuación](#sistema-de-puntuación)
6. [Compilación y Ejecución](#compilación-y-ejecución)
7. [Sprites](#sprites)
8. [Autores](#autores)
9. [Demostración](#demostración)

## 1. Descripción

**FlipFall** es un juego estilo Flappy Bird implementado completamente en el lenguaje Jack para el proyecto final del curso de Organización de Computadores. El juego presenta un pájaro que debe esquivar tuberías horizontales que caen desde arriba mientras recolecta monedas para aumentar su puntuación.

## 2. Características del Juego

### Mecánicas Principales
- **Control del pájaro**: Movimiento en 4 direcciones (arriba, abajo, izquierda, derecha)
- **Tuberías horizontales**: Obstáculos que caen verticalmente con huecos por los que el pájaro debe pasar
- **Sistema de monedas**: Objetos recolectables que otorgan puntos adicionales
- **Sistema de puntuación**: El score aumenta automáticamente con el tiempo y al recolectar monedas
- **Game Over**: El juego termina al colisionar con una tubería

### Objetos del Juego
- **Pájaro (Bird)**: El personaje controlado por el jugador (tamaño 30x30 píxeles)
- **Tuberías (HorizontalWall)**: Obstáculos horizontales con hueco de 90 píxeles de ancho
- **Monedas (FallingObject)**: Objetos circulares de 16x16 píxeles que otorgan +5 puntos

## 3. Controles

| Tecla | Acción |
|-------|--------|
| Flecha Arriba | Mover el pájaro hacia arriba |
| Flecha Abajo | Mover el pájaro hacia abajo |
| Flecha Izquierda | Mover el pájaro hacia la izquierda |
| Flecha Derecha | Mover el pájaro hacia la derecha |
| Q | Salir del juego |

## 4. Arquitectura del Proyecto

### Estructura de Archivos

```
FinalProject-OrgComp/
│
├── Main.jack              # Punto de entrada del programa
├── BirdGame.jack          # Lógica principal del juego
├── Bird.jack              # Clase del pájaro (jugador)
├── FallingObject.jack     # Clase para objetos cayendo (monedas)
├── HorizontalWall.jack    # Clase para las tuberías/obstáculos
└── README.md              # Este archivo
```

### Clases y Responsabilidades

#### `Main.jack`
- Clase principal que inicia el juego
- Crea una instancia de `BirdGame` y ejecuta el loop principal

#### `BirdGame.jack`
- **Gestión del juego**: Controla el flujo principal del juego
- **Manejo de entrada**: Procesa las teclas presionadas por el usuario
- **Sistema de colisiones**: Verifica colisiones entre el pájaro y los objetos
- **Sistema de puntuación**: Gestiona el score y lo muestra en pantalla
- **Creación de objetos**: Genera tuberías y monedas de forma pseudo-aleatoria
- **Variables principales**:
  - `lives`: Vida del jugador (termina el juego cuando llega a 0)
  - `score`: Puntuación actual
  - `objects`: Array de objetos cayendo (máximo 5)
  - `horizontalWalls`: Array de tuberías (máximo 3)

#### `Bird.jack`
- **Representación del jugador**: Sprite de 30x30 píxeles
- **Movimiento**: Métodos para mover el pájaro en 4 direcciones
- **Dibujo**: Renderiza el sprite usando `Memory.poke` para escribir directamente en memoria de pantalla
- **Límites**: Verifica que el pájaro no salga de los bordes de la pantalla

#### `FallingObject.jack`
- **Objetos recolectables**: Actualmente solo monedas (tipo 2)
- **Movimiento**: Caen verticalmente y reaparecen arriba al salir de pantalla
- **Reactivación**: Sistema de reactivación tras ser recolectadas
- **Detección de colisiones**: Método para verificar colisión con el pájaro

#### `HorizontalWall.jack`
- **Obstáculos principales**: Tuberías que caen verticalmente
- **Estructura**: Dos muros (izquierdo y derecho) con un hueco en medio
- **Dimensiones**: Altura de 10 píxeles, hueco de 90 píxeles
- **Reposicionamiento**: Al salir de pantalla, vuelve arriba con nueva posición de hueco
- **Detección de colisiones**: Verifica si el pájaro está dentro del hueco o colisiona con los muros

## 5. Sistema de Puntuación

- **Puntos por tiempo**: +1 punto cada ~2 segundos
- **Puntos por monedas**: +5 puntos por cada moneda recolectada
- **Final Score**: Se muestra en la pantalla de Game Over

## 6. Compilación y Ejecución

### Opción 1: Usando el IDE Online de Nand2Tetris

**Paso 1 - Preparar el entorno:**
- Ingresa al IDE de Nand2Tetris online
- Navega hasta la herramienta Jack Compiler

**Paso 2 - Compilar los archivos:**
- Selecciona la opción para cargar un directorio
- Localiza y abre la carpeta del proyecto `FinalProject-OrgComp`
- Presiona el botón de compilación para generar los archivos `.vm`

**Paso 3 - Ejecutar el juego:**
- Una vez compilado, accede al botón de ejecución
- El VMEmulator se iniciará automáticamente
- Ajusta la velocidad de ejecución según tu preferencia (recomendado: Fast)
- Presiona el botón de inicio para jugar

### Opción 2: Usando Herramientas Locales

Si tienes instalada la suite de Nand2Tetris localmente:

**Compilación:**

En Linux:
```bash
JackCompiler.sh ./FinalProject-OrgComp
```

En Windows:
```cmd
JackCompiler.bat ./FinalProject-OrgComp
```

**Ejecución:**
- Abre el VMEmulator
- Carga el directorio compilado
- Ejecuta el programa

## 7. Sprites

### Pájaro (Bird)
- Sprite dibujado con `Memory.poke` en 2 columnas de 16 píxeles
- Representación visual de un pájaro pixelado

### Moneda
- Círculo de 16x16 píxeles
- 8 filas de datos en memoria

### Tuberías
- Rectángulos dibujados con `Screen.drawRectangle`
- Dos secciones (izquierda y derecha) con hueco en medio

## 8. Autores

Proyecto desarrollado para el curso de Organización de Computadores por:

- Juan Esteban Trujillo Montes

- Arturo Fernando Murgueytio Arias

- Felipe Castro Jaimes

## 9. Demostración

### Video Demostrativo

Puedes ver una demostración y explicación completa del juego en el siguiente video:

[Enlace al video](https://youtu.be/beaHDHwc1ks)

**¡Disfruta jugando FlipFall!**
