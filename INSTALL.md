Make sure that you have anaconda installed. You can verify this by running the following command in your terminal or command prompt:

```bash
conda --version
```

- If the command outputs a version number (e.g., conda 23.x.x), Anaconda is installed.
- If the command is not recognized or an error appears, Anaconda may not be installed.

Check that "(base)" appears before your user in the terminal. If not, initialize conda with `conda init` and restart your terminal. Now it should appear.

Create conda environment. To run this code it is necessary to install Python 3.7 version.

```bash
conda create --name MEGA -y python=3.7
```

Activate conda environment

```bash
conda activate MEGA
```

Install the right pip and dependencies for the fresh python (ipython and pip)

```bash
conda install ipython pip
```

Type enter ("yes" option by default) to proceed with the installation of the new packages

Install mega and coco api dependencies

```bash
pip install ninja yacs cython matplotlib tqdm opencv-python scipy
```

Install pytorch and torchvision for CUDA 10.0 (instructions in https://pytorch.org/get-started/previous-versions/#conda-31)

```bash
conda install pytorch==1.2.0 torchvision==0.4.0 cudatoolkit=10.0 -c pytorch
```

Type enter ("yes" option by default) to proceed with the installation of the new packages

```bash
export INSTALL_DIR=$PWD
```

Install pycocotools

```bash
cd $INSTALL_DIR
git clone https://github.com/cocodataset/cocoapi.git
cd cocoapi/PythonAPI
python setup.py build_ext install
```

Install cityscapesScripts

```bash
cd $INSTALL_DIR
git clone https://github.com/mcordts/cityscapesScripts.git
cd cityscapesScripts/
python setup.py build_ext install
```

Install apex

```bash
cd $INSTALL_DIR
git clone https://github.com/NVIDIA/apex.git
cd apex
```

Go to /apex/apex/contrib/test/optimizers/test_dist_adam.py, search for "self.world_size=" and change it to "self.world_size". Save the changes.

```bash
python setup.py build_ext install
```

Install PyTorch Detection

```bash
cd $INSTALL_DIR
git clone https://github.com/Scalsol/mega.pytorch.git
cd mega.pytorch
```

The following will install the lib with symbolic links, so that you can modify the files if you want and won't need to re-build it

```bash
python setup.py build develop
```

```bash
pip install 'pillow<7.0.0'
```

```bash
unset INSTALL_DIR
```

Create a "visualization" folder to store the results. You can do it by running the following command in your terminal or command prompt:

```bash
mkdir visualization
```

From the root folder of https://github.com/Scalsol/mega.pytorch, go to ‘Main Results’ section, download ‘singleframe baseline’ and ‘MEGA’ model checkpoints (backbone ResNet-101) and place them in the ‘mega.pytorch’ folder.

Change cloning to my repositories to avoid apex and opencv errors:

There are some errors in the cloned repositories that have to be changed in order to run the demo:

    - Go to /mega.pytorch/mega_core/layers/nms.py, comment line 5 (import) and remove amp.float_function function (leave the _C.nms)

    - Go to /mega.pytorch/mega_core/layers/roi_pool.py and comment lines 10 and 56

    - Go to /mega.pytorch/mega_core/layers/roi_pool.py and comment lines 10 and 57

    - Go to /mega.pytorch/demo/predictor.py

Follow the instructions detailed on demo/README.md to run the demo code using both BASE and MEGA approaches. Use the “Inference on image folder” mode with the example.

