# graylog-docker

## Install

### Install Docker

```shell
sudo curl -sSL https://get.docker.com/ | sh
sudo curl -L https://github.com/docker/compose/releases/download/1.25.4/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
docker-compose --version
```

中国版安装

```shell
sudo curl -sSL https://get.daocloud.io/docker | sh
sudo curl -sSL https://get.daocloud.io/daotools/set_mirror.sh | sh -s http://d52bcda9.m.daocloud.io
sudo curl -L https://get.daocloud.io/docker/compose/releases/download/1.25.4/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
docker-compose --version
```

换中国源

```shell
vim /etc/docker/daemon.json
```

添加代码：

```json
{
    "registry-mirrors": [
        "https://dockerhub.azk8s.cn",
        "https://docker.mirrors.ustc.edu.cn"
    ]
}
```

重启服务

```
sudo systemctl daemon-reload && sudo systemctl restart docker
```

### Clone Code

```shell
git clone https://github.com/forecho/graylog-docker.git
cd graylog-docker 
```


### Config env

```shell
cp .env.example .env
```

change config

- **`GRAYLOG_PASSWORD_SECRET`**: This field is used to encrypt Graylog passwords. Must be at least 16 characters.
- **`GRAYLOG_ROOT_PASSWORD_SHA2`**: This is a SHA2 hash of the password for the admin user (above, the hash is for the password “admin”). You can generate your own password hash with the following command:

```shell
echo -n "Enter Password: " && head -1 </dev/stdin | tr -d '\n' | sha256sum | cut -d" " -f1
```
- **`GRAYLOG_HTTP_EXTERNAL_URI`**: The public URI of Graylog which will be used by the web interface to communicate with the Graylog REST API.

### Install Graylog

```shell
sudo docker-compose up -d
```

Finally access `GRAYLOG_HTTP_EXTERNAL_URI` through the browser, local default <http://127.0.0.1:9000/>

### About `graylog.conf`

I set Graylog’s retention strategy in its configuration file, so graylog retain log data for 30 days:

```
elasticsearch_max_time_per_index = 1d
elasticsearch_max_number_of_indices = 30
retention_strategy = delete
```

[How to config graylog data save days](https://www.digitalocean.com/community/questions/how-to-config-graylog-data-save-days)

## Test

```shell
echo '{"version": "1.1","host":"example.org","short_message":"A short message that helps you identify what is going on","full_message":"Backtrace here\n\nmore stuff","level":1,"_user_id":9001,"_some_info":"foo","_some_env_var":"bar"}' | gzip | nc -u -w 1 127.0.0.1 12201
```

## Link

- [How to Create a Graylog Container in Docker](https://hometechhacker.com/how-to-create-a-graylog-container-in-docker/)
- [Docker - Graylog 3.2.0 documentation](https://docs.graylog.org/en/3.2/pages/installation/docker.html)
- [镜像加速器](https://yeasy.gitbooks.io/docker_practice/install/mirror.html)