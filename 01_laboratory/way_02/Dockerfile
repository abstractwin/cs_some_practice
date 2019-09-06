FROM ubuntu:latest
RUN apt-get update
RUN apt-get -y upgrade
RUN apt-get install -y gcc
RUN apt-get install -y nano
ADD main.c main.c
RUN gcc main.c -o main
