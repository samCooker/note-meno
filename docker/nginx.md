# docker

docker run  --name nginx-scx -itd -p 23333:23333 -v /opt/shicx/myNginx/html:/usr/share/nginx/html -v /opt/shicx/myNginx/conf.d:/etc/nginx/conf.d -v /opt/shicx/myNginx/log:/var/log/nginx/ --link=tomcat-scx-01:tomcat-scx-01 c82521676580