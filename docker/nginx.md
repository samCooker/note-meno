# docker

docker run  --name nginx-scx -itd -p 23333:23333 -v /opt/shicx/myNginx/html:/usr/share/nginx/html -v /opt/shicx/myNginx/conf.d:/etc/nginx/conf.d -v /opt/shicx/myNginx/log:/var/log/nginx/ --link=tomcat-scx-01:tomcat-scx-01 c82521676580

docker run --name tomcat-scx-01 -itd -p 20001:8080 -v /opt/shicx/docker-webapps/tomcat-01/upload:/opt/upload -v /opt/shicx/docker-webapps/tomcat-01/logs:/usr/local/tomcat/logs -v /opt/shicx/docker-webapps/tomcat-01/webapps:/usr/local/tomcat/webapps 2d43521f2b1a