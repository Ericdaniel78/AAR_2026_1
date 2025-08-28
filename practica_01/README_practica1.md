# Práctica Quincenal 1 – Definición de producto y base de datos

El estudiante tiene que definir el producto y con ello crear un dataset simulado de pólizas.

## Objetivo

El objetivo de esta práctica es que los estudiantes aprendan a:

0. Definir coberturas, exclusiones y segmentos de un producto de seguros.
1. Acceder al portal de la CNSF y ubicar el **Sistema Estadístico de Seguros (SESA)**.
2. Seleccionar el ramo de interés de acuerdo con la **LISF (art. 25 y 26)**.
3. Descargar datos agregados (primas, siniestros, pólizas).
4. Derivar supuestos de **frecuencia y severidad**.
5. Simular una base de datos sintética que represente la cartera de pólizas de una aseguradora.

# Ejemplo:

Seguros de Autos (Ramo Daños), con las coberturas básicas de:
- Responsabilidad Civil (RC)
- Daños Materiales (DM) 
- ROBO Total
- Asistencia Vial (opcional)
- Gastos Médicos Ocupantes (opcional)


## 1. Acceso al portal de SESA
1. Ingresar a la página sobre  **"Información estadística" → "SESA" (Sistema Estadístico de Seguros).**:  
   👉 [SESA](https://www.cnsf.gob.mx/EntidadesSupervisadas/InstitucionesSociedadesMutualistas/Paginas/InformacionEstadistica.aspx)

2. Seleccionar **“Información estadística detallada del Sector Asegurador”**.  
   Ahí podrán elegir:
   - Ramo de seguros (Autos, Gastos Médicos, Vida, Hogar, Marítimo, etc.).
   - Periodo (Selecciona el ultimo año disponible).


### a. Selección del ramo conforme a la LISF
- El **artículo 25 de la LISF** establece que las instituciones solo pueden operar en los ramos autorizados.
- Ejemplo de clasificación:
  - **Vida** → seguros de vida, pensiones.  
  - **Daños** → autos, hogar, marítimo, agrícola.  
  - **Salud** → gastos médicos, accidentes personales.  
- **Restricciones (art. 26 LISF):**  
  Una aseguradora **no puede operar Vida y Daños a la vez**.

> **Ejemplo rápido (ficticio, Autos)**  
> Si tu equipo elige “Autos”, deberán ubicarlo bajo el ramo **Daños** en SESA.

---

## 2. Variables a descargar
De la base de SESA, descargar:
- **Primas emitidas y devengadas.**
- **Siniestros ocurridos y pagados.**
- **Número de pólizas.**
- **Índice de siniestralidad.**

---

## 3. Derivación de supuestos técnicos

Con los datos agregados, calcular:

- **Frecuencia:**  
   $$Frecuencia = \frac{\text{Número de siniestros}}{\text{Número de pólizas}}$$

- **Severidad:**  
   $$Severidad = \frac{\text{Monto de siniestros}}{\text{Número de siniestros}}$$

- **Prima pura esperada:**  
  $$\text{Prima pura} = Frecuencia \times Severidad$$


- **Prima comercial:**  
  Agregar gastos de adquisición, administración y utilidad esperada.

## a) ¿Cómo derivar **frecuencia y severidad**?

### Caso A – El cuadro trae **# de pólizas** y **# de siniestros**

- **Frecuencia** = (N.º de siniestros) / (N.º de pólizas)  
- **Severidad** = (Monto de siniestros) / (N.º de siniestros)

### Caso B – El cuadro NO trae **# de siniestros**

1. Calcula **LR** si no viene:  
   $$LR = \frac{\text{Siniestros}}{\text{Primas}}$$  

2. El **costo esperado por póliza** ≈ $LR \times \text{prima promedio}$


3. **Descomposición Frecuencia × Severidad**:  
   - Elige una **severidad promedio razonable** (literatura/benchmark) y despeja la **frecuencia**:  

   $$\text{Frecuencia} \approx \frac{\text{Costo esperado por póliza}}{\text{Severidad asumida}}$$

   - Alternativamente, fija una **frecuencia** (benchmark) y despeja la **severidad**.

> **Ejemplo rápido (ficticio, Autos)**  
> Primas devengadas = $12,000 millones; Siniestros = $9,000 millones; Pólizas = 1,000,000.  
> Prima promedio ≈ $12,000; LR = 75%.  
> Costo esperado por póliza = 0.75 × 12,000 = $9,000.  
> Si asumes severidad ≈ $60,000 → Frecuencia ≈ 9,000 / 60,000 = **15%**.  


---
# 4) Mix de coberturas
- El modelado se realiza pro cobertura entonces necesitas aplicar un  **mix de coberturas** que debe ser consistente con el producto elegido:


> **Ejemplo: Autos; RC, Daños materiales, Robo**  
> Si SESA no desagrega por cobertura, se puede suponer un mix con base en benchmarks: 
>- **Responsabilidad Civil (RC):** 40%  
>- **Daños Materiales (DM):** 35%  
>- **Robo Total (RT):** 25%  



### a. Ejemplo con ramo Autos (valores ficticios SESA)

- Primas devengadas = \$12,000 millones.  
- Siniestros = \$9,000 millones.  
- Pólizas = 1,000,000.  

**Cálculos:**
$$\text{Prima promedio} = \frac{12,000,000,000}{1,000,000} = 12,000 $$
$$LR = \frac{9,000}{12,000} = 75\%$$

Supongamos 150,000 siniestros estimados: (Supuesto dado por mi equipo)

$$Frecuencia = \frac{150,000}{1,000,000} = 15\%$$
$$Severidad = \frac{9,000,000,000}{150,000} \approx 60,000 $$

Primas y siniestros por cobertura

Cálculo proporcional:

- RC: Primas = 4,800 millones; Siniestros = 3,600 millones.  
  - $$Frecuencia_{RC} = 15\% \cot 40\% = 6\% $$
  - $$Severidad_{RC} = 60,000 \cot 40\% = 24,000$$
- DM: Primas = 4,200 millones; Siniestros = 3,150 millones. 
  - $$Frecuencia_{RC} = 15\% \cot 35\% = 5\% $$
  - $$Severidad_{RC} = 60,000 \cot 35\% = 21,000$$
- RT: Primas = 3,000 millones; Siniestros = 2,250 millones.  
  - $$Frecuencia_{RC} = 15\% \cot 25\% = 4\% $$
  - $$Severidad_{RC} = 60,000 \cot 25\% = 15,000$$

---


# 5. Checklist de coherencia (antes de simular)

- El **LR** que obtienes con tus supuestos debe ser cercano al del cuadro SESA del periodo elegido.  
- La **severidad media** y el **percentil 95** deben ser plausibles para el ramo/país.  
- Documenta en el reporte **de qué cuadro y periodo** tomaste los datos.  

---

# 6. Entregable.

1. Reporte en PDF con:
   - Evidencia de acceso a SESA.
     - **Cita el cuadro SESA** (nombre, URL o ruta en gob.mx/cnsf), **periodo** y **fecha de descarga**.
   - Ramo elegido y justificación (cita LISF).
     - Verifica que el **ramo** seleccionado corresponde a la **clasificación de la LISF** (Art. 25).
   - Supuestos técnicos obtenidos
     - **Justifica** el método (Caso A o B) y cualquier **supuesto de severidad/frecuencia**.   
   - Dataset simulado.
     - Archivo de simulación en **Rmd** o **Jupyter Notebook (.ipynb)**.

---


# Guias:

## Requisitos:

- R: `dplyr`, `tidyr`, `ggplot2`.
- Python: `numpy`, `pandas`.


## Archivos
- `practica1_autos_simulacion.Rmd`: plantilla en R Markdown.
- `practica1_autos_simulacion.ipynb`: plantilla en Python (Jupyter).
- 
- Al ejecutar, se generan:
  - `cartera_autos_simulada.csv`

## Pasos

1. Ajusta supuestos (frecuencia/severidad/gastos).
2. Ejecuta la simulación (R o Python).
3. Revisa KPIs por segmento (LR) y compara con objetivos.
4. Exporta CSV 


## Notas adicionales y recomendaciones

Los puntos anteriores describen el flujo general de la práctica. A
continuación se incluyen **recomendaciones complementarias** para
facilitar el trabajo y asegurar la coherencia de los resultados:

### Navegación detallada en SESA

La página de la CNSF puede ser complicada para quienes no la conocen.
Además de la descripción general en el punto 1, se sugiere lo siguiente:

-   Después de ingresar a la sección **"Información estadística
    detallada del Sector Asegurador"**, selecciona el **ramo** en el
    menú desplegable de la izquierda y el **periodo** (año) en el que
    deseas trabajar.
-   Al hacer clic en el ramo, la página mostrará un conjunto de cuadros
    en formato Excel; descarga el que corresponda a las variables que
    necesitas (primas, siniestros, pólizas).
-   Documenta la ruta exacta y el nombre del cuadro (por ejemplo:
    *SESA → Daños → Autos → Primas y Siniestros 2024*) y registra la
    fecha en que lo descargaste.
-   **Sugerencia:** puedes tomar capturas de pantalla como evidencia de
    que entraste a la plataforma y de los pasos seguidos.

### Estructura del dataset simulado

Al generar el archivo `cartera_autos_simulada.csv`, se recomienda incluir al menos las siguientes columnas:

| Columna              | Descripción                                                                 |
|-----------------------|-----------------------------------------------------------------------------|
| `id_poliza`           | Identificador único para cada póliza                                        |
| `segmento`            | Segmento de riesgo asignado (p. ej., Bajo riesgo, Estándar, Alto riesgo)   |
| `n_siniestros_DM`     | Número de siniestros en Daños Materiales                                    |
| `siniestro_DM`        | Monto total de siniestros de DM                                             |
| `n_siniestros_Robo`   | Número de siniestros por Robo Total                                         |
| `siniestro_Robo`      | Monto total de siniestros de Robo Total                                     |
| `n_siniestros_RC`     | Número de siniestros en Responsabilidad Civil                               |
| `siniestro_RC`        | Monto total de siniestros de RC                                             |
| `prima_DM_comercial`  | Prima comercial calculada para DM                                           |
| `prima_Robo_comercial`| Prima comercial para Robo                                                   |
| `prima_RC_comercial`  | Prima comercial para RC                                                     |
| `prima_total`         | Suma de las primas comerciales de las coberturas                           |
| `siniestro_total`     | Suma de los montos de siniestro de todas las coberturas                     |
| `LR`                  | Razón de siniestralidad (`siniestro_total` / `prima_total`)                 |

Esta estructura facilitará el análisis posterior, permitiendo calcular KPIs por cobertura y segmento, y comparar tus resultados con los indicadores de SESA.

---

### Definición de segmentos

Se propone definir tres segmentos ficticios:

| Segmento     | Probabilidad de pertenencia | Multiplicador de frecuencia | Descripción                                                      |
|--------------|------------------------------|-----------------------------|------------------------------------------------------------------|
| Bajo riesgo  | 30 %                         | 0.7                         | Conductores con buen historial y vehículos nuevos                |
| Estándar     | 50 %                         | 1.0                         | Perfil promedio                                                  |
| Alto riesgo  | 20 %                         | 1.5                         | Conductores jóvenes o zonas con mayor siniestralidad             |


Puedes ajustar las probabilidades y multiplicadores para reflejar tu
propio criterio de segmentación (edad del conductor, uso del vehículo,
ubicación geográfica, etc.). El objetivo es que la mezcla de segmentos
reproduzca la siniestralidad observada en SESA.

### Parámetros de severidad y percentiles

Se sugiere modelar los montos de siniestro mediante una distribución
**lognormal**. La media de la lognormal se consigue con
$\mu = \ln\left( \text{media} \right) - \frac{1}{2}\sigma^{2}$ , donde
$\sigma$ es la desviación estándar del logaritmo.

En el ejemplo se emplea $\sigma = 0.6$ , pero puedes variarlo para
reproducir colas más o menos pesadas. Además de la media, revisa el
**percentil 95** de la severidad resultante y asegúrate de que sea
plausible para el ramo/país.\

Recuerda que la severidad base se da por cobertura (DM = $21k,
Robo = $15k, RC = \$24k) y que debe ajustarse si tu benchmark
sugiere valores diferentes.


### Comparación con indicadores de SESA

Una vez simulada la cartera, compara los resultados con las estadísticas
de SESA:

-   **Pérdida promedio (LR):** calcula el LR agregado de tu simulación y
    verifica que sea similar al del cuadro de SESA para el periodo
    elegido.
-   **Severidad media y percentil 95:** compáralos con referencias de la
    industria o con el comportamiento observado en tu cuadro.
-   Si existen discrepancias significativas, ajusta los supuestos
    (frecuencia, severidad, mix de coberturas, segmentos) hasta lograr
    un alineamiento razonable.

### Evidencias y documentación

No olvides documentar todo el proceso: desde la justificación del ramo
elegido y la clasificación de la LISF, pasando por los supuestos
técnicos adoptados (caso A o B de la derivación de frecuencia y
severidad), hasta la descripción de los segmentos.
Incluye en tu reporte capturas de pantalla de la navegación en SESA, la
ruta completa de descarga y la fecha.
Esto facilitará la revisión y demostrará que las conclusiones se basan
en fuentes oficiales.

