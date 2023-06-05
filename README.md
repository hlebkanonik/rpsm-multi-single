# Report Portal storage migration
Report Portal storage migration from multiple buckets to single bucket for S3 and MinIO

# Parameters
## Image Parameters
|Name|Description|Value|
|-|-|-|
|`image.repository`|Image repository|`reportportal/complex-migrations`|
|`image.tag`|Image tag|`1.0.0`|
|`image.pullPolicy`|Image pull policy|`IfNotPresent`|
|`imagePullSecrets`|Specify docker-registry secret names as an array|`[]`|

## Common parameters
|Name|Description|Value|
|-|-|-|
|`nameOverride`|String to partially override rabbitmq.fullname template (will maintain the release name)|`""`|
|`fullnameOverride`|String to fully override rabbitmq.fullname template|`""`|

## Job.batch parameters
|Name|Description|Value|
|-|-|-|
|`podAnnotations`|Pod annotations. Evaluated as a template|`{}`|
|`podSecurityContext`|Security Context|`{}`|
|`securityContext`|Container Security Context|`{}`|
|`resources.limits`|The limits limits for container|`{}`|
|`resources.requests`|The resources limits for container|`{}`|
|`nodeSelector`|Node labels for pod assignment. Evaluated as a template|`{}`|
|`tolerations`|Tolerations for pod assignment. Evaluated as a template|`[]`|
|`affinity`|Pod affinity|`[]`|

## Container environments
|Name|Description|Value|
|-|-|-|
|`storage.type`|Switching between MinIO and S3 storages (parametes: `minio`, `s3`)|`minio`|
|`storage.removeAfterMigration`|Allow files to be deleted after migration|`true`|
|`storage.secretName`|Secret name for Job.batch with access and secret key to `storage.type`|`""`|
|`storage.accesskey`|Access key to `storage.type`. Required if `SecretName` is not specified|`""`|
|`storage.secretkey`|Secret key to `storage.type`. Required if `SecretName` is not specified|`""`|
|`storage.accesskeyName`|Key form K8s Secret for Access key (`.data.access-key`)|`access-key`|
|`storage.secretkeyName`|Key form K8s Secret for Secret key (`.data.secret-key`)|`secret-key`|
|`storage.minio.endpoint`|MinIO endpoint|`http://<minio-release-name>-minio.default.svc.cluster.local:9000`|
|`storage.s3.region`|Amazon S3 Region|`eu-west-3`|
|`storage.bucket.bucketPrefix`|Bucket prefix on FS|`prj-`|
|`storage.bucket.bucketForPlugins`|Bucket name for storing Plugins|`rp-bucket`|
|`storage.bucket.bucketSingleName`|A new single bucket to which the data will be migrated|`rp-storage`|
|`postgresql.SecretName`|Secret name for Job.batch with database passowrd||
|`postgresql.endpoint.address`|Database URL|`<postgresql-release-name>-postgresql.default.svc.cluster.local`|
|`postgresql.endpoint.port`|Database port|`5432`|
|`postgresql.endpoint.user`|Database user name|`rpuser`|
|`postgresql.endpoint.dbName`|Database name|`reportportal`|
|`postgresql.endpoint.password`|Database pasword. Required if `SecretName` is not specified|`""`|
|`postgresql.endpoint.connections`|Number of database connections|`""`|
