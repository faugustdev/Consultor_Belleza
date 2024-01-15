# Documentación del Modelo Consultor de Belleza

### El Consultor de Belleza es un sistema de recomendación diseñado para proporcionar orientación en el cuidado estético y analizar el comportamiento del usuario durante el tratamiento para optimizar las   recomendaciones de productos.

## Objetivo

### En esta primera etapa, nos centraremos en el perfil del usuario para el cuidado de la piel y la recomendación de productos asociados. El modelo utiliza técnicas avanzadas de recomendación, incluida la   Descomposición de Valor Singular (SVD), para ofrecer sugerencias personalizadas basadas en las preferencias y necesidades individuales de cada usuario.

## Funcionalidades Principales

- Recomendación personalizada de productos para el cuidado de la piel.
- Análisis del comportamiento del usuario para mejorar las sugerencias.
- Adaptación continua a medida que el usuario avanza en su tratamiento.

### Este documento proporciona una guía detallada sobre la implementación y uso del Consultor de Belleza, abordando aspectos técnicos, métodos de entrenamiento del modelo y detalles sobre la interfaz del usuario.

## 1. Interacción de Datos

En el contexto del Consultor de Belleza, se utilizan dos conjuntos de datos clave que proporcionan información esencial sobre los usuarios y los productos. A continuación, se describen estos conjuntos y cómo interactúan:

### Conjunto de Datos de Preguntas al Usuario

Este conjunto de datos contiene respuestas a preguntas relacionadas con el perfil del usuario para el cuidado de la piel. Cada entrada en el conjunto de datos representa un usuario y sus respuestas a diversas preguntas sobre textura de piel, brillo, tono, granitos, enrojecimiento, irritación, tirantez, poros abiertos, alergias cosméticas y tipo de piel. 

**Columnas:**
- Textura_Piel_Num
- Piel_Brillante_Num
- Tono_Piel_Num
- Granitos_Imperfecciones_Num
- Enrojece_Facilidad_Num
- Irritacion_Piel_Num
- Tirantez_Sequedad_Num
- Poros_Abiertos_Num
- Alergia_Cosmeticos_Num
- Tipo_Piel_Num

### Conjunto de Datos de Cosméticos

Este conjunto contiene información detallada sobre los productos cosméticos disponibles. Cada entrada representa un producto y proporciona detalles como la combinación, el grupo de nombre, el grupo de marca, nombre, marca, categoría de precio, clasificación, etiqueta y otros atributos relevantes.

**Columnas:**
- Combination
- Name_Group_Num
- Brand_Group_Num
- Name
- Brand
- Price_Category
- Rank_Num
- Label_Num

### Conjunto de Datos Unificado

Para mejorar las recomendaciones, se realiza una unión entre los conjuntos de datos de preguntas al usuario y cosméticos. Esto crea un conjunto de datos unificado que incorpora tanto la información del usuario como la de los productos.

**Columnas Resultantes:**
- Combination
- Name_Group_Num
- Brand_Group_Num
- Name
- Brand
- Price_Category
- Rank_Num
- Label_Num
- Textura_Piel_Num
- Piel_Brillante_Num
- Tono_Piel_Num
- Granitos_Imperfecciones_Num
- Enrojece_Facilidad_Num
- Irritacion_Piel_Num
- Tirantez_Sequedad_Num
- Poros_Abiertos_Num
- Alergia_Cosmeticos_Num
- Tipo_Piel_Num

Esta unión de datos proporciona una base completa para el entrenamiento y la generación de recomendaciones personalizadas.

## 2. Preparación del Conjunto de Datos

Durante la preparación del conjunto de datos para el modelo del Consultor de Belleza, se llevan a cabo los siguientes pasos utilizando las clases proporcionadas por la biblioteca Surprise:

### Reader

Se emplea la clase `Reader` para especificar la escala de calificación, que en este caso va de 1 a 14. La clase `Reader` también permite configurar otros aspectos relacionados con los datos, proporcionando una estructura clara para la interpretación de las calificaciones.

### Dataset

Utilizando la clase `Dataset`, se carga el conjunto de datos desde el dataframe. Se seleccionan las columnas relevantes, como `Name_Group_Num`, `Textura_Piel_Num`, `Brillo_Piel_Num`, etc. Esta clase facilita la representación y manipulación eficientes de los datos, preparándolos para su uso en el modelo de recomendación.

Estos pasos son fundamentales para garantizar que los datos sean adecuadamente interpretados por el modelo y que la información relevante se incorpore de manera efectiva en el proceso de recomendación del Consultor de Belleza.

## 3. Definición y Ajuste de Hiperparámetros

Antes de entrenar el modelo, se definen los hiperparámetros que serán ajustados para optimizar el rendimiento del algoritmo de recomendación. Para lograr esto, se utiliza la técnica de búsqueda de cuadrícula (GridSearch), donde se exploran diversas combinaciones de hiperparámetros para encontrar los valores óptimos.

## 4. División del Conjunto de Datos

El conjunto de datos se divide en conjuntos de entrenamiento y prueba para evaluar el rendimiento del modelo. Esta división garantiza que el modelo sea evaluado de manera imparcial en datos no vistos durante el entrenamiento, lo que ayuda a estimar su capacidad de generalización.

## 5. Entrenamiento del Modelo

En esta etapa, se selecciona el algoritmo de recomendación, siendo SVD una elección común debido a su eficacia en problemas de filtrado colaborativo. El proceso de entrenamiento se realiza de la siguiente manera:

- **Selección del Algoritmo:** Se elige el algoritmo, en este caso, SVD.
- **Instanciación del Modelo:** Se crea una instancia del modelo utilizando la implementación proporcionada por la biblioteca.
- **Entrenamiento:** El modelo se entrena utilizando el conjunto de entrenamiento. Durante este proceso, el algoritmo ajusta sus parámetros internos para aprender patrones y relaciones en los datos.

Estos pasos son cruciales para establecer la capacidad predictiva del modelo y asegurar que esté listo para realizar recomendaciones personalizadas basadas en las preferencias del usuario y las características de los productos.

## 6. Generación de Recomendaciones:
Después de entrenar el modelo, se pueden generar recomendaciones para usuarios específicos.
Las recomendaciones se generan utilizando funciones proporcionadas por la biblioteca de recomendación.
