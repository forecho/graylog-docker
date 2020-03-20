# graylog-docker

## Install

### Install Docker

```shell
sudo curl -L https://github.com/docker/compose/releases/download/1.25.4/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
docker-compose --version
```

国内版安装

```shell
sudo curl -sSL https://get.daocloud.io/daotools/set_mirror.sh | sh -s http://d52bcda9.m.daocloud.io
sudo curl -L https://get.daocloud.io/docker/compose/releases/download/1.25.4/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
docker-compose --version
```


### Clone Code

```shell
git clone https://github.com/forecho/graylog-docker.git
cd graylog-docker 
```


### Change `docker-compose.yml`

- **`GRAYLOG_PASSWORD_SECRET`**: This field is used to encrypt Graylog passwords. Must be at least 16 characters.
- **`GRAYLOG_ROOT_PASSWORD_SHA2`**: This is a SHA2 hash of the password for the admin user (above, the hash is for the password “admin”). You can generate your own password hash with the following command:

```
echo -n "Enter Password: " && head -1 </dev/stdin | tr -d '\n' | sha256sum | cut -d" " -f1
```
- **`GRAYLOG_HTTP_EXTERNAL_URI`**: The public URI of Graylog which will be used by the web interface to communicate with the Graylog REST API.

### Install Graylog

```shell
sudo docker-compose up -d
```

Finally access `GRAYLOG_HTTP_EXTERNAL_URI` through the browser, local default <http://127.0.0.1:9000/>




## Link

- [How to Create a Graylog Container in Docker](https://hometechhacker.com/how-to-create-a-graylog-container-in-docker/)
- [Docker - Graylog 3.2.0 documentation](https://docs.graylog.org/en/3.2/pages/installation/docker.html)