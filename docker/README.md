# stable-diffusion-webui

Stable Diffusion web UI

--------

``` bash

docker build -f docker/Dockerfile -t gabr1elt/stable-diffusion-webui:base --target base
docker build -f docker/Dockerfile -t gabr1elt/stable-diffusion-webui:run --target run

docker run --rm -v ./models:/home/user/stable-diffusion-webui/models -v ./inputs:/home/user/stable-diffusion-webui/inputs -v ./outputs:/home/user/stable-diffusion-webui/outputs -p 127.0.0.1:7860:7860 -it gabr1elt/stable-diffusion-webui:run
docker run --rm -v ./models:/home/user/stable-diffusion-webui/models -v ./inputs:/home/user/stable-diffusion-webui/inputs -v ./outputs:/home/user/stable-diffusion-webui/outputs -p 127.0.0.1:7860:7860 -it gabr1elt/stable-diffusion-webui:run /bin/bash

```