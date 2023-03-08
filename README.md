# Airflow - Docker


## Initialize the database

On all operating systems, you need to run database migrations and create the first user account. To do it, run.

```
cp .env_example .env
docker-compose up airflow-init
```

After initialization is complete, you should see a message like below.

```
airflow-init_1       | Upgrades done
airflow-init_1       | Admin user airflow created
airflow-init_1       | 2.3.4
start_airflow-init_1 exited with code 0
```

The account created has the login airflow and the password airflow.

## Running Airflow

Now you can start all services:

```
docker-compose up
```

In the second terminal you can check the condition of the containers and make sure that no containers are in unhealthy condition:

```
$ docker ps
CONTAINER ID   IMAGE                  COMMAND                  CREATED          STATUS                    PORTS                              NAMES
247ebe6cf87a   apache/airflow:2.3.4   "/usr/bin/dumb-init …"   3 minutes ago    Up 3 minutes (healthy)    8080/tcp                           compose_airflow-worker_1
ed9b09fc84b1   apache/airflow:2.3.4   "/usr/bin/dumb-init …"   3 minutes ago    Up 3 minutes (healthy)    8080/tcp                           compose_airflow-scheduler_1
7cb1fb603a98   apache/airflow:2.3.4   "/usr/bin/dumb-init …"   3 minutes ago    Up 3 minutes (healthy)    0.0.0.0:8080->8080/tcp             compose_airflow-webserver_1
74f3bbe506eb   postgres:13            "docker-entrypoint.s…"   18 minutes ago   Up 17 minutes (healthy)   5432/tcp                           compose_postgres_1
0bd6576d23cb   redis:latest           "docker-entrypoint.s…"   10 hours ago     Up 17 minutes (healthy)   0.0.0.0:6379->6379/tcp   
```


## Running the CLI commands

You can also run CLI commands, but you have to do it in one of the defined airflow-* services. For example, to run airflow info, run the following command:


```
docker-compose run airflow-worker airflow info

```

If you have Linux or Mac OS, you can make your work easier and download a optional wrapper scripts that will allow you to run commands with a simpler command.

```
chmod +x airflow.sh
```

Now you can run commands easier.

```
./airflow.sh info

```

You can also use bash as parameter to enter interactive bash shell in the container or python to enter python container.

```
./airflow.sh bash
./airflow.sh python
```
