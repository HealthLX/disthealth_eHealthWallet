```
ipfs:
  tty: true
  image: ipfs/go-ipfs:latest
  stdin_open: true
  labels:
      io.rancher.scheduler.affinity:host_label: com.healthlx.provider=mayoclinic
  ports:
  - 80:8080/tcp
  - 4001:4001/tcp
  - 5001:5001:/tcp
volumes:
  - /tmp/ipfs/data:/data/ipfs
  - /tmp/ipfs/staging:/export
```
