```mermaid
graph TD
    A[API Gateway] -->|Invoke via API| B[Lambda 1: Scraping]
    C[Cron Trigger] -->|Invoke on schedule| B
    B -->|Download files| D[S3 Bucket]
    D -->|Trigger on new object| E[Lambda 2: Data Processing]
    E -->|Save processed data| F[(Database)]
    B -->|Scrape web page| G[Web Page]
````


----------------------------

Este diagrama describe lo siguiente:

1. **Lambda 1**: Se puede ejecutar tanto por un **API Gateway** (llamado manualmente desde una API) como por un **Cron Trigger** (programado).
2. **Lambda 1**: Realiza web scraping y descarga dos archivos desde una página web.
3. Los archivos descargados se guardan en un bucket de **Amazon S3**.
4. Al crearse nuevos objetos en el bucket de **S3**, se gatilla la ejecución de **Lambda 2**.
5. **Lambda 2**: Procesa los datos de los archivos y los guarda en una base de datos.
