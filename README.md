#**--ETL Pipeline: Binance Real-Time Data to Snowflake--**

Un pipeline End-to-End completamente automatizado que extrae información financiera de criptomonedas, la procesa y la disponibiliza en la nube para análisis

##**--Arquitectura--**

El flujo de datos sigue una arquitectura ETL:

1.**Extracción:** Conexión a la API pública de Binance para obtener datos de mercado en tiempo real ('ticker/24hr')
2.**Orquestación:** Apache Airflow gestiona y programa las tareas dentro de contenedores Docker
3.**Transformación:** Limpieza de datos, filtrado de monedas irrelevantes y conversión de tipos usando Pandas y PyArrow.
4.**Carga (Load):** Ingesta eficiente hacia Snowflake (Data Warehouse) utilizando conectores nativos.

##**--Tecnologías utilizadas--**

**Lenguaje:** Python 3.12
**Contenerización:** Docker & Docker Compose
**Orquestador:** Apache Airflow
**Data Warehouse:** Snowflake
**Librerías:** pandas, snowflake-connector-python, apache-airflow

##**--Estructura del Repositorio--**

```bash
├── dags/
│   ├── extraccion.py          # Lógica de conexión a Binance API
│   ├── transformacion.py      # Limpieza y estructuración de datos
│   ├── cargar_SnowFlake.py    # Conexión y carga a la nube
│   └── dag_cripto_etl.py      # Definición del DAG en Airflow
├── Dockerfile                 # Configuración de la imagen de Airflow
├── docker-compose.yaml        # Orquestación de servicios y redes
├── requirements.txt           # Dependencias de Python
└── README.md                  # Documentación del proyecto