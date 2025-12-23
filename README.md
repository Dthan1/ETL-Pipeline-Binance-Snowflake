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
```
##**--Resultados--**
##1.**Orquestación del flujo**
Se observa el grafo de dependencias en Airflow. El proceso inicia y se bifurca en dos tareas paralelas: carga de reporte diario y precios actuales.

<img width="626" height="531" alt="image" src="https://github.com/user-attachments/assets/0d171cb6-643b-4604-b259-342fb3d7a0fe" />



##2.**Evidencia de ejecución**

Logs de ejecución exitosa donde se confirma la inserción de registros en la tabla `REPORTE_DIARIO` y `PRECIOS_ACTUALES`.
<img width="901" height="99" alt="image" src="https://github.com/user-attachments/assets/f7f24457-e8c9-433e-8907-43551ceccb97" />
<img width="1033" height="94" alt="image" src="https://github.com/user-attachments/assets/8afda2e6-e64b-4214-8adb-9ed566cd1877" />


##3.**Validación de datos en Snowflake**
Consulta final en la base de datos verificando que los datos se alojaron correctamente en la capa Bronze.
<img width="1670" height="910" alt="image" src="https://github.com/user-attachments/assets/a4adedbe-750b-44e3-82ff-6352488ce9b9" />
<img width="1430" height="756" alt="image" src="https://github.com/user-attachments/assets/3675d3d5-c068-490d-9212-f9eca29ec858" />




