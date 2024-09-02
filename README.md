# Ingesta de Datos con Azure Data Factory

<br><img src="https://i.postimg.cc/85Q3GjPL/Ingesta-con-Azure-Data-Factory.png" alt="">

La ingesta de datos es una parte fundamental del flujo de trabajo en el manejo de datos modernos. En este artículo, exploraremos cómo utilizar Azure Data Factory para copiar datos de un Blob Storage a un Data Lake sin necesidad de realizar codificación. Este enfoque permite a los profesionales de datos simplificar sus procesos de ETL y enfocarse en tareas más estratégicas.

## Resumen del Ejercicio

En este ejercicio, nuestro objetivo es demostrar cómo Azure Data Factory puede facilitar la transferencia de datos de un Blob Storage a un Data Lake utilizando un pipeline de copia de datos. Utilizamos Azure Data Factory, una herramienta potente para la integración y transformación de datos, para configurar una solución sin código que gestiona la ingesta de datos de manera eficiente.

## 🛠️Recursos Utilizados

📌Azure Data Factory: Servicio de integración de datos en la nube que permite crear, programar y administrar pipelines de datos.
📌Blob Storage: Almacenamiento de objetos en la nube para almacenar grandes volúmenes de datos no estructurados.
📌Data Lake: Almacenamiento optimizado para grandes volúmenes de datos, diseñado para análisis de Big Data y procesamiento a gran escala.

## 🚀Pasos del Desarrollo

📌Creación del Grupo de Recursos
📌Configuración de Blob Storage
📌Configuración del Data Lake
📌Creación de Azure Data Factory
📌Configuración de Servicios Linkeados
📌Creación de Datasets
📌Desarrollo del Pipeline de Copia

## Desarrollo

1. Inicie el explorador web Microsoft Edge o Google Chrome.
2. Iniciar Sesión en Azure Portal
3. Dirígete a la sección Create a resource y dale clic
4. En el buscador escribe Resource group, una vez lo ubiques dale clic
5. Clic en Create
Para crear el Grupo de recursos, realice los siguientes pasos:
 Nombre grupo de recursos: rg-azuredatafactory
6. Clic en Review + create
7. Clic en Create
<br><img src="https://i.postimg.cc/J07p7JwH/2-Create-a-resource-group.png" alt="">

## Crear Blob Storage y Data Lake

1. Dirígete a la sección Create a resource y dale clic
2. En el buscador escribe Storage account, una vez lo ubiques dale clic
3. Clic en Create
Para crear el Blob Storage, realice los siguientes pasos:
 Resource group: Seleccione el grupo de recursos creado en el paso anterior rg- azuredatafactory
 Storage account name: covidbsjmdc01
 Region: (US) East US
 Performance: Standard
 Redundancy: Locally-redundant storage (LRS)
4. Clic en Review + create
5. Clic en Create
<br><img src="https://i.postimg.cc/TPdfmbv7/4-Create-a-storage-account.png" alt="">
6. Nos dirigimos al Storage browser y damos clic en Bloc containers.
7. Damos clic en Add container y le damos el nombre de population
8. Clic en Create
9. Clic en el contenedor creado y cargamos un .csv no dirigimos a la opçión Upload y cargamos un .csv que puedes descargarlo aquí
10. Seleccione en el Browse file la ruta donde se has descargado el covid_population.csv y das clic a Upload
<br><img src="https://i.postimg.cc/rsY3vgdw/8-upload-populations.png" alt="">
<br><img src="https://i.postimg.cc/Hkbv2Ttx/8-create-container-data-lake.png" alt="">

## Crear Data Lake

1. Dirígete a la sección Create a resource y dale clic
2. En el buscador escribe Storage account, una vez lo ubiques dale clic
3. Clic en Create 
 Para crear el Data Lake, realice los siguientes pasos:
 Resource group: Seleccione el grupo de recursos creado en el paso anterior rg- azuredatafactory
 Storage account name: coviddljmdc01
 Region: (US) East US
 Performance: Standard
 Redundancy: Locally-redundant storage (LRS)
4. En la pestaña Advanced habilitamos la opción Enable hierarchical namespace
4. Clic en Review + create
5. Clic en Create
<br><img src="https://i.postimg.cc/kGkwQH6K/5-Enable-hierarchical-namespace.png" alt="">
6. Nos dirigimos al Storage browser y damos clic en Bloc containers
7. Damos clic en Add container y le damos el nombre de raw
8. Clic en Create
<br><img src="https://i.postimg.cc/3xzXLwhG/6-Create-Data-Lake.png" alt="">

## Crear Azure Data FactoryCrear Azure Data Factory

1. Dirígete a la sección Create a resource y dale clic
2. En el buscador escribe Data Factory, una vez lo ubiques dale clic
3. Clic en Create
Para crear el Azure Data Factory, realice los siguientes pasos:
 Resource group: Seleccione el grupo de recursos creado en el paso anterior rg- azuredatafactory
 Name: azuredatafactoryjmdc
 Region: East US
 Version: V2
4. Clic en Review + create
5. Clic en Create
<br><img src="https://i.postimg.cc/QM2rxc3M/10-Create-Data-Factory.png" alt="">

## Crear servicios linkeados del Blob Storage en Data Factory

1. Dentro de nuestro Data Factory Studio nos dirigimos a Manage y seleccionamos la opción Linked services
2. Damos clic a New
3. En el buscador escribimos Blob Storage
4. Clic en continue
Para crear el servicio linkeado, realice los siguientes pasos:
 Name: ls_blob_covidbs
 Connect via integration runtime: AutoResolveIntegrationRuntime
 Authentication type: Account key
 Account selection method: From Azure subscription
 Azure subscription: Seleccionamos nuestra cuenta de suscripción
 Storage account name: ovidbsjmdc01
5. Clic en test conection, si todo esta ok
6. Clic en Create
<br><img src="https://i.postimg.cc/ryhQ1MD1/12-Create-linked-services-blob.png" alt="">

## Crear servicios linkeados del Data Lake en Data Factory

1.  Dentro de nuestro Data Factory Studio nos dirigimos a Manage y seleccionamos la opción Linked services
2. Damos clic a New
3. En el buscador escribimos Data Lake
4. Clic en continue
<br><img src="https://i.postimg.cc/P5Hyhx9k/13-linked-services-data-lake.png" alt="">
Para crear el servicio linkeado, realice los siguientes pasos:
 Name: ls_dl_coviddl
 Connect via integration runtime: AutoResolveIntegrationRuntime
 Authentication type: Account key
 Account selection method: From Azure subscription
 Azure subscription: Seleccionamos nuestra cuenta de suscripción
 Storage account name: coviddljmdc01
5. Clic en test conection, si todo esta ok
6. Clic en Create
<br><img src="https://i.postimg.cc/Y9BqD5j8/14-Create-linked-services-data-lake.png" alt="">
<br><img src="https://i.postimg.cc/02jxnkcP/15-lista-de-ls.png" alt="">

## Crear dataset que apunta al Blob Storage en Data Factory

1.  Dentro de nuestro Data Factory Studio nos dirigimos a Author y seleccionamos la opción Datasets
2. Damos clic a New dataset 
3. En el buscador escribimos Blob Storage clic en CSV
Colocamos los siguientes datos:
 Name:ds_covid_population_raw_bs
 Linked service: ls_blob_covidbs
 File path: Seleccionamos el browse , seleccionamos nuestro archivo covid_population.csv 
4. Clic en ok
<br><img src="https://i.postimg.cc/MTHt4F4M/16-create-dataset-blob.png" alt="">

<br><img src="https://i.postimg.cc/c4y2gd2F/18-create-dataset-blob-3.png" alt="">

## Crear dataset que apunta al Data Lake en Data Factory
1.  Dentro de nuestro Data Factory Studio nos dirigimos a Author y seleccionamos la opción Datasets
2. Damos clic a New dataset 
3. En el buscador escribimos Data Lake clic continue y seleccionamos CSV, clic en continue
Colocamos los siguientes datos:
 Name:dl_covid_population_raw_bl
 Linked service: ls_dl_coviddl
 File path: Seleccionamos el browse , seleccionamos nuestro contenedor raw 
4. Clic en ok
<br><img src="https://i.postimg.cc/85dWZBkJ/19-create-dataset-data-lake.png" alt="">
5. colocamos en el file name el nombre del archivo: covid_population,csv
6. Clic al botón Validate all
<br><img src="https://i.postimg.cc/2jhmX9fX/20-validate-all.png" alt="">
7. Clic en Publish all
8. Clic en Publish
<br><img src="https://i.postimg.cc/J7cvkf8m/21-lista-de-linked-services.png" alt="">

## Crear pipeline y activity en Data Factory

1.  Dentro de nuestro Data Factory Studio nos dirigimos a Author y seleccionamos la opción pipeline
2. Damos clic a New pipeline
3. Asignamos un nombre: pl_ingestion_covid_population
4. Arrastramos y soltamos la actividad Copy Data
<br><img src="https://i.postimg.cc/P5kCRvc1/22-activity-Copy-Data.png" alt="">
5. En la opción source seleccionamos el dataset ds_covid_population_raw_bs
<br><img src="https://i.postimg.cc/5trF94p3/23-Source-Dataset.png" alt="">
6. En la opción Sink seleccionamos el dataset dl_covid_population_raw_bl
<br><img src="https://i.postimg.cc/8z55F87n/24-Sink-Dataset.png" alt="">
7. En la opción Mapping damos clic a import schemas
<br><img src="https://i.postimg.cc/CM7SbPpy/25-import-schemas.png" alt="">
8. Clic en Debug para validar que funcione correctamente.
<br><img src="https://i.postimg.cc/rpZY8rvP/26-Debug.png" alt="">
<br><img src="https://i.postimg.cc/rsXjmCgQ/27-Publish-all.png" alt="">
10. Revisamos el Data Lake para verificar que el pipeline haya copiado los datos correctamente, validamos como se ha creado el archivo.
<br><img src="https://i.postimg.cc/FFV334K9/28-comprobacion-data-lake.png" alt="">
