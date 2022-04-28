### 查看 image/container 状态
    docker images
    docker ps -a

### 清除 image/container
    docker rm <container_id>
    docker rmi <image_id>


### 停止所有容器并清除
    docker stop $(docker ps -a -q)
    docker rm $(docker ps -a -q)
    
    docker rmi $(docker iamges -q)

### 进入构建结束的 image/container
    docker run -it <image_id> sh
    docker exec -it [image_id] sh


