# SSH Docker GUI


### How To

Get HEX:
```
xauth list | grep "^$(hostname)/unix:10 " | awk '{print $3}'
```

Start Docker
```
docker run -ti -e DISPLAY=$DISPLAY -v /tmp/.X11-unix:/tmp/.X11-unix --net=host  --hostname `hostname`  <DOCKER_IMAGE>
```

Paste HEX:
```
xauth add `hostname`/unix:10  MIT-MAGIC-COOKIE-1 <HEX>
```

### Issues

Might have to clean up `.Xauthority` folder:
```
mv /root/.Xauthority /root/old_folder.Xauthority
mv /root/.Xauthority-n /root/.Xauthority
```
