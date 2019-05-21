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


### Automated Version

Add to `~/.bashrc` and use `xac <container_name>`:
```
# functions
___xac() {
    container=${1:-'valid_container_namei'}
    display_id=`echo $DISPLAY | grep -Eo '[+-]?[0-9]+([.][0-9]+)?'`
    display_id=${display_id%".0"}
    docker exec $container sh -c "xauth add `hostname`/unix:$display_id  MIT-MAGIC-COOKIE-1 `xauth list | grep "^$(hostname)/unix:$display_id " | awk '{print $3}'`"
}

# aliases
alias xac=___xac
```

Then call:
```
$ xac <container_name_or_id>
```
