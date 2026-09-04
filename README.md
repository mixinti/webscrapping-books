# Web Scraping Paralelo y Enriquecimiento de Datos con SQLite

Este repositorio contiene una solucion automatizada para la extraccion de datos, enriquecimiento mediante APIs externas y persistencia en una base de datos relacional local utilizando Python y SQLite.

## Caracteristicas Tecnicas

* **Concurrencia con Hilos:** Uso de `ThreadPoolExecutor` para paralelizar la descarga de paginas, extraccion de contenido y consultas a la API publica.
* **Control de Concurrencia (Thread Safety):** Implementacion de `threading.Lock` para gestionar de forma segura los accesos de lectura y escritura en los diccionarios de cache compartidos.
* **Consumo Eficiente de APIs:** Sistema de cache de dos niveles (Titulo-Autor y Autor-Perfil) para minimizar peticiones redundantes y evitar bloqueos por Rate Limiting (HTTP 429).
* **Base de Datos Optimizada:** Diseño relacional en SQLite con integridad referencial activa (`foreign_keys = ON`), modo de diario avanzado (`WAL`) e indices estrategicos para optimizar consultas de busqueda.

## Arquitectura de la Base de Datos

El sistema genera un esquema relacional compuesto por las siguientes entidades:
* `categories`: Catalogo unico de categorias de productos.
* `books`: Datos tecnicos y comerciales de los libros (UPC, precios con/sin impuestos, rating, disponibilidad).
* `authors`: Datos demograficos enriquecidos desde la API Open Library (año de nacimiento, pais, total de obras).
* `book_author`: Tabla intermedia que gestiona la relacion de muchos a muchos entre libros y autores.

## Arquitectura del Proyecto

* `Scraping Challenge.ipynb`: Notebook que contiene la configuracion inicial, definicion de funciones de extraccion, logica paralela y las consultas SQL de analisis.
* `books.db`: Base de datos SQLite generada automaticamente al ejecutar el proceso.
