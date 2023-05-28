# stable-diffusion-webui

Stable Diffusion web UI

--------

``` bash

podman build \
    . \
    -f docker/Dockerfile.podman \
    -t gabr1elt/stable-diffusion-webui

podman run \
    --rm \
    -it \
    # use gpu (CDI)
    --device nvidia.com/gpu=all \
    -p 127.0.0.1:7860:7860 \
    -v ./models:/home/user/stable-diffusion-webui/models \
    -v ./inputs:/home/user/stable-diffusion-webui/inputs \
    -v ./outputs:/home/user/stable-diffusion-webui/outputs \
    -h "stable-diffusion-webui" \
    gabr1elt/stable-diffusion-webui
    # gabr1elt/stable-diffusion-webui /bin/bash

podman run \
    --rm \
    -it \
    --device nvidia.com/gpu=all \
    -p 127.0.0.1:7860:7860 \
    -v ./models:/home/user/stable-diffusion-webui/models \
    -v ./inputs:/home/user/stable-diffusion-webui/inputs \
    -v ./outputs:/home/user/stable-diffusion-webui/outputs \
    -h "stable-diffusion-webui" \
    gabr1elt/stable-diffusion-webui

```

``` bash

cd ./docker

docker build -t gabr1elt/stable-diffusion-webui:base --target base ./
docker build -t gabr1elt/stable-diffusion-webui:run --target run ./

docker run --rm -v models:/home/user/Development/stable-diffusion-webui/models -v inputs:/home/user/Development/stable-diffusion-webui/inputs -v outputs:/home/user/Development/stable-diffusion-webui/outputs -p 127.0.0.1:7860:7860 -it gabr1elt/stable-diffusion-webui:run
docker run --rm -v models:/home/user/Development/stable-diffusion-webui/models -v inputs:/home/user/Development/stable-diffusion-webui/inputs -v outputs:/home/user/Development/stable-diffusion-webui/outputs -p 127.0.0.1:7860:7860 -it gabr1elt/stable-diffusion-webui:run /bin/bash

```