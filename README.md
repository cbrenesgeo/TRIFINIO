# TRIFINIO
Repositorio del código de js  para GEE usando en el proceso de elaboración del mapa de uso / cobertura del Trifinio

# Clasificación de Cobertura del Suelo con Random Forest en Google Earth Engine  
**Caso de estudio: Región Trifinio**

Este repositorio contiene un script de **Google Earth Engine (GEE)** para la **clasificación supervisada de cobertura del suelo** utilizando el algoritmo **Random Forest**, a partir de un mosaico de **Sentinel-2** y puntos de entrenamiento previamente definidos.

El flujo incluye:
- Visualización de datos de entrada
- Extracción de firmas espectrales
- Entrenamiento y validación del modelo
- Evaluación de precisión
- Exportación del mapa clasificado

---

## 🛰️ Datos de entrada

### 1. Imagen Sentinel-2 (Asset GEE)
- **Tipo:** `ee.Image`
- **Descripción:** Mosaico Sentinel-2 preprocesado
- **Bandas utilizadas:**  
  `b1, b2, b3, b4, b5, b6, b7`
- **Ruta del asset:**


### 2. Puntos de entrenamiento
- **Tipo:** `ee.FeatureCollection`
- **Descripción:** Puntos de entrenamiento con clases de cobertura
- **Campo de clase:** `cod_2`
- **Ruta del asset:**


---

## 🧠 Metodología

1. **Selección de bandas espectrales**  
   Se utilizan 7 bandas del mosaico Sentinel-2.

2. **Extracción de valores espectrales**  
   Se asocian los valores de las bandas a los puntos de entrenamiento mediante `sampleRegions()`.

3. **División entrenamiento / validación**
   - 80% entrenamiento
   - 20% validación
   - División aleatoria

4. **Clasificación supervisada**
   - Algoritmo: **Random Forest**
   - Número de árboles: `250`

5. **Evaluación**
   - Matriz de confusión
   - Precisión global (OA)
   - Índice Kappa
   - Precisión del productor (PA)
   - Precisión del usuario (UA)

6. **Exportación**
   - Resultado exportado a Google Drive
   - Resolución: 10 m

---

## 🎨 Clases de cobertura del suelo

| Código | Clase |
|------:|-------|
| 1 | Bosque latifoliado |
| 2 | Bosque de coníferas |
| 3 | Bosque mixto |
| 4 | Matorral / guamil |
| 5 | Plantación forestal |
| 6 | Pastos |
| 7 | Cultivos anuales |
| 8 | Cultivos perennes |
| 9 | Café |
| 10 | Área urbana/habitada |
| 11 | Suelo desnudo |
| 12 | Cuerpos de agua |
| 13 | Asentamientos |
| 14 | Nubes |
| 15 | Sombras |

---

## ▶️ Cómo ejecutar el script

1. Abrir **Google Earth Engine Code Editor**  
   https://code.earthengine.google.com/

2. Copiar el contenido de `rf_trifinio.js` en un nuevo script  
   o abrirlo directamente usando **Get Link**.

3. Verificar que se tiene acceso de lectura (`Reader`) a los assets:
   - `s2_mos`
   - `train_301024_ptos`

4. Ejecutar el script (`Run`).

---

## 🔐 Compartir y reproducibilidad

Para que otros usuarios puedan ejecutar el script sin modificaciones:

- El script debe compartirse mediante **Get Link**
- Los assets deben tener permisos **Reader**
- Se utilizan rutas en `projects/.../assets/`, compatibles con trabajo colaborativo

---

## 📤 Salida

- **Producto principal:**  
  Mapa de clasificación de cobertura del suelo (Random Forest)
- **Formato:** GeoTIFF (exportado a Google Drive)
- **Resolución espacial:** 10 m

---

## 🛠️ Requisitos

- Cuenta activa de Google Earth Engine
- Permisos de acceso a los assets del proyecto

---

## ✍️ Autor

**Christian Brenes**  
Análisis espacial, SIG y sensores remotos  
Clasificación supervisada y modelación ambiental

---

## 📄 Licencia

Este proyecto se distribuye bajo licencia **MIT** (o la que prefieras especificar).
