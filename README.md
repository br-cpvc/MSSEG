![Logo](https://github.com/sergivalverde/MSSEG/blob/master/logo.png)

# MSSEG: Multiple Sclerosis brain tissue SEGmentation method for MR patient images

Over the last few years, the increasing interest in brain tissue volume measurements on clinical settings has lead to the development of a wide number of automated tissue segmentation methods. However, white matter lesions are known to reduce the accuracy of automated tissue segmentation methods, which requires manual annotation of the lesions and refilling them before segmentation, which is tedious and time-consuming. __MSSEG__ is  a new, fully automated T1-w/FLAIR tissue segmentation approach designed to deal with images in the presence of WM lesions. This approach integrates a robust partial volume tissue segmentation with WM outlier rejection and filling, combining intensity and probabilistic and morphological prior maps.

# Dependencies:
+ So far, the method only runs on GNU/Linux 64 bits if [NiftyReg](http://cmictig.cs.ucl.ac.uk/wiki/index.php/NiftyReg) is not installed in the host system. If NiftyReg is installed in your system, just change the path to the NiftyReg binaries in `register_prior.m` function.

+ This software uses the [Computer Vision System Toolbox for MATLAB](http://es.mathworks.com/products/computer-vision/).


# How to use MSSEG:

This is a simple example showing how to run the method. First, the paths of the T1-w, FLAIR and the brainmask images have to be provided:

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
# Available options:

In general, all the available options in the software are set to values that are known to work well in most of the cases. However, each of these can be tuned in the `options` variable passed as an input:

+`options.prior`:  The prior variable controls the amount of prior probability information used by the membership functions  (default 0.025)

+`options.weighting`: Fuzzy factor exponent in Fuzzy C-means clustering (default 2)

+`options.maxiter`: Number of maximum iterations during energy minimization FCM (default 200)

+`options.num_neigh`: Radius of the neighborhood used in spatial contraint (default 1)

+`options.dim`: Dimension of the neighborhood (default 2)

+`options.term`:  Minimum error in energy minimization to stop (default 1E-3)

+`options.gpu`: Use GPU (default 0)

+`options.alpha`:  This parameter regulates the minimum intensity considered in FLAIR candidates (default 3)

+`options.info`:  Show information during tissue segmentation (default 0)

+`options.debug`:  Save registered and intermediate files (default 0)


[NeuroImage Computing Group](http://atc.udg.edu/nic/research.html), VICOROB [Vision and Robotics Institute](vicorob.udg.edu), University of Girona.
