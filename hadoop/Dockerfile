FROM centos7-ssh
MAINTAINER sow <watson.song@gmial.com>

WORKDIR /root

# ssh without key
RUN ssh-keygen -t rsa -f ~/.ssh/id_rsa -P '' && \
    cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys
    
ADD server-jre-8u291-linux-x64.tar.gz /usr/local/
RUN mv /usr/local/jdk1.8.0_291 /usr/local/jdk1.8
ENV JAVA_HOME=/usr/local/jdk1.8
ENV PATH=$JAVA_HOME/bin:$PATH

ADD hadoop-3.3.1.tar.gz /usr/local
RUN mv /usr/local/hadoop-3.3.1 /usr/local/hadoop
ENV HADOOP_HOME=/usr/local/hadoop
ENV PATH=$HADOOP_HOME/bin:$HADOOP_HOME/sbin:$PATH

RUN adduser hadoop
RUN echo "hadoop:hadoop" | chpasswd
RUN usermod -a -G hadoop hadoop
RUN echo "hadoop    ALL=(ALL)     ALL" >> /etc/sudoers

RUN mkdir -p ~/hdfs/namenode && \ 
    mkdir -p ~/hdfs/datanode && \
    mkdir $HADOOP_HOME/logs
    
COPY config/* /tmp/

RUN mv /tmp/ssh_config ~/.ssh/config && \
    mv /tmp/hadoop-env.sh $HADOOP_HOME/etc/hadoop/hadoop-env.sh && \
    mv /tmp/hdfs-site.xml $HADOOP_HOME/etc/hadoop/hdfs-site.xml && \ 
    mv /tmp/core-site.xml $HADOOP_HOME/etc/hadoop/core-site.xml && \
    mv /tmp/mapred-site.xml $HADOOP_HOME/etc/hadoop/mapred-site.xml && \
    mv /tmp/yarn-site.xml $HADOOP_HOME/etc/hadoop/yarn-site.xml && \
    mv /tmp/slaves $HADOOP_HOME/etc/hadoop/slaves && \
    mv /tmp/workers $HADOOP_HOME/etc/hadoop/workers && \
    mv /tmp/start-hadoop.sh ~/start-hadoop.sh && \
    mv /tmp/run-wordcount.sh ~/run-wordcount.sh

RUN chmod 600 ~/.ssh/config

RUN chmod +x ~/start-hadoop.sh && \
    chmod +x ~/run-wordcount.sh && \
    chmod +x $HADOOP_HOME/sbin/start-dfs.sh && \
    chmod +x $HADOOP_HOME/sbin/start-yarn.sh 

# format namenode
RUN $HADOOP_HOME/bin/hdfs namenode -format
EXPOSE 50070 8088 9000