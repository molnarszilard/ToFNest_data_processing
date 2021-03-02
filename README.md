# ToFNest_data_processing
This repository is an extension for the ToFNest method https://github.com/molnarszilard/ToFNest.
It contains scripts that helps you to create dataset and to evaluate the performance of the method.

You might need to have PointCloudLibrary and opencv installed.

mkdir build
cd build
cmake ..
make

## Dataset preparation

After you have obtained your depth images, and they are inside path/to/dataset/depth go into bash_files/ and run:

bash create_dataset.sh path/to/dataset/ path/to/build/

Initially the normals are computed using PCLNormals, but you can use your own preferred version (just modify the code accordingly).
The data for training will be stored in depth3/ and in normalimages/ as the ground truth.

## Data augmentation
If you want to apply some augmentations on your depth images run:
python3 augmentation.py --dir=path/to/dataset/depth/
And run the Dataset preparation for your augmented data.

## Add noise to your data

By running 

bash addnoise.sh path/to/dataset/ path/to/build/

you can add noise to your depth images. (if you want to set the noise level, modify the src/addnoise2depth.cpp file), and then run the code, from Dataset preparation (note you might want to calculate your the normals for your data without noise, and in this case it is enough to create the depth3 images, be sure that all the names are correct)

### Verify the model
If you have created your normaimages (they should look like something like this: 00000_pred.png), copy them to path/to/dataset/predictions/

run
bash depth2pcd_normal.sh path/to/dataset/ path/to/build/
bash normal_performance.sh

in path/to/build/histogram.txt you can find the histogram about your model
in path/to/dataset/pcdpred_delta/ there are the pointclouds that show you which part of the pcd was predicted correctly or not.
