FROM ubuntu:16.04
WORKDIR /DevOps-Docker/Part1/Exercise7/
RUN apt-get update && apt-get install -y curl

COPY curling.sh .
RUN chmod +x ./curling.sh

CMD ["./curling.sh"]
