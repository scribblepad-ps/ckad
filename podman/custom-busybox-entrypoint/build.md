## Custom busybox image with CMD[] and ENTRYPOINT[]

### Podman Build

   ❯ podman build custom-busybox-entrypoint -t docker.io/scribblepad/custom-busybox-entrypoint
   
   
   STEP 1/3: FROM busybox:musl
   STEP 2/3: ENTRYPOINT ["echo","\t\t"]
   --> Using cache 6ab92e230a344dc17e6225cc7a75c738a2e6e452595e04a91a2b714c31f8a1f1
   --> 6ab92e230a3
   STEP 3/3: CMD ["RED"]
   --> Using cache 4aee25325740f88903b182045e78270ff2d63c6d6315cfa45f0c0e2ebc11f1c9
   COMMIT docker.io/scribblepad/custom-busybox-entrypoint
   --> 4aee2532574
   Successfully tagged docker.io/scribblepad/custom-busybox-entrypoint:latest
   4aee25325740f88903b182045e78270ff2d63c6d6315cfa45f0c0e2ebc11f1c9


### Podman Push to docker.io

   ❯ podman push docker.io/scribblepad/custom-busybox-entrypoint
   
   
   Getting image source signatures
   Copying blob d3c2197ed4c4 [--------------------------------------] 0.0b / 0.0b
   Copying config 4aee253257 done  
   Writing manifest to image destination
   Storing signatures



### Podman run command
   ❯ podman run --rm docker.io/scribblepad/custom-busybox-entrypoint
                  RED


### Podman run command overriding the CMD

   ❯ podman run --rm docker.io/scribblepad/custom-busybox-entrypoint BLUE
                  BLUE

### Podman run command overriding the ENTRYPOINT

   ❯ podman run --rm --entrypoint '["hostname"]' docker.io/scribblepad/custom-busybox-entrypoint
   11078e0b31df


### Podman run command overriding the ENTRYPOINT and CMD

   ❯ podman run --rm --entrypoint '["ip"]' docker.io/scribblepad/custom-busybox-entrypoint 'addr'


   1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN qlen 1000
      link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
      inet 127.0.0.1/8 scope host lo
         valid_lft forever preferred_lft forever
      inet6 ::1/128 scope host 
         valid_lft forever preferred_lft forever
   2: tap0: <BROADCAST,UP,LOWER_UP> mtu 65520 qdisc fq_codel state UNKNOWN qlen 1000
      link/ether 2e:72:9f:82:23:d3 brd ff:ff:ff:ff:ff:ff
      inet 10.0.2.100/24 brd 10.0.2.255 scope global tap0
         valid_lft forever preferred_lft forever
      inet6 fe80::2c72:9fff:fe82:23d3/64 scope link tentative 
         valid_lft forever preferred_lft forever


