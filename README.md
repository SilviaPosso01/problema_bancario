# SIMULACIÓN BANCO DE COLOMBIA — ANÁLISIS M/M/1

Este notebook contiene una simulación de un sistema de atención al cliente en un banco, utilizando el modelo de colas M/M/1 (llegadas Poisson, servicio exponencial, 1 servidor). El objetivo es analizar diferentes configuraciones de cajeros y tipos de clientes para optimizar los tiempos de espera y servicio.

## Parámetros Globales de la Simulación

- **Tiempo Total de Simulación**: 480 minutos (8 horas)
- **Número de Cajeros**: 3 (en la configuración base)
- **Número de Réplicas**: 10
- **Probabilidad de Retiro**: 70%
- **Probabilidad de Pago**: 30%

Se definen diferentes tipos de usuarios (Rápido, Normal, Lento, Muy Lento) para Retiros y Pagos, cada uno con su propia media de tiempo de servicio y tiempo entre llegadas.

## Puntos Clave de Análisis y Resultados

La simulación aborda 5 puntos principales, detallados a continuación:

### Punto 1: Cajero con menor y mayor tiempo promedio de atención

Se analiza el tiempo promedio de servicio de cada cajero a lo largo de las 10 réplicas. Se identifican el cajero más rápido y el más lento, proporcionando métricas como la media, desviación estándar e intervalos de confianza del 95% para el tiempo de servicio.

**Resultados:**
- **Cajero MÁS RÁPIDO**: Se identifica el cajero con el menor tiempo promedio de servicio.
- **Cajero MÁS LENTO**: Se identifica el cajero con el mayor tiempo promedio de servicio.

### Punto 2: Promedio de usuarios por tipo en todos los cajeros

Se calcula el promedio de usuarios por tipo de transacción (Retiro o Pago) y por categoría de usuario (Rápido, Normal, Lento, Muy Lento) a través de todas las réplicas. Se incluyen intervalos de confianza del 95% para estos promedios.

**Resultados:**
- Detalle del promedio de usuarios para cada combinación de acción y tipo de usuario.
- Total promedio de usuarios por réplica.

### Punto 3: Total de usuarios por tipo en cada réplica y la réplica con menos clientes

Se tabulan los totales de usuarios por tipo de acción y categoría de usuario para cada una de las réplicas. Además, se identifica la réplica que resultó en la menor cantidad total de usuarios.

**Resultados:**
- Tabla pivote con el desglose de usuarios por réplica, acción y tipo.
- Identificación de la réplica con la menor cantidad de usuarios totales.

### Punto 4: ¿Necesidad de un nuevo cajero? (Análisis de tiempos de espera)

Se evalúa el tiempo promedio de espera en cola (Wq) y el tiempo en el sistema (W) para cada cajero y de manera global. Se utiliza un umbral de 5 minutos de espera como indicador para la posible necesidad de un cajero adicional.

**Resultados:**
- Métricas de espera (Wq, W) y factor de utilización (ρ) promedio por cajero.
- Tiempo global de espera promedio (Wq) y tiempo global en sistema promedio (W), con sus respectivos intervalos de confianza.
- Comparación con el umbral de 5 minutos para determinar si se recomienda un cajero adicional.
- Análisis de estabilidad (ρ < 1).

### Punto 5: Configuración óptima (cajas especializadas)

Se simulan diferentes configuraciones de cajeros (mixtos, especializados en retiros o pagos, y un aumento de cajeros a 4) para identificar cuál ofrece el menor tiempo de espera en cola (Wq).

**Configuraciones Evaluadas:**
- Mixta (3 Cajeros)
- 2 Cajeros de Retiro + 1 Cajero de Pago
- 1 Cajero de Retiro + 2 Cajeros de Pago
- 4 Cajeros Mixtos

**Resultados:**
- Tabla comparativa de Wq, W, T_srv y N promedio/día para cada configuración.
- Identificación de la configuración óptima (la de menor Wq).
- Análisis separado de Wq y W para retiros y pagos en la configuración mixta para entender cuál operación genera mayor espera.

## Visualizaciones

El notebook genera una serie de gráficos para visualizar los resultados de los 5 puntos de análisis, incluyendo:

- Tiempo Promedio de Servicio por Cajero a lo largo de las réplicas.
- Boxplot del Tiempo de Servicio por Cajero.
- Promedio de Usuarios por Tipo (con IC 95%).
- Total de Usuarios por Réplica.
- Tiempo Promedio de Espera (Wq) por Cajero.
- Comparación de Wq entre las diferentes configuraciones.

Todas las gráficas se guardan en el archivo `graficas_banco.png` dentro del directorio `sample_data/`.

## Archivos Generados

Los resultados detallados de cada punto de análisis se han guardado en archivos CSV dentro del directorio `sample_data/`:

- `resultados_completos.csv`: Contiene todos los datos generados por la simulación.
- `punto1_cajeros.csv`: Resumen del tiempo promedio de atención por cajero.
- `punto2_usuarios.csv`: Promedio de usuarios por tipo.
- `punto3_replicas.csv`: Total de usuarios por tipo en cada réplica.
- `punto4_espera.csv`: Métricas de espera por cajero.
- `punto5_configs.csv`: Comparación de las diferentes configuraciones.
- `graficas_banco.png`: Archivo de imagen con todas las visualizaciones.