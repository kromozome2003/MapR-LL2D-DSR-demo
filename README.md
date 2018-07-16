# MapR-LL2D-DSR-demo
This repository contains all required resources in order to reproduce the MapR DSR (Data Science Refinery) demo shown during the #LL2D webinar (16th of July, 2018)

## You will find the following resources
* a Dataset folder that contain csv files to import in Hive
* A Zeppelin notebook in JSON format to import into your DSR : LL2D DSR Zeppelin Notebook.json

## Prerequisites
* [MapR SandBox image (VMware/VirtualBox)](https://mapr.com/products/mapr-sandbox-hadoop/download-sandbox-drill/)
* [VirtualBox for Mac](https://download.virtualbox.org/virtualbox/5.2.8/VirtualBox-5.2.8-121009-OSX.dmg)
* [Docker for Mac](https://www.docker.com/community-edition)

## Useful links
* [Running Zeppelin on MapR](https://maprdocs.mapr.com/home/Zeppelin/Zeppelin.html)
* [MapR DSR mini-site](https://maprdocs.mapr.com/home/DataScienceRefinery/DataScienceRefineryOverview.html)
* [Converge Community / DSR](https://community.mapr.com/community/products/mapr-converged-platform/data-refinery)

## Assumption
* VirtualBox is installed
* MapR Sandbox imported into VirtualBox and running
* Docker is installed and running
* You created a MapR volume (via MCS or maprcli) named dsr mounted on /demos/dsr

## Retrieving the Datasets into MapR Sandbox
I highly recommend to change the VirtualBox's MapR Sandbox network as follow :
* Host-Only adapter

Then on your laptop retrieve the Github project including the datasets
```
cd ~
git clone https://github.com/kromozome2003/MapR-LL2D-DSR-demo.git
cp -Rf Datasets/* /mapr/demo.mapr.com/demos/dsr
ls -l /mapr/demo.mapr.com/demos/dsr
```

## Running the DSR and binding to localhost:9995
```
docker run -it -p 9995:9995 -e HOST_IP=localhost -p 20000-20010:20000-20010 -e MAPR_CLUSTER=demo.mapr.com -e MAPR_CLDB_HOSTS=192.168.56.101 -e MAPR_CONTAINER_USER=mapr -e MAPR_CONTAINER_PASSWORD=mapr -e MAPR_CONTAINER_GROUP=mapr -e MAPR_CONTAINER_UID=5000 -e MAPR_CONTAINER_GID=5000  -e MAPR_MOUNT_PATH=/mapr --cap-add SYS_ADMIN --cap-add SYS_RESOURCE --device /dev/fuse -e ZEPPELIN_NOTEBOOK_DIR=/mapr/demo.mapr.com/notebook -e MAPR_TZ=US/Pacific maprtech/data-science-refinery:v1.2_6.0.1_5.0.0_centos7
```
### Go to Zeppeling homepage
http://localhost:9995
![](/Images/1-zep-homepage.png)

### Login to Zeppeling with MapR credentials
According to the docker run command you will log as mapr/mapr
![](/Images/2-zep-login.png)

### Then the first thing to do is to update the interpreters
Clic on top right button and choose "Interpreter"
![](/Images/3-zep-interpreter.png)

### Update Hive interpreter
Set the Hive server to your MapR Sandbox ip address (localhost by default)
To update clic the "edit" button on top right, then "save" when done
![](/Images/4-zep-update-hive.png)

### Update Drill interpreter (if needed)
If you need Drill set it as well.
You can set any other Interpreter according to your needs
To update clic the "edit" button on top right, then "save" when done
![](/Images/5-zep-update-drill.png)

### Import the DSR demo Notebook
This is the notebook I presented during the LL2D (16th of July, 2018)
![](/Images/6-zep-import-notebook.png)

### Browse to your home directory where your "cloned" this repo
![](/Images/7-zep-browse-notebook.png)

### Choose the json document to import
![](/Images/8-zep-choose-notebook.png)

### Clic open to import it
![](/Images/9-zep-open-notebook.png)

### Have fun with your first notebook
![](/Images/10-zep-run-notebook.png)

You are now ready to play with Zeppelin
