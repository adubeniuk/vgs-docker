Trial task for DevOps opportunity 


Using docker, setup three instances that communicate to each other.

1. a docker instance running rsyslog (centralized logging server)
2. a docker instance running rsyslog which forwards to the centralized logging server (logging agent)
3. a docker instance running nginx serving static content (app server)

Ensure that the app server's access logs are forwarded to the centralized logging server via the logging agent.

The ideal solution here should be re-usable. In production we would want to run one logging agent and many app server instances together on any host. This would provide us with an easy way to ship logs for each container from each docker host to the centralized logging service.

A good solution will include the ability to easily configure the address of the centralized logging server (it could change so just re-configuring the logging agent should be easy). We should also be able to easily choose what files we want to ship to the logging service.

Your solution should be organised as repository on github with shell, Dockerfile-s and any other files as needed.

**Extra credit** - if we didn't use rsyslog how else could we ship these logs? Do you have experience with other logging systems that are more advanced such as fluentd?
