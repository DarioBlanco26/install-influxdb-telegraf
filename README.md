# **Instalación de InfluxDB y Telegraf**

Ver el token en la UI de InfluxDB http://ol-nocmon-idb01:8086

Para utilizar el InfluxQL en la version 2 se debe mapear el bucket a una base de datos y crear un usuario +  contraseña

Para obtener el "org-id", a la izquierda en el menú de navegación, desplegar el menu del usuario y seleccionar "About"
export INFLUX_ORG_ID=org-id

En la izquierda en el menú de navegación, seleccionar Load Data > Tokens.
```
export INFLUX_TOKEN=bucket-token
```

Crear la base de datos "prod" con politíca de retencion de 365 días. Para obtener el "bucket-id", a la izquierda en el menú de navegación, seleccionar Load Data > Buckets
```
# influx v1 dbrp list 
# influx v1 dbrp create --db prod --rp 365d --bucket-id bucket-id --default
# influx v1 dbrp list 
ID                      Database        Bucket ID               Retention Policy        Default Organization ID
db-id                   prod            bucket-id               365d                    true    org-id
```

Crear el usuario "noc" con permisos de lectura a la base de datos "prod"
```
# influx v1 auth create --read-bucket bucket-id --username noc
# influx v1 auth list --id id
ID                      Description     Name / Token    User Name       User ID                 Permissions
id                                      noc             admin           user-id                 [read:orgs/org-id/buckets/bucket-id]
```

Para configurar el datasource en grafana realizar los pasos según la documentacion https://docs.influxdata.com/influxdb/v2.0/tools/grafana/ 

