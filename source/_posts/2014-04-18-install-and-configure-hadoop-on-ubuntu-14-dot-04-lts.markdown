---
layout: post
title: "Install and Configure Hadoop on Ubuntu 14.04 LTS"
date: 2014-04-18 23:38:24 +0700
comments: true
categories: [ubuntu, learning, hadoop]
---

Following steps were copied from a [blog post](http://codesfusion.blogspot.com/2013/10/setup-hadoop-2x-220-on-ubuntu.html) and kept here for reference purpose only.

# Download Hadoop 2.4.0

```
$ cd ~
$ wget http://apache.osuosl.org/hadoop/common/hadoop-2.4.0/hadoop-2.4.0.tar.gz
$ sudo tar vxzf hadoop-2.4.0.tar.gz -C /usr/local
$ cd /usr/local
$ sudo mv hadoop-2.4.0 hadoop
$ sudo chown -R hduser:hadoop hadoop
```

# Setup Hadoop Environment Variables

```
$cd ~
$vi .bashrc
```

paste following to the end of the file

```
#Hadoop variables
export JAVA_HOME=/usr/lib/jvm/jdk/
export HADOOP_INSTALL=/usr/local/hadoop
export PATH=$PATH:$HADOOP_INSTALL/bin
export PATH=$PATH:$HADOOP_INSTALL/sbin
export HADOOP_MAPRED_HOME=$HADOOP_INSTALL
export HADOOP_COMMON_HOME=$HADOOP_INSTALL
export HADOOP_HDFS_HOME=$HADOOP_INSTALL
export YARN_HOME=$HADOOP_INSTALL
export HADOOP_COMMON_LIB_NATIVE_DIR=${HADOOP_INSTALL}/lib/native
export HADOOP_OPTS="-Djava.library.path=$HADOOP_INSTALL/lib"
###end of paste
```

```
$ cd /usr/local/hadoop/etc/hadoop
$ vi hadoop-env.sh

#modify JAVA_HOME
export JAVA_HOME=/usr/lib/jvm/jdk/
Re-login into Ubuntu using hdser and check hadoop version
$ hadoop version
Hadoop 2.4.0
Subversion http://svn.apache.org/repos/asf/hadoop/common -r 1583262
Compiled by jenkins on 2014-03-31T08:29Z
Compiled with protoc 2.5.0
From source with checksum 375b2832a6641759c6eaf6e3e998147
This command was run using /usr/local/hadoop-2.4.0/share/hadoop/common/hadoop-common-2.4.0.jar
``` 
At this point, hadoop is installed.

# Configuring Hadoop

based on script of ericduq at https://github.com/ericduq/hadoop-scripts/blob/master/make-single-node.sh

```
$ cd /usr/local/hadoop/etc/hadoop
# Edit configuration files
$ sudo -u hduser sed -i.bak 's=<configuration>=<configuration>\<property>\<name>fs\.default\.name\</name>\<value>hdfs://localhost:9000\</value>\</property>=g' core-site.xml 
$ sudo -u hduser sed -i.bak 's=<configuration>=<configuration>\<property>\<name>yarn\.nodemanager\.aux-services</name>\<value>mapreduce_shuffle</value>\</property>\<property>\<name>yarn.nodemanager.aux-services.mapreduce.shuffle.class</name>\<value>org\.apache\.hadoop\.mapred\.ShuffleHandler</value>\</property>=g' yarn-site.xml
  
$ sudo -u hduser cp mapred-site.xml.template mapred-site.xml
$ sudo -u hduser sed -i.bak 's=<configuration>=<configuration>\<property>\<name>mapreduce\.framework\.name</name>\<value>yarn</value>\</property>=g' mapred-site.xml
 
$ cd ~
$ mkdir -p mydata/hdfs/namenode
$ mkdir -p mydata/hdfs/datanode

$ cd /usr/local/hadoop/etc/hadoop
$ sudo -u hduser sed -i.bak 's=<configuration>=<configuration>\<property>\<name>dfs\.replication</name>\<value>1\</value>\</property>\<property>\<name>dfs\.namenode\.name\.dir</name>\<value>file:/home/hduser/mydata/hdfs/namenode</value>\</property>\<property>\<name>dfs\.datanode\.data\.dir</name>\<value>file:/home/hduser/mydata/hdfs/datanode</value>\</property>=g' hdfs-site.xml


# Format Namenode
# hdfs namenode -format

# Start Hadoop Service
# sudo -u hduser start-dfs.sh
# sudo -u hduser start-yarn.sh

# Check status
# sudo -u hduser jps

# Example
# sudo -u hduser cd /usr/local/hadoop
# sudo -u hduser hadoop jar ./share/hadoop/mapreduce/hadoop-mapreduce-examples-2.2.0.jar pi 2 5
```
