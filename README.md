# Aplicación basada en Grafos para Analizar una Red de Distribución de Agua Grupo 6

> Aplicación desarrollada en **Python** para modelar una red de distribución de agua potable mediante **teoría de grafos**, permitiendo generar automáticamente un dataset, construir un grafo, validar su estructura y visualizar la red de forma gráfica utilizando **Pandas**, **NetworkX** y **Matplotlib**.

---

# Descripción

**Aplicación basada en Grafos para Analizar una Red de Distribución de Agua** es un proyecto académico desarrollado para la asignatura **Análisis de Algoritmos** de la **Universidad Espíritu Santo (UEES)**.

El proyecto tiene como objetivo representar computacionalmente la estructura de una red de distribución de agua potable inspirada en la urbanización **Ciudad Celeste – Etapa La Coralia**, ubicada en Samborondón, Ecuador. Debido a que el plano hidráulico oficial de la urbanización no es público, la red implementada corresponde a una **simplificación académica** diseñada únicamente con fines educativos.

La aplicación genera automáticamente un conjunto de datos compuesto por los principales elementos de la red (red pública, estaciones de bombeo, válvulas de sectorización y viviendas), construye un grafo utilizando la biblioteca **NetworkX**, verifica que toda la estructura sea consistente mediante diversas validaciones y finalmente genera una representación gráfica de la red utilizando **Matplotlib**.

El modelo desarrollado corresponde a un **análisis topológico**, es decir, representa cómo están conectados los distintos componentes de la red y verifica su estructura mediante teoría de grafos. No realiza simulaciones hidráulicas relacionadas con presión, caudal, velocidad del agua o pérdidas de energía, ya que dichas funcionalidades pertenecen a herramientas especializadas como EPANET y WNTR.

---

# Objetivos del Proyecto

## Objetivo General

Desarrollar una aplicación basada en teoría de grafos que permita modelar una red de distribución de agua potable mediante la generación automática de un dataset, la construcción de un grafo y la validación de su estructura.

## Objetivos Específicos

- Diseñar una red inspirada en Ciudad Celeste – Etapa La Coralia.
- Generar automáticamente los archivos **nodos.csv** y **tuberias.csv**.
- Representar la red mediante un grafo Ponderado, Dirigido utilizando NetworkX.
- Validar la consistencia estructural del dataset generado.
- Comprobar que el grafo sea conexo y no presente ciclos.
- Generar una representación gráfica del modelo.
- Preparar la estructura necesaria para futuras simulaciones de conectividad y análisis de la red.

---

# Flujo General del Proyecto

```text
                  Diseño de la Red
                         │
                         ▼
             configuracion_red.py
                         │
                         ▼
             generar_dataset.py
                         │
                         ▼
       nodos.csv + tuberias.csv
                         │
                         ▼
               crear_grafo.py
                         │
                         ▼
             Grafo (NetworkX)
                         │
                         ▼
             validar_grafo.py
                         │
                         ▼
        Verificación del Dataset
                         │
                         ▼
           visualizar_grafo.py
                         │
                         ▼
             Imagen del Grafo
                         │
                         ▼
               Resultados Finales
```

---

# Características Principales

✔ Generación automática del dataset.

✔ Construcción del grafo mediante NetworkX.

✔ Validación automática de la estructura de la red.

✔ Representación gráfica del modelo.

✔ Dataset completamente reproducible.

✔ Grafo finito, simple, no dirigido, ponderado, conexo y con estructura de árbol.

✔ Código organizado en módulos independientes.

✔ Arquitectura preparada para futuras simulaciones de conectividad.
---

# Stack Tecnológico

El proyecto fue desarrollado utilizando tecnologías y bibliotecas de Python orientadas al procesamiento de datos, construcción de grafos y visualización de información. Cada una cumple una función específica dentro de la aplicación.

| Capa / Módulo | Tecnología |
|---------------|------------|
| Lenguaje de programación | Python 3 |
| Manipulación del dataset | Pandas |
| Construcción del grafo | NetworkX |
| Visualización del grafo | Matplotlib |
| Gestión de rutas | Pathlib |
| Archivos de datos | CSV |

---

# Estructura del Repositorio

```text
proyecto-red-distribucion-agua/
│
├── configuracion_red.py          # Define toda la estructura de la red
├── generar_dataset.py            # Genera automáticamente los archivos CSV
├── crear_grafo.py                # Construye el grafo utilizando NetworkX
├── validar_grafo.py              # Ejecuta todas las validaciones del dataset y del grafo
├── visualizar_grafo.py           # Dibuja y exporta la imagen del grafo
├── main.py                       # Ejecuta todo el flujo del proyecto
│
├── datos/
│   ├── nodos.csv
│   └── tuberias.csv
│
├── imagenes/
│   ├── grafo_red.png
│   ├── Ciudadela-Ciudad Celeste.png
├── capturas/
│   ├── dataset.png
│   ├── grafo.png
│   ├──Ciudadela-Ciudad Celeste.png
│   
│
└── README.md
```

---

# Arquitectura del Sistema

La aplicación sigue una arquitectura modular donde cada archivo Python tiene una responsabilidad específica dentro del proceso de generación y análisis de la red. Esta separación facilita el mantenimiento del código, permite realizar modificaciones sin afectar el resto del proyecto y hace que cada etapa del proceso pueda entenderse de forma independiente.

Todo el flujo comienza con la definición de la red en **configuracion_red.py**. A partir de esa configuración se generan los archivos del dataset, posteriormente se construye el grafo, se valida su estructura y finalmente se genera una representación gráfica del modelo.

```text
                   configuracion_red.py
                             │
                             ▼
                  generar_dataset.py
                             │
                             ▼
                nodos.csv     tuberias.csv
                             │
                             ▼
                    crear_grafo.py
                             │
                             ▼
                  Grafo de NetworkX
                             │
                             ▼
                   validar_grafo.py
                             │
                             ▼
                  visualizar_grafo.py
                             │
                             ▼
                     grafo_red.png
```

Cada módulo depende únicamente del resultado generado por el módulo anterior, permitiendo que el proyecto tenga un flujo de trabajo claro, ordenado y fácilmente escalable.

---

# Arquitectura del Modelo

La red implementada representa una distribución jerárquica inspirada en una urbanización cerrada.

El agua ingresa desde la conexión con la red pública (**RP**), pasa hacia la estación de bombeo principal (**B1**) y posteriormente se distribuye hacia los distintos sectores mediante válvulas de sectorización. Para abastecer el sector sur existe una segunda estación de bombeo (**B2**), desde donde se alimentan las dos últimas manzanas del modelo.

```text
                 Red Pública (RP)
                         │
                         ▼
                 Estación B1
          ┌──────┼──────┬──────┐
          ▼      ▼      ▼      ▼
         V1     V2     V3 ... V8
          │      │      │
      Viviendas Viviendas Viviendas

                 │
                 ▼
               Estación B2
                 │
            ┌────┴────┐
            ▼         ▼
           V9        V10
            │         │
      Viviendas   Viviendas
```

Esta estructura corresponde a una **red ramificada**, donde cada derivación abastece únicamente un conjunto específico de viviendas.

---

# Componentes de la Red

El modelo está compuesto por cuatro tipos principales de nodos.

| Componente | Cantidad | Función |
|------------|---------:|---------|
| Red Pública | 1 | Punto de ingreso del agua hacia la urbanización. |
| Estaciones de Bombeo | 2 | Mantienen la distribución del agua hacia los diferentes sectores. |
| Válvulas de Sectorización | 10 | Dividen la red por manzanas y controlan el suministro hacia cada sector. |
| Viviendas | 37 | Representan los puntos finales de consumo de agua. |

En conjunto, estos componentes forman una red de **50 nodos** conectados mediante **49 tuberías**, representadas como aristas dentro del grafo.

---

# Distribución de las Viviendas

Las viviendas se organizaron siguiendo la distribución general de la urbanización utilizada como referencia.

| Manzana | Válvula | Viviendas | Sector |
|----------|----------|-----------|--------|
| MZ-E1 | V1 | C1 – C4 | Este |
| MZ-E2 | V2 | C5 – C7 | Este |
| MZ-E3 | V3 | C8 – C10 | Este |
| MZ-E4 | V4 | C11 – C14 | Este |
| MZ-O1 | V5 | C15 – C21 | Oeste |
| MZ-O2 | V6 | C22 – C24 | Oeste |
| MZ-O3 | V7 | C25 – C27 | Oeste |
| MZ-O4 | V8 | C28 – C31 | Oeste |
| MZ-S1 | V9 | C32 – C34 | Sur |
| MZ-S2 | V10 | C35 – C37 | Sur |

Cada válvula abastece únicamente las viviendas pertenecientes a su manzana, manteniendo la estructura jerárquica definida durante el diseño del modelo.

---
---

# Funcionamiento de la Aplicación

La aplicación fue desarrollada siguiendo una arquitectura modular, donde cada archivo Python tiene una responsabilidad específica dentro del proceso de construcción del modelo. Esta organización permite que cada etapa del proyecto sea independiente, facilitando el mantenimiento, las pruebas y futuras ampliaciones.

El flujo completo de ejecución comienza con la definición de la estructura de la red, continúa con la generación automática del dataset, posteriormente construye el grafo, verifica la consistencia de toda la información y finalmente genera una representación gráfica del modelo.

```text
configuracion_red.py
        │
        ▼
generar_dataset.py
        │
        ▼
nodos.csv + tuberias.csv
        │
        ▼
crear_grafo.py
        │
        ▼
Grafo dirigido y ponderado
        │
        ▼
validar_grafo.py
        │
        ▼
visualizar_grafo.py
        │
        ▼
grafo_red.png
```

---

# Módulos del Proyecto

Cada módulo implementa una etapa específica dentro del proceso de construcción del modelo de la red de distribución de agua.

---

## configuracion_red.py

Este archivo constituye la base del proyecto. Aquí se define toda la estructura lógica de la urbanización que posteriormente será utilizada para generar el dataset.

Dentro de este módulo se encuentran definidos:

- La organización de las manzanas.
- Las válvulas de sectorización.
- Las estaciones de bombeo.
- La conexión con la red pública.
- La distribución de las viviendas.
- Las conexiones entre cada componente.
- Las longitudes de las tuberías.

Toda esta información permanece centralizada, permitiendo modificar el diseño completo de la red sin necesidad de alterar el resto del código de la aplicación.

---

## generar_dataset.py

Este módulo se encarga de transformar la información definida en **configuracion_red.py** en un conjunto de datos estructurado.

Durante su ejecución se generan automáticamente los archivos:

```text
nodos.csv
tuberias.csv
```

El proceso consiste en recorrer toda la configuración de la red, construir listas de información utilizando diccionarios de Python y convertirlas posteriormente en **DataFrames** mediante la biblioteca **Pandas**.

Finalmente, ambos DataFrames son exportados en formato CSV utilizando codificación UTF-8, permitiendo que puedan abrirse directamente desde Excel u otras herramientas de análisis de datos.

Una característica importante de este módulo es que **la generación del dataset es completamente determinista**, por lo que cada ejecución produce exactamente los mismos resultados.

---

## crear_grafo.py

Una vez generado el dataset, este módulo construye la representación computacional de la red mediante la biblioteca **NetworkX**.

Inicialmente se leen los archivos **nodos.csv** y **tuberias.csv**, agregando posteriormente todos los componentes de la red como nodos del grafo.

Después se incorporan las tuberías como aristas, asignando a cada una sus respectivos atributos.

Entre los atributos almacenados se encuentran:

- Identificador de la tubería.
- Longitud.
- Diámetro.
- Material.
- Estado.
- Peso de la arista.

La longitud de cada tubería se utiliza como **peso (weight)** del grafo, permitiendo que posteriormente puedan aplicarse algoritmos de búsqueda de rutas y caminos mínimos.

Antes de incorporar cada conexión, el programa verifica que ambos nodos existan dentro del dataset, evitando crear componentes inexistentes por errores de digitación.

---

## Características del Grafo

La estructura obtenida presenta las siguientes características:

| Característica | Descripción |
|----------------|-------------|
| Tipo | Grafo dirigido |
| Peso | Longitud de cada tubería |
| Total de nodos | 50 |
| Total de aristas | 49 |
| Componentes | Red pública, estaciones de bombeo, válvulas y viviendas |
| Representación | NetworkX |
| Peso de las aristas | Longitud de la tubería en metros |

El uso de un **grafo dirigido** permite representar el sentido del flujo definido para el abastecimiento dentro del modelo, mientras que la ponderación mediante la longitud de las tuberías proporciona información adicional que puede ser utilizada posteriormente por algoritmos de optimización y análisis de rutas.

---

## Organización de la Información

Durante la construcción del grafo, cada tipo de componente conserva todos los atributos definidos originalmente en el dataset.

### Nodos

Cada nodo almacena información como:

- Identificador.
- Nombre.
- Tipo.
- Sector.
- Manzana.
- Estado.
- Información de la vivienda (cuando corresponde).

### Aristas

Cada arista almacena:

- Identificador de la tubería.
- Nodo de origen.
- Nodo de destino.
- Longitud.
- Material.
- Diámetro.
- Clase de presión.
- Estado.
- Fecha de inspección.

Gracias a esta estructura, el grafo no solo representa la conectividad entre los componentes de la red, sino que también conserva información descriptiva que podrá utilizarse en futuras etapas del proyecto.

---
---

# Validación del Modelo

Una vez construido el grafo, la aplicación ejecuta una serie de verificaciones para garantizar que tanto el dataset como la estructura de la red sean consistentes. Estas validaciones permiten detectar errores antes de utilizar el modelo para realizar análisis posteriores.

El proceso de validación se desarrolla en dos etapas principales:

1. Validación del dataset.
2. Validación del grafo.

Cada una verifica aspectos diferentes de la información generada.

---

## validar_grafo.py

Este módulo concentra todas las comprobaciones necesarias para asegurar que la red fue construida correctamente.

Durante su ejecución se analizan tanto los archivos CSV como el grafo generado por NetworkX.

El objetivo principal es garantizar que la información almacenada sea coherente y que la estructura del grafo represente correctamente el diseño definido para la urbanización.

---

# Validaciones del Dataset

Antes de construir el grafo se verifica la consistencia de los archivos **nodos.csv** y **tuberias.csv**.

Entre las validaciones implementadas se encuentran:

| Validación | Descripción |
|------------|-------------|
| Existencia de columnas | Comprueba que todos los campos obligatorios estén presentes en los archivos CSV. |
| Cantidad de nodos | Verifica que existan exactamente 50 registros en nodos.csv. |
| Cantidad de tuberías | Comprueba que existan exactamente 49 conexiones. |
| Identificadores únicos | Evita la existencia de nodos o tuberías duplicadas. |
| Longitudes válidas | Verifica que todas las longitudes sean numéricas y mayores que cero. |
| Nodos existentes | Comprueba que todas las tuberías conecten nodos definidos en nodos.csv. |
| Relaciones válidas | Verifica que cada vivienda pertenezca a la válvula correspondiente a su manzana. |

Estas comprobaciones permiten detectar errores de digitación, registros incompletos o inconsistencias dentro del conjunto de datos.

---

# Validaciones del Grafo

Después de construir el grafo, el programa ejecuta una segunda fase de validaciones enfocadas en la estructura de la red.

Entre las verificaciones realizadas se encuentran:

| Validación | Propósito |
|------------|-----------|
| Número de nodos | Confirmar que el grafo contenga los 50 nodos esperados. |
| Número de aristas | Verificar que existan exactamente 49 conexiones. |
| Nodos aislados | Detectar componentes sin conexión dentro de la red. |
| Conectividad | Confirmar que toda la red pertenezca a un único componente conectado. |
| Grado de las viviendas | Verificar que cada vivienda tenga únicamente una conexión. |
| Aristas duplicadas | Evitar conexiones repetidas entre los mismos nodos. |
| Integridad estructural | Confirmar que la red conserve la topología definida durante el diseño. |

Estas validaciones garantizan que el modelo represente correctamente la red propuesta antes de generar la visualización final.

---

# visualizar_grafo.py

Una vez comprobada la consistencia del modelo, este módulo genera una representación gráfica de toda la red.

A diferencia de los algoritmos automáticos de distribución de nodos, la aplicación utiliza posiciones previamente definidas para conservar una distribución similar a la organización de la urbanización utilizada como referencia.

Cada tipo de componente se representa mediante un color diferente para facilitar la interpretación del modelo.

| Componente | Representación |
|------------|----------------|
| Red Pública | Nodo inicial de la red |
| Bombeos | Estaciones de distribución |
| Válvulas | División por sectores |
| Viviendas | Puntos finales de consumo |

Las conexiones representan las tuberías que unen todos los componentes del sistema.

Finalmente, la figura es exportada automáticamente mediante Matplotlib.

```python
plt.savefig("imagenes/grafo_red.png")
```

La imagen obtenida constituye la representación computacional del modelo desarrollado durante el proyecto.

---

# main.py

El archivo **main.py** funciona como punto de entrada de toda la aplicación.

Su responsabilidad consiste en coordinar la ejecución de todos los módulos en el orden correcto.

El flujo general ejecutado por este archivo es el siguiente:

```text
1. Leer configuración de la red
            │
            ▼
2. Generar el dataset
            │
            ▼
3. Crear los archivos CSV
            │
            ▼
4. Construir el grafo
            │
            ▼
5. Ejecutar validaciones
            │
            ▼
6. Dibujar el grafo
            │
            ▼
7. Mostrar resultados
```

Gracias a esta organización, el usuario únicamente necesita ejecutar un solo archivo para generar automáticamente todo el proyecto.

```bash
python main.py
```

---

# Flujo Completo de Ejecución

El siguiente diagrama resume el funcionamiento general de toda la aplicación.

```text
               main.py
                   │
                   ▼
          configuracion_red.py
                   │
                   ▼
            generar_dataset.py
                   │
                   ▼
                nodos.csv
              tuberias.csv
                   │
                   ▼
             crear_grafo.py
                   │
                   ▼
             Grafo (NetworkX)
                   │
                   ▼
            validar_grafo.py
                   │
                   ▼
          visualizar_grafo.py
                   │
                   ▼
              grafo_red.png
```

Todo el proceso se ejecuta automáticamente, permitiendo obtener un dataset consistente, un grafo correctamente construido y una representación gráfica de la red a partir de una única ejecución del programa.

---
---

# Dataset Generado

La aplicación genera automáticamente dos archivos CSV que representan toda la información utilizada para construir el grafo de la red de distribución de agua.

Estos archivos constituyen la base del modelo computacional y permiten separar completamente los datos de la lógica de programación.

```text
datos/
│
├── nodos.csv
└── tuberias.csv
```

---

# nodos.csv

Este archivo almacena la información correspondiente a cada componente físico de la red.

Cada fila representa un nodo dentro del grafo.

Los nodos pueden corresponder a:

- Red pública.
- Estaciones de bombeo.
- Válvulas de sectorización.
- Viviendas.

## Campos principales

| Campo | Descripción |
|--------|-------------|
| id_nodo | Identificador único del nodo. |
| nombre | Nombre descriptivo del componente. |
| tipo | Tipo de nodo (Red Pública, Bombeo, Válvula o Casa). |
| sector | Sector de la urbanización al que pertenece. |
| manzana | Manzana correspondiente. |
| nombre_casa | Nombre asignado a la vivienda. |
| valvula_abastecedora | Válvula responsable del suministro. |
| propietario | Nombre ficticio del propietario. |
| numero_residentes | Cantidad estimada de habitantes. |
| consumo_estimado_m3_mes | Consumo mensual aproximado. |
| estado_acometida | Estado de la acometida domiciliaria. |
| estado_medidor | Estado del medidor de agua. |
| fecha_ultima_inspeccion | Fecha de la última inspección. |
| activo | Indica si el nodo se encuentra operativo. |

---

## Ejemplo de registros

```csv
RP,Conexión a la red pública,RedPublica
B1,Estación de bombeo principal,Bombeo
V1,Válvula de sectorización,Valvula
C12,Vivienda C12,Casa
```

---

# tuberias.csv

Este archivo contiene todas las conexiones existentes entre los nodos del modelo.

Cada registro representa una tubería y posteriormente se convierte en una arista dentro del grafo.

## Campos principales

| Campo | Descripción |
|--------|-------------|
| id_tuberia | Identificador de la tubería. |
| nodo_origen | Nodo de origen. |
| nodo_destino | Nodo de destino. |
| sector | Sector correspondiente. |
| manzana | Manzana abastecida. |
| clase_tuberia | Tipo de tubería. |
| longitud_m | Longitud en metros. |
| diametro_mm | Diámetro principal. |
| diametro_acometida_mm | Diámetro de la acometida. |
| material | Material principal. |
| material_acometida | Material de la acometida. |
| clase_presion | Clasificación de presión. |
| profundidad_instalacion_m | Profundidad de instalación. |
| estado | Estado operativo. |
| fecha_ultima_inspeccion | Última inspección realizada. |

La longitud de cada tubería es utilizada como **peso de la arista** dentro del grafo.

---

# Representación del Modelo

El proyecto fue inspirado en la distribución general de la urbanización **Ciudad Celeste – Etapa La Coralia**, ubicada en Samborondón.

La imagen satelital fue utilizada únicamente como referencia para definir la organización general de la red.

> Debido a que no existe acceso al plano hidráulico oficial, la red implementada corresponde a una simplificación académica diseñada exclusivamente con fines educativos.

## Urbanización utilizada como referencia

<p align="center">
<img src="capturas/ciudad_celeste.jpg" width="90%">
</p>

---

# Grafo Generado

A partir del dataset construido automáticamente, la aplicación genera una representación computacional mediante NetworkX.

Cada tipo de componente posee un color específico para facilitar su identificación.

| Color | Componente |
|--------|------------|
| 🟣 | Red Pública |
| 🔵 | Estaciones de Bombeo |
| 🟢 | Válvulas de Sectorización |
| ⚪ | Viviendas |

Las aristas representan las tuberías que conectan todos los elementos de la red.

## Grafo obtenido

<p align="center">
<img src="C:\Users\Usuario\Downloads\entrega_la_coralia_grafo_corregido\grafo_red_agua_coralia.png" width="95%">
</p>

La estructura obtenida representa una red compuesta por **50 nodos** y **49 conexiones**, organizadas jerárquicamente desde la red pública hasta las viviendas.

El modelo conserva la distribución general observada en la urbanización utilizada como referencia, aunque no corresponde a su infraestructura hidráulica oficial.

---

# Comparación del Modelo

La siguiente comparación muestra el origen del proyecto y su representación computacional.

| Urbanización de referencia | Grafo generado |
|----------------------------|----------------|
| <img src="C:\Users\Usuario\Downloads\Ciudadela-Ciudad Celeste.jpg" width="100%"> | <img src="capturas/grafo_red.png" width="100%"> |

La imagen de la izquierda corresponde a la referencia espacial utilizada durante el diseño del modelo.

La imagen de la derecha representa el grafo construido automáticamente por la aplicación utilizando teoría de grafos y la biblioteca NetworkX.

---
