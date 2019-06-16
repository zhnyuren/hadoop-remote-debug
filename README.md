# hadoop-remote-debug
hadoop remote debug using intellij idea and maven

environment: macOS Mojave 10.14.5 (client), CentOS 7 (server), hadoop 2.9.2

1. install hadoop 2.9.2, hdfs, mysql, hive on server
2. install hadoop 2.9.2 (same version with the server) on macOS and configure environment path
3. edit /etc/hosts on the server (127.0.1.1 should be commented)
![image](https://github.com/zhnyuren/hadoop-remote-debug/blob/master/images/pic1.png)
4. edit $HADOOP_HOME/etc/hadoop/core-site.xml file (change "localhost" to hostname)
![image](https://github.com/zhnyuren/hadoop-remote-debug/blob/master/images/pic2.png)
5. format your hadoop with "hadoop namenode -format"
6. notice that the "host" is your server ip address, not "localhost" / "127.0.0.1" / "127.0.1.1". Or you cannot access the server through port 9000
![image](https://github.com/zhnyuren/hadoop-remote-debug/blob/master/images/pic3.png)
7. delete tmp/ directory with "rm -rf $HADOOP_HOME/tmp/" to avoid NameNode & DataNode having different ClusterID
8. restart your hadoop with ".$HADOOP_HOME/sbin/start-all.sh"
9. confirm "namenode", "datanode", "secondary namenode" are running using "jps"
10. check port 9000 is available for remote connection with "netstat -tpln" (before ":9000" should be you server IP address not 127.0.0.1)
![image](https://github.com/zhnyuren/hadoop-remote-debug/blob/master/images/pic4.png)
11. check port 9000 using "telnet <your server IP addr> 9000"
12. create a new Maven project using intellij idea and copy "core-site.xml" from server to directory ProjectName/src/main/resources/ and delete hadoop.tmp.dir configuration or it will generate the wrong tmp dir on your client.
13. edit "Run/Debug Configuration" as follow
![image](https://github.com/zhnyuren/hadoop-remote-debug/blob/master/images/pic5.png)
14. you can debug the hadoop project remotely using intellij idea
