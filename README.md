## OpenDock Template

The empty structure contains necessary folder and files to start building site based on project [opendocks/docks](https://github.com/opendocks/docks).

### How to use for project
- Clone [opendocks/template](https://github.com/opendocks/docks) i.e. [this](https://github.com/opendocks/docks) repository using command
```bash
    git clone git@github.com:opendocks/template.git
```
OR 
```bash
    git clone https://github.com/opendocks/template.git
```

- Clone [opendocks/docks](https://github.com/opendocks/docks) repository within root of this repo using command
```bash
    git clone git@github.com:opendocks/docks.git
```
OR 
```bash
    git clone https://github.com/opendocks/docks.git
```

### Create required directories
- Create code and data directories in root if not already exists
- Copy your code in code folder within the root directory or any sub directory

### Update general .env variables
   1. APP_BASE_DIR (See comments in file)
   2. Search {{PROJECT-IDENTIFIER}} & {{TLD}} and replace with names you preffer, 
      > NOTE It is suggested to use `ts` to replace `{{TLD}}` for local development
   3. PHP_VERSION (Use any value from 8.1, 8.0,7.3, 7.2, 7.1, 7.0, 5.6)
   4. DOCKER_HOST_IP (IP of host machine) `(optional)`
   5. PHP_IDE_CONFIG `(optional)`

### Setup nginx reverse proxy (if not already)
   - Clone this `opendocks/proxy` repository using command
   ```bash
      git clone git@github.com:opendocks/proxy.git
   ```
   OR 
   ```bash
      git clone https://github.com/opendocks/proxy.git
   ```
   - Create docker network using command
   ```bash
      docker network create net1-nginx-proxy
   ```
   - Run service
   ```bash
      docker-compose up
   ```
   - Above will setup nginx reverse proxy server, using IP 127.0.0.1 & default ports 80, 443 

### Update .env variables for Apache Service
   1. APACHE_VIRTUAL_HOST defined in .env file contains comma separated list of domains a& sub-domains, and is used by reverse proxy server service
   2. Reverse proxy service will read this value will setup reverse proxy for provided host names
   3. Update (Windows,linux,macOS) host file to add hostname entries used in APACHE_VIRTUAL_HOST pointing reverse proxy servic (server)
   4. Reverse proxy will automatically, sends all requests to desired container
      
### Update .env variables for PHP Service
   1. Enable or disable required PHP extentions for PHP service
   2. Enable or disable required PHP extentions for Workspace service

### Update .env for MySQL Service
   1. MYSQL_VERSION
   2. MYSQL_DATABASE
   3. MYSQL_USER
   4. MYSQL_PASSWORD
   5. MYSQL_ROOT_PASSWORD  

### Update conf/sites/appache/apache.conf
- Check comment in file `conf/sites/appache/apache.conf`


### Useful Commands

Docker compose useful commands
   
To build/start all services
```bash
docker-compose up
```
  
To build/start first time
```bash
docker-compose up apache php-fpm mysql
```

To build/rebuild explicitly
```bash
docker-compose up --build apache 
```

Close all running Containers
```bash
docker-compose stop
```

To stop single container do:
```bash
docker-compose stop {container-name}
```

To stop and remove all containers:
```bash
docker-compose down
```

To stop and remove single containers:
```bash
docker-compose down {container-name}
```

To enter container terminal window
```bash
docker exec -it {container-name} bash
```


### Workspace Commands
To Update all NPM packages in package.jon, (if npm-check-update is installed)
```bash
ncu -u
```