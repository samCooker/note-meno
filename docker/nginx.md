# docker

- nginx

docker run  --name nginx-scx -itd -p 23333:23333 -v /opt/shicx/myNginx/html:/usr/share/nginx/html -v /opt/shicx/myNginx/conf.d:/etc/nginx/conf.d -v /opt/shicx/myNginx/log:/var/log/nginx/ --link=tomcat-scx-01:tomcat-scx-01 --link=tomcat-scx-02:tomcat-scx-02 c82521676580

docker run  --name nginx-80 -itd -p 80:80 -v /opt/shicx/nginx80/html:/usr/share/nginx/html -v /opt/shicx/nginx80/conf.d:/etc/nginx/conf.d -v /opt/shicx/nginx80/log:/var/log/nginx/ --link=tomcat-scx-01:tomcat-scx-01 c82521676580

- tomcat

docker run --name tomcat-scx-01 -itd -p 20001:8080 -v /opt/shicx/docker-webapps/tomcat-01/upload:/opt/upload -v /opt/shicx/docker-webapps/tomcat-01/logs:/usr/local/tomcat/logs -v /opt/shicx/docker-webapps/tomcat-01/webapps:/usr/local/tomcat/webapps 2d43521f2b1a

docker run --name tomcat-scx-02 -itd -p 20002:8080 -v /opt/shicx/docker-webapps/tomcat-02/upload:/opt/upload -v /opt/shicx/docker-webapps/tomcat-02/logs:/usr/local/tomcat/logs -v /opt/shicx/docker-webapps/tomcat-02/webapps:/usr/local/tomcat/webapps 2d43521f2b1a

- node

docker run --name node-scx-20003 -itd -p 20003:8080 -v /opt/shicx/docker-node/servers:/opt/node-servers --link=node-scx-20003:node-scx-20003 8672b25e842c

- mysql
docker run --name mysql3306 -itd -p 3306:3306 -v /opt/shicx/docker-mysql/mysqld.cnf:/etc/mysql/mysql.conf.d -v /opt/shicx/docker-mysql/data:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=123456 docker.io/mysql:5

- kms

docker run -d --name kms -p 8888:8888 9247e88b6a09

- openmeetings

docker run -d -t -i --name apache-openmeetings -p 23333:23333 -p 20005:1935 -p 20006:8088 dramaturg/apache-openmeetings