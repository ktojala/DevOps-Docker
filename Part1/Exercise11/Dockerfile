FROM ubuntu:16.04
EXPOSE 8000

RUN apt-get update && apt-get install -y git curl

RUN git clone https://git@github.com/docker-hy/backend-example-docker.git
WORKDIR /backend-example-docker
COPY logs.txt .

RUN curl -sL https://deb.nodesource.com/setup_10.x | bash
RUN apt-get install -y  nodejs
RUN npm install
CMD npm start
