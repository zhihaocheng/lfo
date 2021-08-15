# Learning from Observation (LfO)

This repository provides the implementation of GAIfO in the paper---On the Guaranteed Almost Equivalence between Imitation Learning from Observation and Demonstration. Our code is mainly based on [OpenAI Baselines](https://github.com/openai/baselines).   

## Requirements

Our code follows the framework of [OpenAI Baselines](https://github.com/openai/baselines), so you need to install [OpenAI Baselines](https://github.com/openai/baselines) at first following the instructions [here](https://github.com/openai/baselines). 

> NOTE: All of our experiments use [MuJoCo](http://www.mujoco.org) (multi-joint dynamics in contact) physics simulator, so the installation of MuJoCo is necessary. Instructions on setting up MuJoCo can be found [here](https://github.com/openai/mujoco-py).

After the successful installations of [OpenAI Baselines](https://github.com/openai/baselines) and [MuJoCo](http://www.mujoco.org), copy the folder `./gaifo` into `baselines/baselines/`.

## Training

### Step 1: Prepare the expert data
Download the expert data [here](https://drive.google.com/drive/folders/1C4bsf62XbHW36F9gEJPGhrOZ1Ij4Upco?usp=sharing). Then copy the expert data `./expert_data/Hopper-v2.npz` into the folder `baselines/data`.

### Step 2: Set the output path for log file
The variable OPENAI_LOGDIR specifies the path to save the log file. The progress.csv which monitors the training process will be stored in this path.  
```bash
export OPENAI_LOGDIR=path_to_save_log_file
```

### Step 3: Run GAIfO

Run with single rank:

```bash
python -m baselines.gaifo.run_mujoco
```

Run with multiple ranks:

```bash
mpirun -np 8 python -m baselines.gaifo.run_mujoco
```

A complete example of training GAIfO for Hopper-v2 is given as follows:

```bash
mpirun -np 8 python -m baselines.gaifo.run_mujoco --env_id=Hopper-v2 --expert_path data/Hopper-v2.npz --traj_limitation 20 --seed=0 --g_step=3 --d_step=1 --num_timesteps=5000000
```

See help (`-h`) for more options.


## Citation

If you find this repository or our paper useful, please cite it in your publications.

```latex
@ARTICLE{9509344,
  author={Cheng, Zhihao and Liu, Liu and Liu, Aishan and Sun, Hao and Fang, Meng and Tao, Dacheng},
  journal={IEEE Transactions on Neural Networks and Learning Systems}, 
  title={On the Guaranteed Almost Equivalence Between Imitation Learning From Observation and Demonstration}, 
  year={2021},
  volume={},
  number={},
  pages={1-13},
  doi={10.1109/TNNLS.2021.3099621}
}
```

## Others

Thanks to the open source:

- @openai/baselines

## Contributing
The MIT License


