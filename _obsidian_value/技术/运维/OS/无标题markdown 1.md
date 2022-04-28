#### 远程传输
    scp graph.db.dump root@mirror.sinocbd.local:/root
    
#### 查看系统日志
    sudo journalctl

#### 系统服务
    systemctl [start|stop|statue|restart] <service>

#### docker 相关
    docker images
    docker ps -a
    docker [rmi|rm] $(docker ps -a -q)
    docker pull <register.docker>
    docker run -it <container> /sh
    docker exec -it <containe> /sh
    docker build .
    
    docker-compose up
    docker-compose down
    
    

#### neo4j 数据备份/恢复
    neo4j-admin [dump|load] --graph=<graph> 
    --[to|from]
    
#### 查看端口情况
    sudo lsof -i :2181

#### scp
    scp -r OpenOPC-develop-environment.zip root@172.25.2.60:/var/www/resources/openopc