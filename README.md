# Telluride Spike Data Augmentation toolkit
This repository contains a pipeline of data augmentation methods, the effect of which will be tested on various data sets and SOA methods for event- and spike-based data. The goal is to reduce overfitting in learning algorithms by providing implementations of data augmentation methods for event/spike recordings.

## Quickstart
In a terminal: clone this repo and install it
```bash
git clone git@github.com:neuromorphs/spike-data-augmentation.git
cd spike-data-augmentation
pip install -e .
```

In a Python file: choose transforms and a dataset and whether you want shuffling enabled!
```python
import spike_data_augmentation
import spike_data_augmentation.transforms as transforms

transform = transforms.Compose([transforms.TimeJitter(variance=100),
                                transforms.SpatialJitter(variance_x=2, variance_y=2),
                                # mix and match!
                                ])

testset = spike_data_augmentation.datasets.NMNIST(save_to='./data',
                                                  train=False,
                                                  download=True,
                                                  transform=transform)

testloader = spike_data_augmentation.datasets.Dataloader(testset, shuffle=True)

for events, label in iter(testloader):
    print("label: " + str(label))
```

## Possible data sets (asterix marks currently supported in this package)
- [MVSEC](https://daniilidis-group.github.io/mvsec/)
- [NMNIST](https://www.garrickorchard.com/datasets/n-mnist) (\*)
- [ASL-DVS](https://github.com/PIX2NVS/NVS2Graph)
- [NCARS](https://www.prophesee.ai/dataset-n-cars/)
- [N-CALTECH 101](https://www.garrickorchard.com/datasets/n-caltech101)
- [POKER-DVS](http://www2.imse-cnm.csic.es/caviar/POKERDVS.html)
- [IBM gestures](http://www.research.ibm.com/dvsgesture/)
- [ATIS planes](https://www.westernsydney.edu.au/bens/home/reproducible_research/atis_planes)
- NTI Digits
- TIMIT

## Algorithms
- [EV-flownet](https://arxiv.org/pdf/1802.06898.pdf)
- [HOTS/HATS](http://openaccess.thecvf.com/content_cvpr_2018/papers/Sironi_HATS_Histograms_of_CVPR_2018_paper.pdf)
- [SLAYER](https://papers.nips.cc/paper/7415-slayer-spike-layer-error-reassignment-in-time.pdf)
- ContrastNet
- Sound localisation

## Install pre-commit

```
pip install pre-commit
pre-commit install
```

This will install the [black formatter](https://black.readthedocs.io/en/stable/) to a pre-commit hook. When you use ```git add``` you add files to the current commit, then when you run ```git commit``` the black formatter will run BEFORE the commit itself. If it fails the check, the black formatter will format the file and then present it to you to add it into your commit. Simply run ```git add``` on those files again and do the remainder of the commit as normal.

## Run tests

To install pytest

```
pip install pytest
```

To run the tests, from the root directory of the repo

```
python -m pytest test/
```
