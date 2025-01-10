# load_testing
Tests for load testing websites
Task: Conduct Load Test and Stress Test

Test Scenario:

Step 1: Visit the following link:
https://ip.2025ngvolunteer.hk/hello.php
Step 2: Click on the video link button.
Step 3: After Step 2, visit the following link:
https://portal.2025ngvolunteer.hk/player.html


Performance Requirements:
- Process 100,000 visitors per minute.
- 95% of requests should complete within 3 seconds.
- The error rate for all requests should be below 1%.


Test 1: 
Use JMeter to conduct load and stress tests, and export the report in CSV and graphic presentation formats.

Test 2 and Beyond:

Use PuTTY to log in to the server.

Host: s72.igears.com.hk
Port: 22
Login: root
Password: igttest123

Edit the Apache configuration file to improve performance for concurrent users, and conduct the same tests again.


Apache Configuration Location:

Located at /etc/httpd/
The main configuration file is at conf/httpd.conf, and other configuration files may also be relevant to this issue.
After you edit the configuration files, you will need to run the following command to make the changes take effect:

service httpd restart

sudo nano /etc/httpd/conf/httpd.conf

directory for tests

cd "C:\Users\igears\Task 3 Load Testing\Apache JMeter\apache-jmeter-5.6.3\bin"

commands to run tests:

jmeter -n -t Test_main.jmx -l Test_Main/results.csv -e -o Test_Main
jmeter -n -t Alternative_Test.jmx -l Alternative_Test/results.csv -e -o Alternative_Test


command to restart apache:
systemctl restart httpd







changes made

sudo nano /etc/httpd/conf/httpd.conf
<IfModule mpm_event_module>
    StartServers             10
    MinSpareThreads         75
    MaxSpareThreads        250
    ThreadLimit            100
    ThreadsPerChild         64
    MaxRequestWorkers     6400
    MaxConnectionsPerChild   0
    ServerLimit            100
</IfModule>


sudo nano /etc/httpd/conf/httpd.conf

KeepAlive On
MaxKeepAliveRequests 100
KeepAliveTimeout 5

sudo nano /etc/security/limits.conf

* soft nofile 65536
* hard nofile 65536

sudo nano /etc/pam.d/common-session
sudo nano /etc/pam.d/common-session-noninteractive

session required pam_limits.so

sudo nano /etc/sysctl.conf

fs.file-max = 65536
sudo sysctl -p


sudo nano /etc/sysctl.conf

net.core.somaxconn = 65535
net.core.netdev_max_backlog = 65535
net.ipv4.tcp_max_syn_backlog = 65535
net.ipv4.tcp_fin_timeout = 10
net.ipv4.tcp_tw_reuse = 1
net.ipv4.ip_local_port_range = 1024 65535
net.ipv4.tcp_rmem = 4096 87380 6291456
net.ipv4.tcp_wmem = 4096 65536 6291456
net.ipv4.tcp_moderate_rcvbuf = 1
net.ipv4.tcp_congestion_control = cubic
net.ipv4.tcp_syncookies = 1


sudo sysctl -p


sudo nano /etc/sysctl.conf
net.ipv4.tcp_fastopen = 3
sudo sysctl -p




sudo nano /etc/httpd/conf/httpd.conf

LoadModule cache_module modules/mod_cache.so
LoadModule cache_disk_module modules/mod_cache_disk.so
CacheRoot "/var/cache/mod_cache"
CacheEnable disk /
CacheDirLevels 2
CacheDirLength 1
CacheMaxFileSize 1000000
CacheMinFileSize 1
CacheDefaultExpire 3600
CacheMaxExpire 86400
CacheLastModifiedFactor 0.1
CacheIgnoreCacheControl On
CacheIgnoreNoLastMod On
CacheStorePrivate On
CacheStoreNoStore On











