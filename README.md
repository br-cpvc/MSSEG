![Logo](https://github.com/sergivalverde/MSSEG/blob/master/logo.png)

# MSSEG: Multiple Sclerosis brain tissue SEGmentation method for MR patient images

Over the last few years, the increasing interest in brain tissue volume measurements on clinical settings has lead to the development of a wide number of automated tissue segmentation methods. However, white matter lesions are known to reduce the accuracy of automated tissue segmentation methods, which requires manual annotation of the lesions and refilling them before segmentation, which is tedious and time-consuming. __MSSEG__ is  a new, fully automated T1-w/FLAIR tissue segmentation approach designed to deal with images in the presence of WM lesions. This approach integrates a robust partial volume tissue segmentation with WM outlier rejection and filling, combining intensity and probabilistic and morphological prior maps.
a


# How to use it:

This is a simple example which shows how to run the method. First, the paths of the T1-w, FLAIR and the brainmask images have to be provided:

```
t1_path = 'examples/T1';
brainmask_path = 'examples/brainMask';
flair_path = 'examples/T2_FLAIR';
```
Note that the image paths are passed without the extensions. Images can be both NIFTI or NIFTI.gz. Then, the options are set. In this case, we just adjust the method to run with the GPU, and we select the ```options.debug``` to also save all the intermediate files.

```
options.gpu = 1;          % use gpu
options.debug = 1;        % save intermediate files.
```
Finally, the `msseg` method is invoked using this command:

```
[segmentation, seg_pve] = msseg(t1_path, brainmask_path, flair_path, options);
```
Similarly, the method can be also run using only the T1-w modality as follows:

```
[segmentation, seg_pve] = msseg(t1_path, brainmask_path, flair_path, options);
```

#Known limitations:
+ So far, the method only runs on Linux 64 bits. 

[NeuroImage Computing Group](http://atc.udg.edu/nic/research.html), VICOROB [Vision and Robotics Institute](vicorob.udg.edu), University of Girona.
