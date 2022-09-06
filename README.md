# Demo on how to train a Detectron2 segmentation model (R-CNN) on top of a model that was trained with VISSL 

Wonder how to combine the Self-Supervised Learning approach with classical and proven Detectron2 segmentation? Here is how.

## Dataset
Download balloons dataset into the balloon folder.

Direct link https://github.com/matterport/Mask_RCNN/releases/download/v2.1/balloon_dataset.zip from https://github.com/matterport/Mask_RCNN/releases

The content of the folder should be:

    balloon/
        val/
            ...
        train/
            ...
        readme.txt

## Install VISSL

[Install VISSL from source](https://github.com/facebookresearch/vissl/blob/main/INSTALL.md#installing-vissl-from-source-recommended)

    conda create --copy -n ssl_d2 -c pytorch python=3.8 pytorch torchvision torchaudio cudatoolkit=10.2
    conda activate ssl_d2
    
Install APEX from NVIDIA. The installation instructions from vissl webpage works for older pytorch versions.

    git clone https://github.com/NVIDIA/apex
    cd apex
    pip install -v --disable-pip-version-check --no-cache-dir ./


Sanity check if CUDA is available:

    python -c 'import torch;print(torch.cuda.is_available())'

Should print True

Clone vissl repo somewhere, code right here is on 0.1.6 release.

    git clone --recursive https://github.com/facebookresearch/vissl.git && cd $HOME/vissl/
    cd vissl
    git checkout v0.1.6
    git checkout -b v0.1.6

Install additional tools, as listed in 0.1.6 release instructions [copied here for convenience]

    # install vissl dependencies
    pip install --progress-bar off -r requirements.txt
    pip install opencv-python
    # update classy vision install to commit stable for vissl.
    # Note: If building from vissl main, use classyvision main.
    pip uninstall -y classy_vision
    pip install classy-vision@https://github.com/facebookresearch/ClassyVision/tarball/4785d5ee19d3bcedd5b28c1eb51ea1f59188b54d
    # update fairscale install to commit stable for vissl.
    pip uninstall -y fairscale
    pip install fairscale==0.4.6
    # install vissl dev mode (e stands for editable)
    pip install -e ".[dev]"
    # verify installation
    python -c 'import vissl, apex'

Last command should work without errors. 

## Install Detectron 2

Follow the instructions here: https://detectron2.readthedocs.io/en/latest/tutorials/install.html#build-detectron2-from-source

I installed it from commit 717ab9f0aeca216a2f800e43d705766251ba3a55

There should be some errors regarding fvcore and hydra-core. Well . . .

## Install other tools

Now, install some additional tools like jupyterlab 

    conda install jupyterlab ipympl