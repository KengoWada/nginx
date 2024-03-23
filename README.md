# Learning Nginx

Learning Nginx from [Very Academy Course](https://www.youtube.com/playlist?list=PLOLrQ9Pn6cawvMA5JjhzoQrnKbYGYQqx1)

**Note:** Assumes [Docker](https://docker.com/get-started/) and `Make` is installed.

## Lessons

### 02 - Nginx Architecture

- Change into `02. Architecture` directory

- Start the Nginx server

```sh
make buildup
```

- Go to [Nginx Index Page](http://localhost:8080) in your browser

- Start a shell on the `nginx` container

```sh
make shell
```

- Check for the nginx processes running

```sh
ps -C nginx -f
```

```sh
UID          PID    PPID  C STIME TTY          TIME CMD
root           1       0  0 10:12 ?        00:00:00 nginx: master process nginx -g daemon off;
nginx         29       1  0 10:12 ?        00:00:00 nginx: worker process
nginx         30       1  0 10:12 ?        00:00:00 nginx: worker process
nginx         31       1  0 10:12 ?        00:00:00 nginx: worker process
nginx         32       1  0 10:12 ?        00:00:00 nginx: worker process
```

- View the `nginx.conf` file details

```sh
cat /etc/nginx/nginx.conf
```

```sh
user  nginx;
worker_processes  auto;

error_log  /var/log/nginx/error.log notice;
pid        /var/run/nginx.pid;


events {
    worker_connections  1024; # Number of connections each worker process can handle in one second.
}


http {
    include       /etc/nginx/mime.types;
    default_type  application/octet-stream;

    log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
                      '$status $body_bytes_sent "$http_referer" '
                      '"$http_user_agent" "$http_x_forwarded_for"';

    access_log  /var/log/nginx/access.log  main;

    sendfile        on;
    #tcp_nopush     on;

    keepalive_timeout  65;

    #gzip  on;

    include /etc/nginx/conf.d/*.conf;
}
```

- Change the number of `worker_processes` to 2

  **Note:** When `worker_processes` is set to `auto`, it checks for the available CPU cores.

```sh
nano /etc/nginx/nginx.conf # Edit `worker_processes` to 2

nginx -s reload # Relaod Nginx without stopping the server

ps -C nginx -f # Check the number of worker processes
```
