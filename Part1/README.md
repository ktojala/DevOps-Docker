# DevOps-Docker

# Exercise 1.1

$ docker ps -a  
CONTAINER ID        IMAGE               COMMAND                  CREATED              STATUS                      PORTS               NAMES  
df985d1c5dcf        nginx               "nginx -g 'daemon of…"   59 seconds ago       Up 58 seconds               80/tcp              agitated_shirley  
c621fe68ec42        nginx               "nginx -g 'daemon of…"   About a minute ago   Exited (0) 3 seconds ago                        quirky_torvalds  
44f738171b98        nginx               "nginx -g 'daemon of…"   About a minute ago   Exited (0) 10 seconds ago                       practical_thompson

# Exercise 1.2

$ docker ps -a  
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES  
$ docker images  
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE

# Exercise 1.3

$ docker run -it devopsdockeruh/pull_exercise  
Unable to find image 'devopsdockeruh/pull_exercise:latest' locally  
latest: Pulling from devopsdockeruh/pull_exercise  
8e402f1a9c57: Pull complete  
5e2195587d10: Pull complete  
6f595b2fc66d: Pull complete  
165f32bf4e94: Pull complete  
67c4f504c224: Pull complete  
Digest: sha256:7c0635934049afb9ca0481fb6a58b16100f990a0d62c8665b9cfb5c9ada8a99f  
Status: Downloaded newer image for devopsdockeruh/pull_exercise:latest  
Give me the password: basics  
You found the correct password. Secret message is:  
"This is the secret message"

 
# Exercise 1.4

$ docker run -d -it --name ajettava devopsdockeruh/exec_bash_exercise  
$ docker exec -it ajettava bash  
root@30d3e76b5a90:/usr/app# tail -f ./logs.txt  
Thu, 13 Jun 2019 13:09:58 GMT  
Thu, 13 Jun 2019 13:10:01 GMT  
Thu, 13 Jun 2019 13:10:04 GMT  
Thu, 13 Jun 2019 13:10:07 GMT  
Secret message is:  
"Docker is easy"


# Exercise 1.5

$ docker run  -it --name ajettava ubuntu:16.04 sh -c 'echo "Input website:"; read website; sleep 1; apt-get update; apt-get install -y curl wget; curl http://$website'  
Input website:  
helsinki.fi

That created a long output and finally in its tail end:

<!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">  
<html><head>  
<title>301 Moved Permanently</title>  
</head><body>  
<h1>Moved Permanently</h1>  
<p>The document has moved <a href="http://www.helsinki.fi/">here</a>.</p>  
</body></html>

When curl is in 'ajettava', we get the same output with these commands:

$ docker start ajettava  
$ docker exec -it ajettava bash  
root@67c3566acff0:/# curl helsinki.fi

I found that the following order of subcommands works as the first command as well:  
$ docker run  -it --name ajettava ubuntu:16.04 sh -c 'apt-get update; apt-get install -y curl wget; echo "Input website:"; read website; sleep 1; curl http://$website'


# Exercise 1.6

Dockerfile can be found in folder 'Exercise6'

Commands:

$ docker build -t docker-clock .  
$ docker run docker-clock

# Exercise 1.7

Dockerfile can be found in folder "Exercise7"

Commands:

$ docker build -t curler .  
$ docker run -it curler


# Exercise 1.8

Commands:

$ touch logs.txt  
$ docker run -v $(pwd)/logs.txt:/usr/app/logs.txt devopsdockeruh/first_volume_exercise  
$ cat logs.txt

After the run, there was a secret message in the logs.txt file: "Volume bind mount is easy"

I also learned that the run with -v had to be stopped using ^C when it printed:  
(node:1) ExperimentalWarning: The fs.promises API is experimental  
Wrote to file /usr/app/logs.txt  
Wrote to file /usr/app/logs.txt  
Wrote to file /usr/app/logs.txt  
Wrote to file /usr/app/logs.txt  
Wrote to file /usr/app/logs.txt  
Wrote to file /usr/app/logs.txt  
Wrote to file /usr/app/logs.txt  
^CClosing file

Running the same run with -d -v, it did not produce the above output on my screen but only  
fd5ee4d98306345295e6621ddd7d3ee1babc23066a6ba8923fd63ca7534b1f0e  
(that is the ID of the new container - and the run had to be stopped with docker stop)


# Exercise 1.9

Commands:

$ docker run -p 1234:80 devopsdockeruh/ports_exercise  
$ http://localhost:1234

That web page then shows this text: Ports configured correctly!!


# Exercise 1.10

Commands:

$ docker build -t frontendi .  
$ docker run -p 5000:5000 frontendi

Webpage http://localhost:5000 then says:  Exercise 1.10: Congratulations! You configured your ports correctly!


# Exercise 1.11

Commands:

$ touch logs.txt  
$ docker build -t backendi .  
$ docker run -p 8000:8000 -v $(pwd)/logs.txt:/backend-example-docker/logs.txt backendi

Opening webpage http://localhost:8000 then updates the logs.txt file:  
7/9/2019, 8:46:37 AM: Connection received in root

After reloading the webpage http://localhost:8000 the logs.txt file was:  
7/9/2019, 8:46:37 AM: Connection received in root  
7/9/2019, 8:47:03 AM: Connection received in root

After stopping and rerunning backendi and then reloading the webpage, the logs.txt file was:  
7/9/2019, 8:46:37 AM: Connection received in root  
7/9/2019, 8:47:03 AM: Connection received in root  
7/9/2019, 8:48:56 AM: Connection received in root


# Exercise 1.12

Implemented so that the logs.txt file is still updated when http://localhost:8000/ is visited.  
Relevant PrintScreen file on the http://localhost:5000/ page is also included in the folders.

Commands:

$ docker build -t backendi backendhere/  
$ docker build -t frontendi frontendhere/  
$ docker run -p 8000:8000 -v $(pwd)/backendhere/logs.txt:/backend-example-docker/logs.txt backendi  
$ docker run -d -p 5000:5000 frontendi

I also noticed that it does not matter which container is run first.


# Exercise 1.13

Commands:

$ docker build -t springi .  
$ docker run -d -p 8080:8080 springi


# Exercise 1.14

Commands:

$ docker build -t railssi .  
$ docker run -d -p 3000:3000 railssi  

Got output in http://localhost:3000/presses/new after a press:

New Press

 Total presses: 1

Press was successfully created.

- At first I had "RUN npm install" included and everything worked fine with it. 
Then wondering, where is that line needed? Then repeated the exercise without it. 
On building, step 7 (RUN apt-get install -y  nodejs) had some problems: "Failed to fetch.."  
Then I just repeated the same build command, then step 7 was completed fine.  
It seems that builds sometimes fail with no obvious reason.  


# Exercise 1.15

Opened account at Dockerhub and created a repository youtube-dl there.  
In my own computer, in folder Exercise15, created a slightly modified  
Dockerfile of the youtube-dl example in the course material.

Commands:

$ docker build -t ktojala/youtube-dl .  
$ docker login  
$ docker push ktojala/youtube-dl

Then I deleted this image from my computer and created a new folder /gotvids into my pwd.  
Then in that folder (though I do not need to be in that folder..) I ran:

$ docker pull ktojala/youtube-dl  
$ docker run -v $(pwd):/gotvids ktojala/youtube-dl https://www.youtube.com/watch?v=420UIn01VVc

And the mp4-video appeared into /gotvids folder.

Link to my dockerhub: https://hub.docker.com/r/ktojala/youtube-dl  
( I had a README text also on the dockerhub page but removed it from there.  
  That README text is below and is also in folder /Exercise15. )

"With this app you can download videos from Youtube

1. Have Docker installed in your computer from e.g. https://docs.docker.com/  
2. Create a folder /gotvids into your working directory  
3. Type 'docker pull ktojala/youtube-dl' on command line  
4. Type 'docker run -v $(pwd):/gotvids ktojala/youtube-dl < webpage >'  
5. Video appears in your /gotvids folder"


# Exercise 1.16

https://dockersapp.herokuapp.com/


# Exercise 1.17

skipped

