#基于开源项目freeipa-container 自定义option实现静默安装

[root@localhost]# docker build -t kang2023/freeipa-server:rocky-9-4.10.1 -f Dockerfile.rocky-9-kang

#dry run

[root@localhost]# podman run --name freeipa-server-container-test -ti \
    -h freeipa.example.com -p 53:53/udp -p 53:53 \
    -p 80:80 -p 443:443 -p 389:389 -p 636:636 -p 88:88 -p 464:464 -p 88:88/udp \
    -p 464:464/udp --cap-add=SYS_TIME --dns 127.0.0.1 --read-only \
    --sysctl net.ipv6.conf.all.disable_ipv6=0 \
    -v /sys/fs/cgroup:/sys/fs/cgroup:ro \
    -v /var/lib/ipa-data-test:/data:Z  -v /etc/localtime:/etc/locatime:ro \
    -e IP_ADDRESS=`hostname -i` -e DOMAIN_NAME=example.com -e REALM_NAME=EXAMPLE.LOCAL \
    -e HOST_NAME=freeipa.example.com \
    kang2023/freeipa-server:rocky-9-4.10.1
