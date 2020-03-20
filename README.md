# graylog-docker

## Install

### Install Docker

```shell
sudo curl -sSL https://get.docker.com/ | sh
sudo curl -L https://github.com/docker/compose/releases/download/1.25.4/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
docker-compose --version
```

国内版安装

```shell
sudo curl -sSL https://get.daocloud.io/docker | sh
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


### Change env

- **`GRAYLOG_PASSWORD_SECRET`**: This field is used to encrypt Graylog passwords. Must be at least 16 characters.
- **`GRAYLOG_ROOT_PASSWORD_SHA2`**: This is a SHA2 hash of the password for the admin user (above, the hash is for the password “admin”). You can generate your own password hash with the following command:

```
echo -n "Enter Password: " && head -1 </dev/stdin | tr -d '\n' | sha256sum | cut -d" " -f1
```
- **`GRAYLOG_HTTP_EXTERNAL_URI`**: The public URI of Graylog which will be used by the web interface to communicate with the Graylog REST API.
- `GRAYLOG_TRANSPORT` options (Optional): These options specify the settings for the mail relay Graylog will use for sending notifications. You need to set these options appropriately if you want your Graylog instance to be able to email you with alerts and notifications.
- `GRAYLOG_HTTP_BIND_ADDRESS`(Optional): This specifies the network interface used by the Graylog web frontend. If you only have on network interface it is recommended you use 0.0.0.0. Whatever port you specify here must also be in the “ports:” section.
- `GRAYLOG_ROOT_USERNAME`(Optional): Defalut admin


### Install Graylog

```shell
sudo docker-compose up -d
```





Finally access `GRAYLOG_HTTP_EXTERNAL_URI` through the browser.




## Link

- [How to Create a Graylog Container in Docker](https://hometechhacker.com/how-to-create-a-graylog-container-in-docker/)