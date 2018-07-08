# DIGICAM - Udacity Deep Learning Project(Live Camera App)

In this project I build an android application that will recognize numbers using the cameras image stream from the device.

Here you will find a report, a number of jupyter notebooks for data processing and analysis as well as the code to build the classifier and android app.

# Report
- [DIGICAM-report.pdf](DIGICAM%20report.pdf)

# Metrics
In order to find the classifier that predicts the best, we will need to define a way to compare them. For this we  will use the mean accuracy of digits predicted correctly. 
 
For example if the classifier predicts 123 and the correct label is 120, the accuracy for this would be ⅔, as the  digits 1 and 2 are correct and in the correct location, but the 0 is incorrect.  
 
Another example predicts 12, and the correct label is 312, then the accuracy will be 0/3 as no digits are correct  in the correct place. 
 
The final score will be the accuracy averaged across the number of items in the batch

#Deciding the architecture
The architure has been decided by training the synthetic dataset (NOTMNIST) at https://github.com/cnavneet/notMNIST

# Notebooks

- [01 - Explore and preprocess images.ipynb](01 - Explore and preprocess images.ipynb)
- [02 - train, test and score.ipynb](02 - Minimal train, test and score.ipynb)
- [03 - Results processing.ipynb](03 - Results processing.ipynb)
- [04 - Investigate convolutional weights.ipynb](04 - Investigate convolutional weights.ipynb)

# Build classifier and android application
To build this project there are 2 major steps...

#### 1. Building the classifier
 - Attain and preprocess data
 - Run hyperparameter search
 
#### 2. Creating the android application
 - Freeze tensorflow model
 - Build and install android app
    

# Building the classifier
### Requirements

- anaconda2 installation for python 3.x
- tensorflow python libraries

### Steps
#### 1. Attain and preprocess data
- Download the [train](http://ufldl.stanford.edu/housenumbers/train.tar.gz) data and extract into a folder called **train**
- Download the [test](http://ufldl.stanford.edu/housenumbers/test.tar.gz) data and extract into a folder called **test**
- Open the notebook **01 - Explore and preprocess images.ipynb** and run all the steps to create the training and testing datasets.

#### 2. Run the hyperparameter search
- Modify and configuration for the hyper parameter search in **run_search.py**
- Run the search
```bash
python run_search.py
```
- Investigate the results file **results-xmins.csv** for the results summary, where x is the number of minutes chosen to run each graph.
- Investigate the log file in the directory **./log**. The filename is in date format **yy-mm-dd-hh-nn-ss.log**
- Investigate the saved models in the directory **./save**. The filename is in date format **yy-mm-dd-hh-nn-ss**

# Creating the android application
### Requirements
- A clone of [TensorFlow (0.9)](https://github.com/tensorflow/tensorflow)
- TensorFlow building locally. [Instructions](https://www.tensorflow.org/versions/r0.9/get_started/os_setup.html#download-and-setup)
- TensorFlow freeze_graph built. [Instructions](https://github.com/tensorflow/tensorflow/blob/master/tensorflow/python/tools/freeze_graph.py#L27)
- An android device setup to allow application installations via adb. [Instructions](https://developer.android.com/studio/command-line/adb.html)

### Steps
#### 1. Freeze tensorflow model
In order to use the model in an android app, you must freeze the weights into the model and copy this into the correct directory. To do this follow these steps,
- Select the model that you would like to use in the android application. You will need that models **save_name** as recorded in the results and log file. It will be in the format **yy-mm-dd-hh-nn-ss**
- Setup the local file **freeze_graph.sh** to point to your local version of tensorflow freeze_graph application
- Setup the local file **freeze_graph.sh** to be executable

```bash
$ chmod +x freeze_graph.sh
```

- Freeze the graph by executing the bash script. For example

```bash
$ ./freeze_graph.sh 16-08-09-22-46-55
```

- Check a file called **frozen_graph.pb** have been copiied into the **android/assets** directory.

#### 2. Build and install android app
To build and install the android app you will need to replace the tensorflow directory  **tensorflow/tensorflow/examples/android/** with the **android** directory in this repo. 
- To do this there are 2 options
 1. Option 1, copy the local android directory over the tensorflow one.
 2. Option 2, delete the android directory in tensorflow and use a symlink to the android folder in this repo.
 

- Setup your device with adb to receive the application
- Build and install the android demo as normal with these [instructions]( https://github.com/tensorflow/tensorflow/tree/master/tensorflow/examples/android), or run
```bash
$ bazel mobile-install //tensorflow/examples/android:tensorflow_demo
```
- Check your device has the applicaton **TensorFlow demo** installed.
- Have fun!!!
