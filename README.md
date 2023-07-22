# Material for the OHBM 2023 Educational Course Tutorial "Hands (and sensors!) on: a practical guide to acquiring your own physiological data"
This repository contains installation materials, data, and code for the tutorial "Hands (and sensors!) on: a practical guide to acquiring your own physiological data"  at the OHBM 2023 Educational Course "Physiologic fMRI signals: friend or foe? How and why to measure, model, and account for physiology". You can find links to other tutorials in this course [here](https://physiopy.github.io/ohbm23_tutorials/).

Thank you to Stefano Moia for help in preparing the installation instructions for this tutorial! You can also find more comprehensive documentation for installing phys2bids [here](https://phys2bids.readthedocs.io/en/latest/installation.html).

## Laptop set-up
To follow this tutorial, you will need a laptop, requiring a little bit of setup beforehand.

### To start: set up your own installation!

#### 0. Prerequisites
You will need a laptop with python installed, as well as pip. Python version should be 3.7 or above. You also need to download the files in this repository, either zipped in a package or by locally cloning the repository.

#### 1. Virtual environment
The best way to ensure the software will function without changing anything in your system is using a virtual environment. For that, first install virtualenv::

```
pip install -U virtualenv
```

(Note you might need to use pip3 instead of pip, depending on your OS and setup, to work with python 3)

Then, create and activate the virtual environment - in this case I called it OHBM2023phys2bids, but you can use a different name:

```
virtualenv OHBM2023phys2bids
source OHBM2023phys2bids/bin/activate
```

Note that the first command above will create a folder where you called it from, and the second command assumes this is the case - if you want you can specify a different path though.

Once you activated the virtual environment, you can proceed with package installation.

#### 2. Package installation
To install the phys2bids software for this tutorial, you should run the following command:

```
pip install phys2bids[acq]
```

Here, `[acq]` specifies that we are also installing the `bioread` module, which adds support for loading `.acq` files.


#### 3. Check your installation
Run:

```
phys2bids -v
```
I am running 'phys2bids 2.10.0' for this tutorial!

### 4. Get to know phys2bids

You can find all the information you need to interact with phys2bids from the commandline by running:

```
phys2bids -h
```
or
```
phys2bids --help
```

### Let's deal with some data!

#### Load in the first dataset and take a look.

```
phys2bids -in samefreq_multiscan.txt -out multiscan_info -info
```

#### Let's split the dataset into its functional scans!
```
phys2bids -in samefreq_multiscan.txt -out multiscan_split -ntp 534 513 -tr 1.2
```

#### Next, let's go all the way and bids-ify the data using the heuristic file!
```
phys2bids -in samefreq_multiscan.txt -out multiscan_bids -ntp 534 513 -tr 1.2 -sub 001 -ses 01 -heur heur_tutorial.py
```


