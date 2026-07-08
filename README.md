# Hadoop Streaming - WordCount con Python

Este repositorio contiene una implementación clásica del algoritmo **WordCount** utilizando **Hadoop Streaming** con scripts desarrollados en **Python 3**. El proyecto simula y analiza el impacto del paralelismo modificando el número de tareas de reducción en un entorno local.

---

## 📋 Requisitos
* Hadoop 3.x (con soporte para Hadoop Streaming Jar)
* Python 3.x
* Entorno Linux o entorno basado en la nube (ej. Google Colab)

---

## 🛠️ Estructura del Proyecto
* `mapper.py`: Script en Python encargado de leer líneas de texto de `stdin`, limpiar/separar palabras y emitir pares clave-valor `(palabra, 1)`.
* `reducer.py`: Script en Python que recibe las claves ordenadas de `stdin`, acumula los contadores y emite el total por palabra.
* `mi_dataset.txt`: Archivo de texto de prueba utilizado como entrada.

---

## 🚀 Ejecución del Job

Para lanzar el trabajo de MapReduce especificando el número de Reducers, utiliza el siguiente comando base:

```bash
mapred streaming \
  -files mapper.py,reducer.py \
  -input /content/mi_dataset.txt \
  -output /content/resultado_wordcount \
  -mapper "python3 mapper.py" \
  -reducer "python3 reducer.py" \
  -numReduceTasks 1
