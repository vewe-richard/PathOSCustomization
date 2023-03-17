# PathOS Installation and Customization
## 1.Install docker
In an aws server:
```bigquery
sudo apt update && sudo apt install docker.io
```
else
```
curl -fsSL https://get.docker.com | bash
```

## 2.Install Compose V2
```
DOCKER_CONFIG=${DOCKER_CONFIG:-$HOME/.docker}
mkdir -p $DOCKER_CONFIG/cli-plugins
curl -SL https://github.com/docker/compose/releases/download/v2.2.3/docker-compose-linux-x86_64 -o $DOCKER_CONFIG/cli-plugins/docker-compose
chmod +x $DOCKER_CONFIG/cli-plugins/docker-compose
```

## 3.Start PathOs
```
git clone https://github.com/PapenfussLab/PathOS.git
# Navigate to the Docker/database directory
#
cd PathOS/Docker/database

## Run the PathOS docker containers in the background
#
sudo docker compose up -d

# Load the sample data into pathos. Skip this step if you don't want example data.
# you should wait for the command to complete before proceeding to use PathOS.
# since data persists between sessions, this only needs to be run once.
#
sudo docker compose run -v $PWD/load_dir/:/pathos-loader-input.d loader
```

PathOS will then be available on `http://localhost:8080/PathOS`.   
You can log in with the default username `pathosadmin` and password `pathos`.  
You can stop the running image by executing `docker compose down`.  
Data will be saved between sessions, persisting on the local file system in the PathOS/Docker/database/pathos-db-data directory.
```
# Stop the PathOS docker containers
# 
sudo docker compose down
```
