#[EyeTech QRDevops ](#section)

Clone the project using the parameter --recursive as an exemple

````
git clone --recursive git@github.com:eyetech-ia/qrdevops.git
````
To update submodules
````
git submodule foreach git pull origin master
````

To make life easier, use git alias. Run this command from main/root project
````
git config alias.update 'submodule foreach git pull origin master'
````
After this command is executed, you can update your submodules by typing only

````
git update
````
````
Copy the file [Devops/config/magento/env.php] to [app_magento/app/etc/env.php], to have local or remote bank
````

#### Integrador <=> Magento2 GM_Core-GrupoMateus

Make sure there are no service sessions running on the localhost server ports.

````
80:nginx/canto-do-chefe
8001:nginx/integrator
8181:nginx/PhpMyAdmin
9200:elasticsearch
9300:elasticsearch
6379:Redis
3306:MySQL / Local
````

####Install Canto do Chefe in GrupoMateus

Launch application container
````
docker-compose -f docker-compose-dev.yml up --build
````
ou
````
./start --build
````
Para startar o sistema, use:
````
./start
````

Access the container Canto do Chefe
````
docker exec -it app_magento bash
````
and inside it execute
 ````
composer install
 ````
and then
 ````
bin/magento module:enable --all
 ````
Install execute
 ````
bin/magento ithappens:install 
 ````

````
Copy the file [Devops/config/magento/1574190262_db_initDev.sql] to [app_magento/var/backup/1574190262_db_initDev.sql], to have local or remote bank
````

Create host on file by running this /etc/hosts (linux)
 ````
 sudo echo "127.0.0.1 local.grupomateus.com.br" | sudo tee -a /etc/hosts
 ````
 
Access [local.grupomateus.com.br](local.grupomateus.com.br)

###Data Bases

Modify the file [app/etc/env.php], to have local or remote bank
 
 #####Local Data Base
 ````
 'db' => [
         'table_prefix' => '',
         'connection' => [
             'default' => [
                 'host' => 'db_magento',
                 'dbname' => 'magento',
                 'username' => 'magento',
                 'password' => 'magento',
                 'active' => '1'
             ]
         ]
     ],
 ````

###Install with local data base

For this type of installation, follow the step by step instructions. Any questions, contact the Ecommerce Team

To continue instalation of the project canto-do-chefe, access container and run this commands
````
chmod +x bin/magento

bin/magento module:enable --all

bin/magento  app:config:import

bin/magento deploy:mode:set developer

bin/magento setup:db-schema:upgrade

bin/magento config:set  dev/static/sign 0

bin/magento setup:install --use-rewrites=1

bin/magento setup:static-content:deploy -f
````
Make URL of the project
````
bin/magento setup:install \
 --base-url=http://local.grupomateus.com.br/ \
 --base-url-secure=https://local.grupomateus.com.br/
````
Make administrator user
````
bin/magento admin:user:create \
 --admin-user='admin' \
 --admin-password='admin123' \
 --admin-email='GmCore@GmCore.com' \
 --admin-firstname='GmCore' \
 --admin-lastname='GmCore' 
````


````
bin/magento setup:upgrade
bin/magento setup:di:compile
````
##Install Integrator in GrupoMateus
Access the container Integrator
````
docker exec -it app_integrator /bin/bash
````
and inside it execute
 ````
composer install
 ````
Access integrator [ http://localhost:8001/]( http://localhost:8001/)


Teste return token

````
http://localhost:8001/token
````

####Access o PHP_MyAdmin
Access [ http://localhost:8181/]( http://localhost:8181/)

````
http://localhost:8181/
````
Access data
  ````
'host' => 'db_magento',
'dbname' => 'magento',
'username' => 'magento',
'password' => 'magento',
````