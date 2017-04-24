# from vkill/ubuntu-systemd-sshd
# gator1/ubuntu-systemd-sshd

[`solita/ubuntu-systemd`](https://hub.docker.com/r/solita/ubuntu-systemd/) + an SSH server.

## Supported tags

* `latest`

## Reason 

```
need to allow root login. This is going to be used for ceph in docker. 
```

### For Docker

```
$ touch ~/.ssh/authorized_keys
$ chmod 600 ~/.ssh/authorized_keys
$ cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys
```

```
$ docker run -it --rm --name systemd-sshd --security-opt seccomp=unconfined --tmpfs /run --tmpfs /run/lock -v /sys/fs/cgroup:/sys/fs/cgroup:ro -v /var/run/sshd_docker:/var/run/sshd -v ~/.ssh/authorized_keys:/root/.ssh/authorized_keys -d vkill/systemd-sshd
```

```
$ docker exec systemd-sshd systemctl status
$ docker exec systemd-sshd ps aux
```

### For Docker Compose

[Ref](https://github.com/vkill/docker-systemd-sshd/blob/master/docker-compose.yml)

## Test

```
$ git clone git@github.com:gator1/docker-systemd-sshd.git
$ cd docker-systemd-sshd

$ docker-compose up -d

$ docker-compose exec sshd systemctl status

$ docker-compose exec sshd ps aux

$ ssh root@10.0.99.2
```

License
-------

MIT / BSD

Author Information
------------------

gator1, garyxia@gmail.com

&copy; 2017
