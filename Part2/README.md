# DevOps-Docker Part 2 exercises

# Exercise 2.1

$ docker-compose up


# Exercise 2.2

$ docker-compose up

( $ curl localhost:80 gave:
Ports configured correctly!  )


# Exercise 2.3

$ docker-compose up

Not easy to tell whether this is working correctly or not, but after the above command,
the following lines appear among a long list of lines:

backend_1   | Started on port 8000
frontend_1  | INFO: Accepting connections at http://localhost:5000


# Exercise 2.4

$ docker-compose up -d --scale compute=3

Got green button with "Congratulations".
This one works too:

$ docker-compose up -d --scale compute=2


# Exercise 2.5

$ docker-compose up

Working! It took 0.035 seconds.

(If I repeat clicking, responses are faster, 0.009-0.031 seconds.)


# Exercise 2.6

$ docker-compose up

A screenshot on working exercise is included in the exercise folder.


# Exercise 2.7

$ docker-compose up

An example of a successful run is included in the /data folder.


# Exercise 2.8

$ docker-compose up

A screenshot on working exercise is included in the exercise folder.


# Exercise 2.9

$ docker-compose up
$ docker-compose down

Intermediate results from the postgres part can be found from the screenshots folder.
In addition a screenshot showing how the docker-compose has "captured" the redis-data
folder.


# Exercise 2.10

skipped

