# Deep-Hiding-in-3D-Photography
Deep Hiding in 3D Photography
Created by [Hang Zhou](http://home.ustc.edu.cn/~zh2991/), [Dongdong Chen](http://www.dongdongchen.bid/), [Jing Liao](https://liaojing.github.io/html/), [Kejiang Chen](http://home.ustc.edu.cn/~chenkj/), [Weiming Zhang](http://staff.ustc.edu.cn/~zhangwm/index.html).

Introduction
--
We propose a general framework to synthesize the primitives of 3D photography into one single photo based on an image encoding architecture. Specifically, before 3D rendering, we regress these primitives using the image decoding architecture. With the encoding and decoding networks, we are able to prepare these essential components for 3D photography, and thus the resulting 3D photos can be rendered with high visual quality. 

Visualization
--
<a href="http://home.ustc.edu.cn/~zh2991/21TVCG_3DDeepHiding/test1_proposed.mp4" rel="Video"><img src="http://home.ustc.edu.cn/~zh2991/21TVCG_3DDeepHiding/test1_proposed.png" alt="Video" width="100%"></a>



Installation
--
This repository is based on Python 3.6, TensorFlow 1.8.0, CUDA 9.0 and cuDNN 7 on Ubuntu 18.04.

1. Set up a virtual environments using conda for the Anaconda Python distribution.

   ```shell
   conda create -n LGGAN python=3.6 anaconda
   ```

2. Install tensorflow-gpu.

   ```shell
   pip install tensorflow-gpu==1.8.0
   ```

3. While `nvcc` from CUDA needs to compile TF operators, install CUDA from CUDA Source Packages. 
   After downloading, implement

   ```shell
   bash cuda_9.0.176_384.81_linux.run --tmpdir=/tmp --override
   ```

   Note that the installation directory is set to `/xxx/cuda-9.0`

4. For compiling TF operators, please check `tf_xxx_compile.sh` under each op subfolder in `tf_ops` folder. Note that you need to update `nvcc`, `python` and `tensoflow` include library if necessary. 

5. Install other packages.

   ```shell
   pip install h5py
   pip install Pillow
   pip install matplotlib
   ```

6. Point clouds of the ModelNet40 data in HDF5 files are downloaded and unzipped to the `data` folder. 

   ```shell
   wget -c https://shapenet.cs.stanford.edu/media/modelnet40_ply_hdf5_2048.zip
   unzip modelnet40_ply_hdf5_2048.zip
   ```

7. Download the pretrained PointNet model from [GoogleDrive](https://drive.google.com/drive/folders/11c6v_umZmSHiq-1TLKpSyPQK0E9fDkMU), extract it and put it in folder `checkpoints/pointnet/`. 

8. Download [neural_toolbox](https://github.com/GuessWhatGame/neural_toolbox), extract it and put it in folder `LG-GAN`. 

Usage
--

1. Activate LG-GAN environment.

   ```shell
   source activate LGGAN
   ```

2. Set LD_LIBRARY_PATH.

   ```shell
   export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/xxx/cuda-9.0/lib64
   ```

3. Run:

   ```shell
   srun python -u lggan.py --adv_path LGGAN --checkpoints_path LGGAN --log_path LGGAN --tau 1e2
   srun python -u lggan_single.py --adv_path LGGAN_s --checkpoints_path LGGAN_s --log_path LGGAN_s --tau 1e2
   srun python -u lg.py --adv_path LG --checkpoints_path LG --log_path LG --tau 1e2
   ```

