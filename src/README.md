## Demo code

The files 
 - convert-torchvision-to-d2.py
 - convert_vissl_to_detectron2.py
 - run_distributed_engines.py

are copied from the Detectron 2 and VISSL installation folders for convenience.

The pretrained models are downloaded automatically from the Meta/PyTorch model zoo. 

## Run

Launch a ``jupyter lab`` server and load up the ``detectron_vissl_2.ipynb``

Run the notebook just to do a sanity check of the instalation (eg paths are Ok, all the dependencies are installed, etc)
and then beef up the ``SSL_large_iter_count`` and/or ``D2_iter_count`` values to get more train iterations.

Feel free to tweak with number of images per batch size. For a 6Gb VRAM card (GTX 980Ti) a value of 4 is decent.

The code "frees" the memory after each model evaluation, saving the checkpoints and training statistics.

## Platform

Tested on one configuration with Ubuntu 20, with a fairly old GPU.

Good luck!