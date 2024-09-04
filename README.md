#

## Environment settings and libraries we used in our experiments

This project is tested under the following environment settings:

- OS: Ubuntu 20.04.3
- GPU: NVIDIA A100
- Cuda: 11.1, Cudnn: v8.2
- Python: 3.9.5
- PyTorch: 1.8.0
- Torchvision: 0.9.0

## Requirements

- Install or download [AutoAttack](https://github.com/fra31/auto-attack):

```.bash
pip install git+https://github.com/fra31/auto-attack
```

- Install or download [RandAugment](https://github.com/ildoonet/pytorch-randaugment):

```.bash
pip install git+https://github.com/ildoonet/pytorch-randaugment
```

## Training Commands

```.bash
python train-wa.py --data-dir 'dataset-data' \
    --log-dir 'trained_models' \
    --desc 'WRN28-10Swish_cifar10s_lr0p2_TRADES5_epoch400_bs512_fraction0p7_ls0p1' \
    --data cifar10s \
    --batch-size 512 \
    --model wrn-28-10-swish \
    --num-adv-epochs 400 \
    --lr 0.2 \
    --beta 5.0 \
    --unsup-fraction 0.7 \
    --aux-data-filename 'edm_data/cifar10/1m.npz' \
    --ls 0.1
```

## Evaluation Commands

```.bash
python eval-aa.py --data-dir 'dataset-data' \
    --log-dir 'trained_models' \
    --desc 'WRN28-10Swish_cifar10s_lr0p2_TRADES5_epoch400_bs512_fraction0p7_ls0p1'
```

To evaluate the model on last epoch under AutoAttack, run the command:

```.bash
python eval-last-aa.py --data-dir 'dataset-data' \
    --log-dir 'trained_models' \
    --desc 'WRN28-10Swish_cifar10s_lr0p2_TRADES5_epoch400_bs512_fraction0p7_ls0p1'
```

For evaluation under AutoAttack:

1. Download `checkpoint` to `trained_models/mymodel/weights-best.pt`
2. Download `argtxt` to `trained_models/mymodel/args.txt`
3. Run the command:

```.bash
python eval-aa.py --data-dir 'dataset-data' --log-dir 'trained_models' --desc 'mymodel'
```

# Improve-adversarial_training
