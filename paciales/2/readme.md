# 📝 Solución Parcial 2 - Señales y Sistemas

Este repositorio contiene la solución desarrollada para el **Parcial 2** del curso de **Señales y Sistemas - 2025-II**, implementado como un **Dashboard interactivo con Streamlit**.

---

## ✅ Contenido del parcial

### 1. 🎧 Demodulador AM (DSB-CS)

**Objetivo:** Analizar el proceso completo de modulación y demodulación AM DSB-CS utilizando 5 segundos de una canción de YouTube como señal mensaje.

#### 🔍 Etapas implementadas:
- Descarga del audio (YouTube) y recorte a 5 segundos.
- Modulación AM con portadora \( \cos(2\pi f_c t) \).
- Demodulación por mezcla con portadora local (sin desfase).
- Filtrado pasa bajas usando FFT (Transformada Rápida de Fourier).
- Escalado final para recuperar la señal original.

#### 💡 Espectro de Fourier:
- El espectro en cada etapa fue graficado usando FFT y mostrado en el dashboard.
- Las gráficas incluyen: señal original, modulada, mezcla y recuperada, tanto en **tiempo** como en **frecuencia**.

---

### 2. ⚙️ Sistema Masa-Resorte-Amortiguador y Circuito Equivalente

#### 🧮 Parte 1: Modelo mecánico

**Ecuación diferencial:**

\[
m\ddot{y}(t) + c\dot{y}(t) + ky(t) = F_e(t)
\]

**Transformada de Laplace (condiciones iniciales cero):**

\[
m s^2 Y(s) + c s Y(s) + k Y(s) = F_e(s)
\]

**Función de transferencia mecánica:**

\[
H(s) = \frac{Y(s)}{F_e(s)} = \frac{1}{m s^2 + c s + k}
\]

---

#### 🔌 Parte 2: Sistema eléctrico equivalente

**Ecuaciones basadas en el circuito (leyes de Kirchhoff):**

\[
V_i(s) = L s I_1(s) + \frac{1}{Cs} (I_1(s) - I_2(s)), \quad V_o(s) = R I_2(s)
\]

**Función de transferencia del circuito:**

\[
\frac{V_o(s)}{V_i(s)} = \frac{1}{L C s^2 + \frac{L}{R} s + 1}
\]

**Tabla de equivalencias:**

| Sistema Mecánico | Sistema Eléctrico |
|------------------|-------------------|
| Masa \( m \)     | Inductancia \( L \) |
| Amortiguador \( c \) | Resistencia \( R \) |
| Resorte \( k \)   | \( \frac{1}{C} \) |

---

### 3. 📊 Simulación de sistemas de segundo orden

Se simulan 3 condiciones según el **factor de amortiguamiento \( \zeta \)**:

| Tipo               | Condición       |
|--------------------|-----------------|
| Subamortiguado     | \( \zeta < 1 \) |
| Crítico            | \( \zeta = 1 \) |
| Sobreamortiguado   | \( \zeta > 1 \) |

#### 📌 Parámetros simulados:
- Valores de \( m, c, k \) propuestos.
- Equivalentes eléctricos \( R = c, L = m, C = 1/k \).
- Cálculo de:

\[
\zeta = \frac{c}{2 \sqrt{km}}, \quad \omega_n = \sqrt{\frac{k}{m}}, \quad \omega_d = \omega_n \sqrt{1 - \zeta^2}
\]

\[
T_p = \frac{\pi}{\omega_d}, \quad T_r \approx \frac{1.8}{\omega_n}, \quad T_s \approx \frac{4}{\zeta \omega_n}
\]

---

### 4. 🔁 Simulación en tiempo y frecuencia

Para cada sistema se generaron:

- 📈 **Diagrama de polos y ceros**
- 🔊 **Respuesta al impulso**
- ⏫ **Respuesta al escalón**
- 🔁 **Respuesta a la rampa**
- 🌀 **Diagrama de Bode (magnitud y fase)**

También se incluyó el análisis en **modo lazo cerrado**.

---

## 💻 Implementación

- Todo el parcial está implementado como un **Dashboard Streamlit** dividido en páginas:
  - `0_Inicio.py` – Pantalla principal.
  - `pages/1_Presentacion.py` – Descripción general del parcial.
  - `pages/2_Demodulador_AM.py` – Ejercicio 1 completo.
  - `pages/3_Sistema_Masa_Resorte.py` – Ejercicio 2 interactivo con simulaciones y control de parámetros.

- Los códigos están documentados y estructurados en el archivo:  
  `parcial_señales_final.ipynb`

---

## 🎓 Créditos

> **Curso:** Señales y Sistemas  
> **Profesor:** Andrés Marín Álvarez Meza, Ph.D.  
> **Universidad Nacional de Colombia** – Sede Manizales  


---

# Dashboard Parcial 2 - Senales y Sistemas (2025-II)

Repositorio con el dashboard multipagina en Streamlit para los dos ejercicios del parcial:
- **Ejercicio 1:** Demodulador AM (DSB-SC) usando audio de YouTube.
- **Ejercicio 2:** Sistema masa-resorte-amortiguador con simulaciones en lazo abierto y cerrado.

## Contenido del dashboard
- `0_Inicio.py`: portada y estructura del proyecto.
- `pages/1_Presentacion.py`: descripcion general y librerias usadas.
- `pages/2_Ejercicio1_DemoduladorAM.py`: flujo completo del demodulador AM (descarga, modulacion, demodulacion, audios y graficas tiempo/frecuencia).
- `pages/3_Ejercicio2_MasaResorte.py`: simulador interactivo con:
  - Selector de tipo de sistema (subamortiguado, critico, sobreamortiguado) que calcula `c = 2*zeta*sqrt(m*k)` de forma automatica.
  - Opcion de forzar un valor manual de `c`.
  - Respuestas de lazo abierto: polos/ceros, Bode, impulso, escalon, rampa.
  - Respuesta al escalon en lazo cerrado con realimentacion unitaria para comparar desempeno.

## Ejecucion en Google Colab (notebook `parcial_senales_final.ipynb`)
Incluye todas las celdas necesarias:
1. Instalacion de dependencias (streamlit, yt-dlp, pydub, librosa, scipy, matplotlib, soundfile, control, ffmpeg, cloudflared).
2. Generacion de archivos con `%%writefile` para las paginas de Streamlit.
3. Lanzar Streamlit y el tunel de cloudflared (muestra la URL publica `trycloudflare`).

Ejecuta las celdas en orden y abre la URL impresa para usar el dashboard.

## Ejecucion local rapida
```bash
pip install streamlit yt-dlp pydub librosa scipy matplotlib soundfile control
streamlit run 0_Inicio.py
```

## Resumen tecnico breve
### Ejercicio 1 — Demodulador AM
- Descarga y recorte de 5 s desde YouTube.
- Modula en AM DSB-SC y demodula coherente con filtro pasabajas ideal (FFT).
- Exporta audios: `mensaje.wav`, `modulada.wav`, `mezcla.wav`, `recuperada.wav`.
- Graficas en tabs: tiempo y frecuencia para cada etapa.

### Ejercicio 2 — Masa-Resorte-Amortiguador
- Modelacion: `H(s) = 1/(m s^2 + c s + k)` y analogia electrica.
- Parametros calculados: zeta, wn, wd, Tp, Tr, Ts.
- Selector de zeta con calculo automatico de `c`; opcion de `c` manual.
- Respuestas en lazo abierto: polos/ceros, Bode, impulso, escalon, rampa.
- Lazo cerrado: respuesta al escalon con retroalimentacion unitaria.
