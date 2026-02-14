# Performance Testing con Apache JMeter

##  Objetivo

Evaluar el comportamiento del sistema bajo diferentes escenarios de carga utilizando Apache JMeter, identificando capacidad, degradación y punto de quiebre.

---

#  Herramienta utilizada

- Apache JMeter 5.6.3
- CSV Data Set Config para parametrización dinámica

---

#  Diseño del Test Plan

El Test Plan incluye Thread Groups independientes por tipo de prueba:

- Concurrencia (10, 20 y 30 usuarios)
- Carga (25 usuarios – 5 minutos)
- Estrés (incremento progresivo hasta 250 usuarios)
- Picos (base + incremento agresivo)

Cada Thread Group contiene:

- HTTP Request
- CSV Data Set Config (users.csv)
- Response Assertion (validación código 200)
- Aggregate Report

---

#  Métricas Relevantes

##  Throughput Promedio (req/seg)

- Carga (25 usuarios): 75.72 req/seg
- Estrés (250 usuarios): 115.49 req/seg
- Pico Agresivo: 137 req/seg

---

## Tiempo de Respuesta

### Carga (25 usuarios)
- Promedio: 298 ms
- Mínimo: 0 ms
- Máximo: 5,344 ms

### Estrés (250 usuarios)
- Promedio: 1,795 ms
- Mínimo: 1 ms
- Máximo: 21,164 ms

### Pico
- Promedio: 1,408 ms
- Máximo: 23,751 ms

---

## Percentiles

### Carga
- 95%: 649 ms

### Estrés (250 usuarios)
- 95%: 21,035 ms

### Pico
- 90%: 1,065 ms
- 95%: 6,427 ms
- 99%: 22,217 ms


##  Total de Peticiones Enviadas

- Carga (5 min): 22,721
- Estrés (250 usuarios): 9,051
- Pico: 6,878



##  Total de Errores

Error promedio aproximado: ~1%

Se evidenciaron códigos distintos a 200 bajo escenarios de alta presión (4xx / 5xx).

---

#  Identificación del Punto de Quiebre

El sistema mantiene estabilidad hasta aproximadamente 100 usuarios concurrentes.

A partir de 250 usuarios:

- Incremento significativo del tiempo de respuesta
- Percentiles elevados (hasta 21 segundos)
- Disminución relativa del throughput
- Aparición de errores 4xx/5xx

Se identifica este rango como el punto de degradación severa del sistema.

---

# Estructura del Proyecto

- performance-testing-jmeter.jmx
- users.csv
- Thread Groups separados por tipo de prueba
- Response Assertions
- Aggregate Reports


#  Autor

Shary Garcia
