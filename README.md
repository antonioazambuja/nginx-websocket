# nginx-websocket
Example about Nginx Proxy Websocket.

This repository is only use case of websocket configuration on Nginx.


## Requirements

* [Docker Compose](https://docs.docker.com/compose/install/);
* [Docker](https://docs.docker.com/engine/);
* [wscat](https://github.com/websockets/wscat);

## Quick started

This repository have two Nginx configuration files:

* websocket;
* non websocket;

For use correct file choice **nginx/nginx-websocket.conf** on **docker-compose.yml**. For test and error case use **nginx/nginx.conf**.

```
version: "3.8"

services:
  nginx:
    ...
    volumes:
      - ./nginx/nginx-websocket.conf:/etc/nginx/nginx.conf:ro
```

For run this example execute commands below:

```
$ docker-compose build
$ docker-compose up
```

In new terminal, open connection with your nginx websocket:
```
$ wscat -c ws://localhost:8020/
> Send anything
```

### Logs wscat

```
wscat -c ws://localhost:8020/                                                                  
Connected (press CTRL+C to quit)
> Hello
< Server received from client: Hello
> 
```

### Logs Nginx Websocket

```
server  | Received from client: Hello
nginx   | [09/Jul/2023:23:20:54 +0000] - host="localhost" host_name="06d3012d3f22" dest_port="8020" dest_ip="192.168.224.3" dest_server="" src="192.168.224.1" remote_port="37074" src_ip="192.168.224.1" realip_remote_addr="192.168.224.1" realip_remote_port="37074" proxied_to="server" proxied_to_port="80" proxy_protocol_addr="-" time_local="09/Jul/2023:23:20:54 +0000" protocol="HTTP/1.1" status="101" bytes_out=36 bytes_in=0 http_user_agent="-" http_x_forwarded_for="-" http_true_client_ip="-" uri_path="/" http_referer="-" request="GET / HTTP/1.1" http_method="GET" upstream_response_time=61.979 upstream_addr="192.168.224.2:8010" request_time=61.979 connection_requests=1 connections_active=1 connections_reading=0 connections_waiting=0 connections_writing=0 body="-"
```