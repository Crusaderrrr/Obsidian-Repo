- [x] Execa - switch to version 2.0.0^ *node*
- [x] flatted - switch to version 3.4.2 *node*
- [x] node-forge - switch to version 1.4.0 *node*
- [x] @isaacs/brace-expansion - version 5.0.1 *node*
- [ ] spring-web - can be fixed, but only with swapping to Spring Boot version 3.x (drastic change, too many tests needed, does not worth it)
- [ ] linux-image-aws - linux kernel vulnerability, can be fixed by Denis
- [x] immutable - version (3.8.3/4.3.7/5.1.5) *node*
- [x] lodash - version 4.18.0 *node*
- [x] undici - version 7.24.0  *node*
- [ ] apache/httpd - possibly fixed already
- [ ] linux-libc-dev - fix use-after-free in ipc_msg_send_request (Denis)

```properties
[###########################  
# APP CONFIGURATION  
###########################  
  
spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.PostgreSQLDialect  
spring.jpa.properties.hibernate.type.descriptor.sql=error  
  
# Links to the front end  
app.urls.baseUrl=http://localhost:8080  
app.urls.invite=http://localhost:8080/app/register/  
app.urls.password-recovery=http://localhost:8080/app/password-update/  
app.urls.login=http://localhost:8080/app/login/  
external.application.host=http://localhost:8080/api/v1/investors  
  
# this will appear as sender on the emails  
app.mail.sender=test@test.com  
  
# keyword to confirm database clearance  
app.database.clear.keyword=test-keyword  
  
# how many items will a user lock and when do they expire?  
app.gray-list.itemsPerUser=6  
app.gray-list.lockExpireMilliseconds=1800000  
  
# spreadsheet items  
app.maxExportSize.investors=50000  
app.maxExportSize.logs=50000  
  
app.license-key=test-license-key  
  
# see JWT token...  
security.token.expirationInSeconds=604800  
security.token.key=test-token-secret  
  
spring.http.multipart.maxFileSize=300Mb  
spring.http.multipart.maxRequestSize=300Mb  
  
executor.awaitTerminationSeconds=180  
  
threads.async-services.poolSize=5  
threads.async-controllers.poolSize=5  
spring.mvc.async.request-timeout=1800000  
threads.scheduler.poolSize=5  
  
###########################  
# PARALLELISM  
###########################  
threads.batch-processor.parallelism=1  
threads.system-reclassifications.parallelism=1  
threads.user-triggered-reclassifications.parallelism=1  
threads.batch-processor.algorithm-timeout-minutes=5  
  
###########################  
# SCHEDULING  
###########################  
emails.management.schedule=0 0 0 1 * ?  
emails.api.unavailable.schedule=0 0 0 1 * ?  
  
# batch  
app.batch.cvs-to-database-chunk-size=100  
  
###########################  
# GENERAL SERVER CONFIGURATION  
###########################  
jetty.threadPool.minThreads=5  
jetty.threadPool.maxThreads=200  
jetty.threadPool.idleTimeout=15000  
  
spring.main.banner-mode=off  
server.display-name=ClassificationServer  
spring.application.name=ClassificationServer  
  
server.jsp-servlet.registered=false  
server.session.persistent=false  
  
server.servlet.encoding.charset=UTF-8  
server.servlet.encoding.enabled=true  
server.servlet.encoding.force=true  
  
spring.jackson.serialization.indent_output=true  
  
###########################  
# DATASOURCES  
###########################  
jdbc.datasource.update.backup.name=backup.backup  
jdbc.datasource.update.table.name=d8aforce_data_update  
  
database.temp.name=d8aforce_data_update  
database.backup.name=d8aforce_data_update.backup  
database.server.name=d8aforce_data  
  
update.email.link=https://d8aforce.demohoster.com/admin/settings  
  
jdbc.datasource.restore.location=/usr/lib/postgresql/9.5/bin/pg_restore  
jdbc.datasource.dropdb.location=/usr/lib/postgresql/9.5/bin/dropdb  
jdbc.datasource.backup.location=/home  
  
jdbc.driverClassName=org.postgresql.Driver  
jdbc.apache.initialPoolSize=1  
jdbc.apache.maxActiveConnections=5  
  
database.pgpass.path=/root/.pgpass  
  
###########################  
# AMAZON SES  
###########################  
aws.socketTimeout=50000  
aws.maxErrorRetry=3  
aws.maxConnections=50  
aws.connectionTimeout=8000  
  
###########################  
# REVERSE ADDRESS  
###########################  
reverse.address.api.link=https://api.ekata.com/3.0/location  
reverse.address.api.key=test-key  
  
us-streets.api.link=https://us-street.api.smartystreets.com/street-address  
us-streets.api.auth-id=test-auth-id  
us-streets.api.auth-token=test-auth-token  
  
postgrid.api.url=https://api.postgrid.com/v1/addver/  
postgrid.api.key=test-postgrid-key](<###########################
# APP CONFIGURATION
###########################

spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.PostgreSQLDialect
spring.jpa.properties.hibernate.type.descriptor.sql=error


# Links to the front end
app.urls.baseUrl=http://localhost:8080
app.urls.invite=http://localhost:8080/app/register/
app.urls.password-recovery=http://localhost:8080/app/password-update/
app.urls.login=http://localhost:8080/app/login/

# this will appear as sender on the emails
app.mail.sender=avinaash@d8aforce.com

# keyword to confirm database clearance
app.database.clear.keyword=keyword

# how many items will a user lock and when do they expire?
app.gray-list.itemsPerUser=6
app.gray-list.lockExpireMilliseconds=1800000

# spreadsheet items
app.maxExportSize.investors=50000
app.maxExportSize.logs=50000

# "Need not make this super secure as clients are trusted"
app.license-key=SECRET

# see JWT token...
security.token.expirationInSeconds=604800

spring.http.multipart.max-file-size=300Mb
spring.http.multipart.max-request-size=300Mb

executor.awaitTerminationSeconds=180

# async services are mainly emails...how many threads to attend that?
threads.async-services.poolSize=5

# how many users are going to be dumping a csv file concurrently?
threads.async-controllers.poolSize=5
spring.mvc.async.request-timeout=1800000

threads.scheduler.poolSize=5

###########################
# IMPORTANT SECTION: CONFIGURE HERE THE PALLELISM OF THE ALGORITHM ACCORDING TO YOUR MACHINE RESOURCES
###########################

#how many batch records do you want to process in parallel from the batches?
threads.batch-processor.parallelism=1

# how many system reclassifications (classifications after X months) do you want to process in parallel?
threads.system-reclassifications.parallelism=1

# how many user triggered classifications do you want to process in parallel?
threads.user-triggered-reclassifications.parallelism=1

# how much am i willing to wait for the algorithm to finish?
threads.batch-processor.algorithm-timeout-minutes=5

###########################
# END OF IMPORTANT SECTION
###########################

# general emails scheduling (every month at the beginning of the month)
emails.management.schedule=0 0 0 1 * ?
#every minute just to test:
#emails.management.schedule=0 * * * * *

# batch
app.batch.cvs-to-database-chunk-size=100

###########################
# GENERAL SERVER CONFIGURATION
###########################
jetty.threadPool.minThreads=5
jetty.threadPool.maxThreads=200
jetty.threadPool.idleTimeout=15000

spring.main.banner-mode=off
server.display-name=ClassificationServer
spring.application.name=ClassificationServer

server.jsp-servlet.registered=false
server.session.persistent=false

server.servlet.encoding.charset=UTF-8
server.servlet.encoding.enabled=true
server.servlet.encoding.force=true

spring.jackson.serialization.indent_output=true

###########################
# DATASOURCES
###########################
jdbc.datasource.update.backup.name=backup.backup
jdbc.datasource.update.table.name=d8aforce_data_update

database.temp.name=d8aforce_data_update
# d8aforce_data_update.backupg.restore.locationp for prd
database.backup.name=d8aforce_data_update.backup
database.server.name=d8aforce_data

update.email.link=https://d8aforce.demohoster.com/admin/settings

jdbc.datasource.restore.location=/usr/lib/postgresql/9.5/bin/pg_restore
jdbc.datasource.dropdb.location=/usr/lib/postgresql/9.5/bin/dropdb
jdbc.datasource.backup.location=/home

jdbc.driverClassName=org.postgresql.Driver
jdbc.apache.initialPoolSize=1
jdbc.apache.maxActiveConnections=5

database.pgpass.path=/root/.pgpass

###########################
# AMAZON SES
###########################
# AWS DEFAULT = 50000
aws.socketTimeout=50000
# AWS DEFAULT = 3
aws.maxErrorRetry=3
# AWS DEFAULT = 50
aws.maxConnections=50
aws.connectionTimeout=8000

############################
#reverse address
############################

reverse.address.api.link=https://api.ekata.com/3.0/location
reverse.address.api.key=54053622dc404994bdef7dad7bd54b03

us-streets.api.link=https://us-street.api.smartystreets.com/street-address
us-streets.api.auth-id=915f188a-96df-2e94-f11e-75561f07b5c4
us-streets.api.auth-token=2I37qivVv33zgxJmEJgI

security.token.key=My_Dirty_Token_Secret
postgrid.api.url=https://api.postgrid.com/v1/addver/
postgrid.api.key=test_sk_dBVVAaJ7NH9vN1knVeKhWW

external.application.host=http://localhost:8080/api/v1/investors
emails.api.unavailable.schedule=0 0 0 1 * ?>)
```