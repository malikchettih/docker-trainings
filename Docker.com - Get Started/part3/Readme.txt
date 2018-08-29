------------------------------------------------------------------
 Commands
------------------------------------------------------------------


docker stack ls                                            # List stacks or apps
docker stack deploy -c <composefile> <appname>  # Run the specified Compose file
docker service ls                 # List running services associated with an app
docker service ps <service>                  # List tasks associated with an app
docker inspect <task or container>                   # Inspect task or container
docker container ls -q                                      # List container IDs
docker stack rm <appname>                             # Tear down an application
docker swarm leave --force      # Take down a single node swarm from the manager

------------------------------------------------------------------
 Exemples
------------------------------------------------------------------


mchettih@ubuntu:~/Projects/docker-trainings/Docker.com - Get Started/part3$ docker swarm init
Swarm initialized: current node (tv0yysdc8vedy621m4a51xghw) is now a manager.

To add a worker to this swarm, run the following command:

    docker swarm join --token SWMTKN-1-164q57gvm0n7j1m3a9i94fp3tutljq0ia8et6vw34cqxapgrtg-4f8ojq4k5akmfxp3b4ko0q9g2 192.168.38.143:2377

To add a manager to this swarm, run 'docker swarm join-token manager' and follow the instructions.

------------------------------------------------------------------
mchettih@ubuntu:~/Projects/docker-trainings/Docker.com - Get Started/part3$ docker stack deploy -c docker-compose.yml getstartedlab
Creating network getstartedlab_webnet
Creating service getstartedlab_web

------------------------------------------------------------------
mchettih@ubuntu:~/Projects/docker-trainings/Docker.com - Get Started/part3$ docker service ls
ID                  NAME                MODE                REPLICAS            IMAGE                            PORTS
kvqlsrnd640l        getstartedlab_web   replicated          5/5                 malikchettih/get-started:part2   *:4000->80/tcp

------------------------------------------------------------------
mchettih@ubuntu:~/Projects/docker-trainings/Docker.com - Get Started/part3$ docker service ps getstartedlab_web
ID                  NAME                  IMAGE                            NODE                DESIRED STATE       CURRENT STATE                ERROR               PORTS
l8dal460to78        getstartedlab_web.1   malikchettih/get-started:part2   ubuntu              Running             Running about a minute ago
lu5csing6o66        getstartedlab_web.2   malikchettih/get-started:part2   ubuntu              Running             Running about a minute ago
3uh3duu79dzm        getstartedlab_web.3   malikchettih/get-started:part2   ubuntu              Running             Running about a minute ago
s8nx4hwpahds        getstartedlab_web.4   malikchettih/get-started:part2   ubuntu              Running             Running about a minute ago
nktcgp1w4gf8        getstartedlab_web.5   malikchettih/get-started:part2   ubuntu              Running             Running about a minute ago

------------------------------------------------------------------
mchettih@ubuntu:~/Projects/docker-trainings/Docker.com - Get Started/part3$ docker container ls -q
0a3ce51c0be9
951074ec9169
2a731803310e
518f41520030
39b815d2386a

------------------------------------------------------------------
mchettih@ubuntu:~/Projects/docker-trainings/Docker.com - Get Started/part3$ docker stack rm getstartedlab
Removing service getstartedlab_web
Removing network getstartedlab_webnet

------------------------------------------------------------------
mchettih@ubuntu:~/Projects/docker-trainings/Docker.com - Get Started/part3$ docker swarm leave --force
Node left the swarm.
