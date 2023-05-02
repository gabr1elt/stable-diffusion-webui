# FROM ubuntu as base
# FROM debian:11 as base
# FROM nvidia/cuda:12.1.1-devel-ubuntu22.04 as base
FROM nvidia/cuda:12.1.1-runtime-ubuntu22.04 as base

ENV DEBIAN_FRONTEND=noninteractive

# Install the dependencies:
RUN apt-get update -y && \
    # apt-get upgrade -y && \
    apt-get install -y \
    wget \
    # curl \
    git \
    python3 \
    # libgl1 \
    # libglib2.0-0 \
    python3-opencv \
    python3-pip \
    python3-venv && \
    apt-get clean -y && \
    rm -rf /var/lib/apt/lists/*


# add user
RUN adduser --disabled-password --gecos '' user
# RUN mkdir /content && chown -R user:user /content

USER user

ARG HOME=/home/user

WORKDIR $HOME

# COPY ./webui-user.sh ./webui-user.sh

# done also on launch.py called by webui.sh
RUN git clone https://github.com/AUTOMATIC1111/stable-diffusion-webui.git
# ARG SHA=a9fed7c364061ae6efb37f797b6b522cb3cf7aa2
# RUN git clone https://github.com/AUTOMATIC1111/stable-diffusion-webui.git && \
#   cd stable-diffusion-webui && \
#   git fetch && \
#   git reset --hard ${SHA} && \
#   pip install -r requirements_versions.txt


# fix for ImportError: libGL.so.1: cannot open shared object file: No such file or directory
# RUN pip install opencv-python-headless


# To install in /home/$(whoami)/stable-diffusion-webui/, run:
# RUN bash <(wget -qO- https://raw.githubusercontent.com/AUTOMATIC1111/stable-diffusion-webui/master/webui.sh)
# RUN curl -fsSL https://raw.githubusercontent.com/AUTOMATIC1111/stable-diffusion-webui/master/webui.sh | bash


# RUN wget -q https://raw.githubusercontent.com/AUTOMATIC1111/stable-diffusion-webui/master/webui.sh && \
#     /bin/bash ./webui.sh


# RUN sed -i -e 's/if \'--nowebui\' in sys.argv:/if \'--nowebui\' in sys.argv and \'--noapi\' not in sys.argv:/g' /content/stable-diffusion-webui/launch.py
# RUN sed -i -e "s/webui.api_only()/print('Not launching API server for now')/g" stable-diffusion-webui/launch.py

ARG CLI_ARGS="--skip-torch-cuda-test --exit"

# RUN stable-diffusion-webui/webui.sh ${CLI_ARGS}

# RUN sed -i -e 's/print('Not launching API server for now')/webui.api_only()/g' stable-diffusion-webui/launch.py


# scripts
ADD --chown=user https://raw.githubusercontent.com/camenduru/stable-diffusion-webui-scripts/main/run_n_times.py stable-diffusion-webui/scripts/run_n_times.py

# extensions
RUN git clone -b v2.0 https://github.com/camenduru/sd-civitai-browser stable-diffusion-webui/extensions/sd-civitai-browser
RUN git clone https://github.com/camenduru/stable-diffusion-webui-huggingface stable-diffusion-webui/extensions/stable-diffusion-webui-huggingface
RUN git clone https://github.com/camenduru/openpose-editor stable-diffusion-webui/extensions/openpose-editor
RUN git clone https://github.com/camenduru/sd-webui-tunnels stable-diffusion-webui/extensions/sd-webui-tunnels
RUN git clone https://github.com/deforum-art/deforum-for-automatic1111-webui stable-diffusion-webui/extensions/deforum-for-automatic1111-webui
RUN git clone https://github.com/AlUlkesh/stable-diffusion-webui-images-browser stable-diffusion-webui/extensions/stable-diffusion-webui-images-browser
RUN git clone https://github.com/kohya-ss/sd-webui-additional-networks stable-diffusion-webui/extensions/sd-webui-additional-networks
RUN git clone https://github.com/jexom/sd-webui-depth-lib stable-diffusion-webui/extensions/sd-webui-depth-lib
RUN git clone https://github.com/hnmr293/posex stable-diffusion-webui/extensions/posex
RUN git clone https://github.com/etherealxx/batchlinks-webui stable-diffusion-webui/extensions/batchlinks-webui
RUN git clone https://github.com/Mikubill/sd-webui-controlnet stable-diffusion-webui/extensions/sd-webui-controlnet
# ADD --chown=user https://huggingface.co/ckpt/ControlNet/resolve/main/control_canny-fp16.safetensors stable-diffusion-webui/extensions/sd-webui-controlnet/models/control_canny-fp16.safetensors
# ADD --chown=user https://huggingface.co/ckpt/ControlNet/resolve/main/control_depth-fp16.safetensors stable-diffusion-webui/extensions/sd-webui-controlnet/models/control_depth-fp16.safetensors
# ADD --chown=user https://huggingface.co/ckpt/ControlNet/resolve/main/control_hed-fp16.safetensors stable-diffusion-webui/extensions/sd-webui-controlnet/models/control_hed-fp16.safetensors
# ADD --chown=user https://huggingface.co/ckpt/ControlNet/resolve/main/control_mlsd-fp16.safetensors stable-diffusion-webui/extensions/sd-webui-controlnet/models/control_mlsd-fp16.safetensors
# ADD --chown=user https://huggingface.co/ckpt/ControlNet/resolve/main/control_normal-fp16.safetensors stable-diffusion-webui/extensions/sd-webui-controlnet/models/control_normal-fp16.safetensors
# ADD --chown=user https://huggingface.co/ckpt/ControlNet/resolve/main/control_openpose-fp16.safetensors stable-diffusion-webui/extensions/sd-webui-controlnet/models/control_openpose-fp16.safetensors
# ADD --chown=user https://huggingface.co/ckpt/ControlNet/resolve/main/control_scribble-fp16.safetensors stable-diffusion-webui/extensions/sd-webui-controlnet/models/control_scribble-fp16.safetensors
# ADD --chown=user https://huggingface.co/ckpt/ControlNet/resolve/main/control_seg-fp16.safetensors stable-diffusion-webui/extensions/sd-webui-controlnet/models/control_seg-fp16.safetensors
ADD --chown=user https://huggingface.co/ckpt/ControlNet/resolve/main/hand_pose_model.pth stable-diffusion-webui/extensions/sd-webui-controlnet/annotator/openpose/hand_pose_model.pth
ADD --chown=user https://huggingface.co/ckpt/ControlNet/resolve/main/body_pose_model.pth stable-diffusion-webui/extensions/sd-webui-controlnet/annotator/openpose/body_pose_model.pth
ADD --chown=user https://huggingface.co/ckpt/ControlNet/resolve/main/dpt_hybrid-midas-501f0c75.pt stable-diffusion-webui/extensions/sd-webui-controlnet/annotator/midas/dpt_hybrid-midas-501f0c75.pt
ADD --chown=user https://huggingface.co/ckpt/ControlNet/resolve/main/mlsd_large_512_fp32.pth stable-diffusion-webui/extensions/sd-webui-controlnet/annotator/mlsd/mlsd_large_512_fp32.pth
ADD --chown=user https://huggingface.co/ckpt/ControlNet/resolve/main/mlsd_tiny_512_fp32.pth stable-diffusion-webui/extensions/sd-webui-controlnet/annotator/mlsd/mlsd_tiny_512_fp32.pth
ADD --chown=user https://huggingface.co/ckpt/ControlNet/resolve/main/network-bsds500.pth stable-diffusion-webui/extensions/sd-webui-controlnet/annotator/hed/network-bsds500.pth
ADD --chown=user https://huggingface.co/ckpt/ControlNet/resolve/main/upernet_global_small.pth stable-diffusion-webui/extensions/sd-webui-controlnet/annotator/uniformer/upernet_global_small.pth
ADD --chown=user https://huggingface.co/ckpt/ControlNet/resolve/main/t2iadapter_style_sd14v1.pth stable-diffusion-webui/extensions/sd-webui-controlnet/models/t2iadapter_style_sd14v1.pth
ADD --chown=user https://huggingface.co/ckpt/ControlNet/resolve/main/t2iadapter_sketch_sd14v1.pth stable-diffusion-webui/extensions/sd-webui-controlnet/models/t2iadapter_sketch_sd14v1.pth
ADD --chown=user https://huggingface.co/ckpt/ControlNet/resolve/main/t2iadapter_seg_sd14v1.pth stable-diffusion-webui/extensions/sd-webui-controlnet/models/t2iadapter_seg_sd14v1.pth
ADD --chown=user https://huggingface.co/ckpt/ControlNet/resolve/main/t2iadapter_openpose_sd14v1.pth stable-diffusion-webui/extensions/sd-webui-controlnet/models/t2iadapter_openpose_sd14v1.pth
ADD --chown=user https://huggingface.co/ckpt/ControlNet/resolve/main/t2iadapter_keypose_sd14v1.pth stable-diffusion-webui/extensions/sd-webui-controlnet/models/t2iadapter_keypose_sd14v1.pth
ADD --chown=user https://huggingface.co/ckpt/ControlNet/resolve/main/t2iadapter_depth_sd14v1.pth stable-diffusion-webui/extensions/sd-webui-controlnet/models/t2iadapter_depth_sd14v1.pth
ADD --chown=user https://huggingface.co/ckpt/ControlNet/resolve/main/t2iadapter_color_sd14v1.pth stable-diffusion-webui/extensions/sd-webui-controlnet/models/t2iadapter_color_sd14v1.pth
ADD --chown=user https://huggingface.co/ckpt/ControlNet/resolve/main/t2iadapter_canny_sd14v1.pth stable-diffusion-webui/extensions/sd-webui-controlnet/models/t2iadapter_canny_sd14v1.pth
RUN git clone -b dev https://github.com/d8ahazard/sd_dreambooth_extension stable-diffusion-webui/extensions/sd_dreambooth_extension

# # models
# # ADD --chown=user https://huggingface.co/runwayml/stable-diffusion-v1-5/resolve/main/v1-5-pruned-emaonly.ckpt  stable-diffusion-webui/models/StableDiffusion/v1-5-pruned-emaonly.ckpt
# # ADD --chown=user https://huggingface.co/runwayml/stable-diffusion-inpainting/resolve/main/sd-v1-5-inpainting.ckpt  stable-diffusion-webui/models/StableDiffusion/sd-v1-5-inpainting.ckpt
# ADD --chown=user https://huggingface.co/stabilityai/sd-vae-ft-mse-original/resolve/main/vae-ft-mse-840000-ema-pruned.ckpt  stable-diffusion-webui/models/VAE/vae-ft-mse-840000-ema-pruned.ckpt
# ADD --chown=user https://github.com/TencentARC/GFPGAN/releases/download/v1.3.4/GFPGANv1.4.pth  stable-diffusion-webui/models/GFPGAN/GFPGANv1.4.pth
# ADD --chown=user https://github.com/xinntao/Real-ESRGAN/releases/download/v0.1.0/RealESRGAN_x4plus.pth  stable-diffusion-webui/models/RealESRGAN/RealESRGAN_x4plus.pth
# ADD --chown=user https://github.com/xinntao/Real-ESRGAN/releases/download/v0.2.2.4/RealESRGAN_x4plus_anime_6B.pth  stable-diffusion-webui/models/RealESRGAN/RealESRGAN_x4plus_anime_6B.pth
# ADD --chown=user https://heibox.uni-heidelberg.de/f/31a76b13ea27482981b4/?dl=1  stable-diffusion-webui/models/LDSR/project.yaml
# # ADD --chown=user https://heibox.uni-heidelberg.de/f/578df07c8fc04ffbadf3/?dl=1  stable-diffusion-webui/models/LDSR/model.ckpt



RUN stable-diffusion-webui/webui.sh ${CLI_ARGS}


# avoid all ADDs
FROM base as run

RUN ln -s /home/user/stable-diffusion-webui/venv/lib/python3.10/site-packages/bitsandbytes/libbitsandbytes_cpu.so /home/user/stable-diffusion-webui/venv/lib/python3.10/site-packages/bitsandbytes/libsbitsandbytes_cpu.so


# create inputs/outputs folders
RUN mkdir -vp \
    stable-diffusion-webui/inputs \ 
    stable-diffusion-webui/outputs 

EXPOSE 7860

# ENV CLI_ARGS="--skip-torch-cuda-test --listen --no-half --precision full --allow-code --enable-insecure-extension-access --api"
# ENV CLI_ARGS="--skip-torch-cuda-test --listen --no-half --enable-insecure-extension-access"
ENV CLI_ARGS="--skip-torch-cuda-test --listen --no-half --enable-insecure-extension-access --force-cpu"

USER root

CMD chown -R :user stable-diffusion-webui/models && \
    chmod -R g+w stable-diffusion-webui/models && \ 
    chown -R :user stable-diffusion-webui/inputs && \ 
    chmod -R g+w stable-diffusion-webui/inputs && \ 
    chown -R :user stable-diffusion-webui/outputs && \ 
    chmod -R g+w stable-diffusion-webui/outputs && \ 
    su user -c "stable-diffusion-webui/webui.sh ${CLI_ARGS}"


# CMD stable-diffusion-webui/webui.sh ${CLI_ARGS}


