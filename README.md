# Docker for utimaco simulator

how to build:

```
docker build -t local_utimaco_sim:0.0.1 -f Dockerfile.utimaco_hsm_sim .
```

how to run

```
docker run -it \
  --name hsm_simulator \
  -p 3000:3000 -p 3001:3001 -p 3002:3002 -p 6070:6070 \
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
 - Also export CS_PKCS11_R3_CFG containing path of `cs_pkcs11_R2.cfg` file
   ```sh
   CS_PKCS11_R3_CFG=./utimaco/etc_utimaco/cs_pkcs11_R2_copi1.cfg
   export CS_PKCS11_R3_CFG
   ```
 - run `java -jar cat.jar` for run CAT or:
 - run `java -jar p11cat.jar` for runing p11 cat 

### Configure HSM simulator

 - create `/opt/utimaco` directory that can be accessed by user, or whatever directory 
   in the `KeyStore` configuration inside `CS_PKCS11_R2_CFG` or `CS_PKCS11_R3_CFG` file 
 - in the configuration file (`CS_PKCS11_R2_CFG` or  `CS_PKCS11_R3_CFG`), 
   edit CryptoServer part, set Device to hsm simulator machine ip:   

   ```
   # example:
   Device = 3001@172.19.0.2
   ```

 - export CS_PKCS11_R3_CFG and/or CS_PKCS11_R2_CFG environment variables
 - Run cat.jar
   - login using keyfile provided in installation folder and user is ADMIN
     ```
     ./SecurityServerEvaluation-V4.51.0.1/Software/Linux/x86-64/\
     Administration/key/ADMIN.key` 
     ```   
     leave the password blank
   - Manage firmware, update the firmware located in
     ```
     ./SecurityServerEvaluation-V4.51.0.1/Firmware/SecurityServer-Simulator\
     /SecurityServer-Simulator-4.51.0.1-linux.mpkg     
     ```

     select 'Updates (install only new firmware)'
 - run p11cat.jar
   - choose slot, e.g: slot 0
   - login using keyfile, enter ADMIN as username
   - Choose 'slot management' icon to init the slot token
   - choose 'Init token'
   - enter SO Pin, for example '12345678' then click 'Init token'

