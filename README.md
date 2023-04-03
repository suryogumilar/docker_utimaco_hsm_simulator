# Docker for utimaco simulator

how to build:

```
docker build -t local_utimaco_sim:0.0.1 -f Dockerfile.utimaco_hsm_sim .
```

how to run

```
docker run -it \
  --name hsm_simulator \
  -p 3000:3000 -p 3001:3001 \
  --network=wfNetwork \
  local_utimaco_sim:0.0.1 bash
```
