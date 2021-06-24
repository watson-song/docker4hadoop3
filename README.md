# docker4hadoop3
Prepare docker environment for Hadoop 3.3.1

# What you need to replace...
1. download real file from file:hadoop-3.3.1.tar.gz.fake
2. download real jre1.8 from oracle website

# Steps to build image:
1. Build Centos7-SSH image
2. Build Hadoop3.3.1 base on centos7-ssh image

## Build Centos7-SSH image
root$ cd centos7
root$ docker build -t centos7-ssh .

## Build Hadoop3.3.1 base on centos7-ssh image
root$ cd hadoop
root$ docker build -t hadoop .
......waiting for complete......
...
...
complete!
root$ ./start-container.sh
root@hadoop-master$ ./start-hadoop.sh
root@hadoop-master$ ./run-wordcount.sh

---------------
Open http://hadoop-master:8088
