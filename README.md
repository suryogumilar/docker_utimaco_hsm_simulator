# Docker for utimaco simulator

how to build:

```
docker build -t local_utimaco_sim:0.0.1 -f Dockerfile.utimaco_hsm_sim .
```

how to run

```
docker run -it \
  --name hsm_simulator \
  -p 3000:3000 -p 3001:3001 -p 6070:6070 \
  --network=wfNetwork \
  local_utimaco_sim:0.0.1 bash
```

### CAT accessing the simulator from remote access

in the remote machine that can reach the simulator machine or container do:

 - export CS_PKCS11_R2_CFG containing path of `cs_pkcs11_R2.cfg` file
   ```sh
   CS_PKCS11_R2_CFG=./utimaco/etc_utimaco/cs_pkcs11_R2_copi1.cfg
   export CS_PKCS11_R2_CFG
   ```
 - run `java -jar cat.jar` for run CAT or:
 - run `java -jar p11cat.jar` for runing p11 cat 
