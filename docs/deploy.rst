################################
Deploy.
################################

This explains the logic regarding the differents tasks used for deployment of the Ductilis application.

*****************************************
Environments
*****************************************

Two differents environments are set-up:

* **development** this environment is used on a virtual webserver
* **vagrant** this environment is used on a container

*****************************************
Confidential informations
*****************************************

All confidential informations are in the **env_vars** folder.

*****************************************
Main tasks
*****************************************

==============================
dbservers
==============================

The **dbservers.yml** file is used to configure the database servers.
In most of the cases the database server is the same as the web server.
This ansible script will install Posgres and create a user

The list of servers is indicated in the **inventory** file under the **[dbservers]** indication


to launch the script use
::
    ansible-playbook -i inventory dbservers.yml

==============================
webservers
==============================

The **webservers.yml** file is used to configure a web server

This script will run the following roles:

* **rabbitmq** used by the task handler celery
* **yarn** used to manage the frontend
* **web** used to install the application (backend and frontend)
* **celery** used to configure the task manager, including a supervisor script to managed in background the service
* **nginx** used to fire the webserver

to launch the script use
::
    ansible-playbook -i inventory webservers.yml --tags "deploy"


==============================
file structure
==============================

the **virtualenv_path** is /webapps/ductilis
the **project_path** is /webapps/ductilis/ductilis


files are positionnedd on the server as follow:

| /webapps
|     /ductilis
|         /bin
|         /ductilis
|         /include
|         /lib
|         /scripts
|         /share
|         /vars