# Docker
| Virtual machine | Docker |
|-----------------|--------|
| Thêm Guest OS | Dùng chung kernel |
| Tốn tài nguyên | Cô lập về mặt TN |


##### Docker storage: 
- Help Container write data to Docker Host (because Container can't share data)
- Persistent Data: store container data to docker host using mount folder from container to docker host:
    + Volumns mount
    + Bind mount
    + Tmpfs mount





##### Use Containerization (Công nghệ của Linux)
- CGroup: Giới hạn tài nguyên sử dụng RAM, CPU, Storage
- Namespace: Cô lập các tiến trình


##### Docker Component
- Docker CLI - client
- Docker Host
- Docker Registry

alpine < slim < bust : weight


##### Common command
```
docker ps -a
docker run -itd --name my_name image_name:tag // i: interactive, t: tty allow open new section, d: detach in background (terminal)
docker container rm -f <id/name>
docker exec -it <id> bash
```

**Volume Mount**
```
docker volume create my-volume
docker volume ls
docker volume inspect my-volume
// Volume:Absolute_Path
docker run -itd -v my-volume:/opt/mount_point centos
docker run -itd --mount type=volume,src=my-volume,des=/opt/mount_point centos
docker container inspect <containerID>
docker exec 5f0c bash -c "echo 'This is file test' > /opt/mount_point/test.txt"
docker exec 5f0c bash -c "cat /opt/mount_point/test.txt"
sudo cat /var/lib/docker/volumes/my-volume/_data/test.txt
```

**Bind Mount**
```
// Path:Path
docker run -itd -v /opt/docker_host_folder:/opt/mount_point centos
// Require directory if use --mount
sudo mkdir -p /opt/docker_host_mount 
docker run -itd --mount type=bind,src=/opt/docker_host_mount,dst=/opt/mount_point centos
docker exec dd65 bash -c "echo 'hello e' -> /opt/mount_point/test.txt"
docker exec dd65 bash -c "cat /opt/mount_point/test.txt"
cat /opt/docker_host_mount/test.txt
```


##### Container: Runtime env