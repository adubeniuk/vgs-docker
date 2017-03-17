#Quick Start

Assuming that the machine already has Docker installed

```
docker-compose build
docker-compose up -d
```

This will build the images and spin-up required containers:

```
Creating verygoodtask_log-server_1
Creating verygoodtask_nginx_1
Creating verygoodtask_log-agent_1
```

```
docker-compose ps
          Name                    Command          State          Ports         
-------------------------------------------------------------------------------
verygoodtask_log-agent_1    rsyslogd -n            Up      514/tcp, 514/udp     
verygoodtask_log-server_1   rsyslogd -n            Up      514/tcp, 514/udp     
verygoodtask_nginx_1        nginx -g daemon off;   Up      0.0.0.0:8080->80/tcp 
```

To verify the solution visit or curl [http://localhost:8080](http://localhost:8080)

Access logs will be forwarded to the centralized log server and stored there:

```
docker exec verygoodtask_log-server_1 cat /storage/nginx/access.log

2017-03-17T08:57:59+00:00 993b6c9db370 nginx-access: 172.18.0.1 - - [17/Mar/2017:08:57:52 +0000] "GET / HTTP/1.1" 304 0 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/56.0.2924.87 Safari/537.36" "-"
2017-03-17T08:57:59+00:00 993b6c9db370 nginx-access: 172.18.0.1 - - [17/Mar/2017:08:57:53 +0000] "GET / HTTP/1.1" 304 0 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/56.0.2924.87 Safari/537.36" "-"
2017-03-17T08:57:59+00:00 993b6c9db370 nginx-access: 172.18.0.1 - - [17/Mar/2017:08:57:54 +0000] "GET / HTTP/1.1" 304 0 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/56.0.2924.87 Safari/537.36" "-"
2017-03-17T09:02:29+00:00 993b6c9db370 nginx-access: 172.18.0.1 - - [17/Mar/2017:09:02:25 +0000] "GET / HTTP/1.1" 200 401 "-" "curl/7.49.1" "-"
2017-03-17T09:02:29+00:00 993b6c9db370 nginx-access: 172.18.0.1 - - [17/Mar/2017:09:02:28 +0000] "GET / HTTP/1.1" 200 401 "-" "curl/7.49.1" "-"
```


#Trial task for DevOps opportunity 


Using docker, setup three instances that communicate to each other.

1. a docker instance running rsyslog (centralized logging server)
2. a docker instance running rsyslog which forwards to the centralized logging server (logging agent)
3. a docker instance running nginx serving static content (app server)

Ensure that the app server's access logs are forwarded to the centralized logging server via the logging agent.

The ideal solution here should be re-usable. In production we would want to run one logging agent and many app server instances together on any host. This would provide us with an easy way to ship logs for each container from each docker host to the centralized logging service.

A good solution will include the ability to easily configure the address of the centralized logging server (it could change so just re-configuring the logging agent should be easy). We should also be able to easily choose what files we want to ship to the logging service.

Your solution should be organised as repository on github with shell, Dockerfile-s and any other files as needed.

**Extra credit** - if we didn't use rsyslog how else could we ship these logs? Do you have experience with other logging systems that are more advanced such as fluentd?
