# AUTOMATIC1111

Stable Diffusion web UI

--------

``` bash

podman build -f docker/Dockerfile -t gabr1elt/automatic1111:base --target base
podman build -f docker/Dockerfile -t gabr1elt/automatic1111:run --target run

podman run --rm -v ./models:/home/user/stable-diffusion-webui/models -v ./inputs:/home/user/stable-diffusion-webui/inputs -v ./outputs:/home/user/stable-diffusion-webui/outputs -p 127.0.0.1:7860:7860 -it gabr1elt/automatic1111:run
podman run --rm -v ./models:/home/user/stable-diffusion-webui/models -v ./inputs:/home/user/stable-diffusion-webui/inputs -v ./outputs:/home/user/stable-diffusion-webui/outputs -p 127.0.0.1:7860:7860 -it gabr1elt/automatic1111:run /bin/bash

```