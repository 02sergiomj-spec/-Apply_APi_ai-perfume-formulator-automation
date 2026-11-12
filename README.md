# -Apply_APi_ai-perfume-formulator-automation
Automatización en Python que integra la API de Google Gemini (JSON estructurado) y Pandas para formular equivalencias de perfumería sobre inventario cerrado, validar reglas de seguridad y calcular escandallos de costes en CSV.
<div align="center">

# 🧪✨ PerfumerIA: Formulador Autónomo & Escandallo Inteligente
### *Ingeniería inversa de fragancias impulsada por Python y la API de Google Gemini*

*De una simple petición en texto a una ficha técnica de laboratorio validada, costeada y almacenada en segundos.*

</div>

---

## 🚀 La Historia y el Reto del Negocio

 **tienda de perfumería autónoma** que busca ofrecer equivalencias de alta gama (*Extrait de Parfum* al 30 %) formuladas a medida en tiempo real. 

Al intentar escalar este modelo de negocio sin depender de horas de ensayo y error manual, surgen **cuatro grandes desafíos**:

1. 📦 **Inventario Cerrado:** La tienda no cuenta con miles de moléculas químicas, sino con un catálogo optimizado de **8 esencias base** (*Bergamota, Tamarindo, Canela/Naranja/Patchouli, Haba Tonka, Vainilla, Ylang Ylang, Ámbar y Musk*). ¿Cómo clonar cualquier perfume del mercado usando **solo** lo que hay en estantería y sin meter ingredientes de relleno?
2. ⚖️ **Seguridad y Proporciones Exactas:** Por normativa y equilibrio olfativo, ciertas esencias (como `CNP`) nunca pueden superar el **15 % (`4.5 ml`)**, y la mezcla total debe cuadrar al milímetro en **`30.0 ml`** de esencia pura.
3. 💡 **Inteligencia de Compras (Mejora Continua):** Si un perfume comercial tiene una nota muy específica que falta en el inventario y la similitud baja del 90 %, el sistema debe ser capaz de decirnos: *"Con lo que tienes logras un 78 %, pero si compras esta esencia concreta por ~7 €, llegarás al 100 %"* y mostrarnos la receta ideal completa.
4. 💰 **Control Financiero y Registro Automático:** Calcular el coste real de fabricación por cada frasco de 100 ml frente al precio de venta original y registrar cada nueva fórmula en una base de datos limpia sin errores humanos.

---

## 🤖 La Solución: Cómo la API de Gemini impulsa el Proyecto

Para resolverlo, hemos diseñado un **flujo de automatización inteligente** donde Python actúa como director de orquesta y la **API de Google Gemini** funciona como el motor de conocimiento olfativo y estructuración de datos:

```text
  [ 👤 Usuario ] ──► Introduce el nombre del perfume (ej. "Dior Sauvage")
        │
        ▼
  [ 🔌 API Gemini ] ──► Analiza pirámide olfativa y precios de mercado
        │               Devuelve un JSON estricto con la fórmula adaptada
        ▼               Detecta qué esencia falta para llegar al 100%
  [ ⚙️ Motor Python ] ─► Audita reglas: CNP <= 4.5ml | Total = 30.0ml
        │               Calcula escandallo de costes (€) por 100ml
        ▼
  [ 📊 Base de Datos ] ► Añade la ficha técnica al CSV maestro (Listo para BI)
```

---

## 🧩 Automatización con funciones

El código está dividido en funciones modulares, claras y fáciles de mantener:

* **`asegurar_entorno()`** 🛠️  
  Detecta la carpeta de trabajo mediante rutas relativas (`os.getcwd()`). Si es la primera vez que se arranca la tienda, crea automáticamente la tabla CSV maestra con sus 22 columnas estructuradas.
* **`obtener_cliente_ia()`** 🔐  
  Gestiona la conexión segura con Google GenAI leyendo la clave desde variables de entorno (`GEMINI_API_KEY`), evitando exponer credenciales privadas en el código fuente.
* **`clonar_perfume()`** 🧠  
  Es el cerebro del sistema. Lanza la petición a la API de Gemini, aplica las reglas de seguridad química, imprime en pantalla el diagnóstico completo (fórmula actual, porcentaje de parecido, recomendación de compra y receta ideal al 100 %) y dispara el guardado.
* **`guardar_receta_en_csv()`** 📈  
  Cruza los mililitros finales con las tarifas unitarias de cada materia prima, calcula el coste total de producción por cada 100 ml, asigna un `ID` incremental y guarda la nueva fila en `tabla_maestra_15_recetas_completa.csv`.

---

## 🛠️ Stack Tecnológico

* **Lenguaje:** Python 3
* **Entorno de Desarrollo:** Jupyter Notebook (`.ipynb`)
* **Inteligencia Artificial:** Google GenAI SDK (`gemini-3.5-flash-lite`)
* **Ingeniería de Datos:** Pandas & JSON
* **Persistencia:** CSV (`utf-8-sig`) listo para conectar con Power BI o Excel

---

## ⚡ Guía Rápida: Cómo Probarlo en 3 Pasos

### 1. Clona el repositorio e instala las librerías
```bash
git clone https://github.com
cd ai-perfume-formulator-automation
pip install -r requirements.txt
```

### 2. Consigue tu API Key gratuita
Entra en [Google AI Studio](https://google.com) y genera tu clave gratuita en un clic.

### 3. Ejecuta el Notebook
1. Abre el archivo `.ipynb` en Jupyter o VS Code.
2. Ejecuta la **Celda 1** para inicializar el motor de formulación.
3. En la **Celda 2**, pega tu clave de API, escribe el perfume que quieras clonar y pulsa **Play**:

```python

# Configura tu clave de Google AI Studio (nunca la subas a repositorios públicos)
os.environ["GEMINI_API_KEY"] = "TU_API_KEY_AQUI"

# ¡Listo! Pide cualquier fragancia y observa la magia
clonar_perfume("Dior Sauvage")
```

---

## 🖥️ Ejemplo Real de Resultado en Pantalla

```text
🔍 Analizando perfume objetivo: DIOR SAUVAGE...

🏷️ MARCA: Christian Dior | ORIGINAL: 115.0€ / 100ml
📝 DESCRIPCIÓN: Fragancia aromática fougère fresca y especiada con salida cítrica vibrante y fondo ambarado limpio.
📌 NOTAS: Bergamota de Calabria, Pimienta, Lavanda, Ambroxan, Cedro

🧪 FÓRMULA ADAPTADA AL 30% (Con tu inventario actual):
   • Fijador (Dimeticona): 1.0 ml
   • Bergamota: 14.5 ml
   • Canela/Naranja/Patchouli (Max 15%): 3.5 ml
   • Ámbar: 7.0 ml
   • Musk: 5.0 ml
   • Alcohol 96º: 69.0 ml
--------------------------------------------------------
📊 SIMILITUD ESTIMADA: 88%
🟡 BASTANTE BIEN. Equivalencia muy disfrutable.

🎯 RECETA IDEAL (Para llegar al 100% en el futuro):
   • Recomendación de compra: Ambroxan (~7.50€ / 50ml)
   • Fijador: 1.0 ml | Bergamota: 10.0 ml | Ambroxan: 12.0 ml | ... | Alcohol 96º: 69.0 ml

💾 [AUTO-GUARDADO]: Receta añadida al CSV maestro (ID: 21).
```

---

<div align="center">

### 👨‍💻 Desarrollado por **Sergio Martínez Jiménez**
*Data & Automation Junior · Python · SQL · APIs & IA · Power BI*


</div>
