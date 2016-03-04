# How to run this branch

This branch was created as standard. Using the input scripts as follows [here](http://visor.udg.edu/gitvicorob/svalverde/msseg/blob/msseg_with_bet/MSSEG/tests/test_SALEM.m)

## How I run the experiments?

Set the general options for the dataset:

``` 
%image_folder{1} = '/home/s/w/ALFI/images/MRBRAINS13/training_w_skull';
image_folder{1} = '/home/s/w/ALFI/images/MRBRAINS13/TestData';
%image_folder{1} = '/home/s/w/ALFI/images/SALEM';
```

Set the experiment name and characterisitics of both the input images and the brainmask. The input brainmask is the results of voting the voxels of the 5 registered training masks.


```
experiment = 'w_FLAIR_reg_atlas';
%experiment = 'w_T1_reg_atlas';
scan_type = 'T1';
options.name = experiment;
run_segmentation =1;
run_evaluation = 1;
```


Tissue segmentation options:


```
%% TISSUE SEGMENTATION OPTIONS

% load options
options.c = 5;                 % number of classes
options.weighting = 2;         % Weighting exponent
% Max. iteration
options.num_neigh = 1;         % Number of neighbors used in the penalized function.
options.dim = 2;           % Dimension of the neiborghood
options.beta = 0.1;        % Beta parameter
% Termination threshold
options.gpu = 1;         % use gpu
options.info = 1;         % Display info or not
options.prior = 0.025;        % prior information ratio
options.force_reg = 0;        % force registration even if it exists a previous file
options.alpha = 3;

```

Then, the script ```tissue_segmentation```is used as follows:

```
execution_time = zeros(size(num_of_scans));
if run_segmentation 
for s= 1:num_of_scans
	current_scan = scan_name{s};
	current_folder = scan_folder{s};
	disp(['Scan number: ', current_scan, ' *********************']);
	FLAIR = fullfile(current_folder, 'T2_FLAIR');	
	T1 = fullfile(current_folder, scan_type);
	brainmask = T1;
	tic;
	[segmentation, seg_pve] = tissue_segmentation(T1, options, brainmask, FLAIR);
	execution_time(s) = toc;
end
end
```



