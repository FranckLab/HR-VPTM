# HR-VPTM (High-Rate Volumetric Particle Tracking Microscopy): Light field microscopy-based multi-particle tracking from high-speed video

HR-VPTM is a script bundle that feeds light field microscopy (LFM) data to volumetric particle tracking (PT) for reconstructing 3D volumetric displacements and strains from LFM images of fluorescent microparticles.  

## Purpose
This repository contains the MATLAB m-files for HR-VPTM along with synthetic example images. The algorithm relies on two primary precursor code: oLaF (https://gitlab.lrz.de/IP/olaf) and SerialTrack (early development fork from https://github.com/FranckLab/SerialTrack, which in turn uses modified part2track https://github.com/Part2Track/Part2Track and TPT https://github.com/FranckLab/T-PT subfunctions).

## Running HR-VPTM

### Software Required
Development and test occurred in Matlab versions 2019a - 2021a on Windows 10. Other versions may work but have not been tested.

The following Toolboxes are dependancies: 
* 'System Identification Toolbox'
* 'Signal Processing Toolbox'
* 'Image Processing Toolbox'
* 'Statistics and Machine Learning Toolbox'
* 'Partial Differential Equation Toolbox'
* 'Wavelet Toolbox'
* 'Curve Fitting Toolbox'
* 'Parallel Computing Toolbox'
* 'MATLAB Parallel Server'
* 'Polyspace Bug Finder'

Workarounds for many of these may be possible. 

Other external tools that may be helpful include:
* inpaint_nans and inpaint_nans3d by John D'Errico (2008) (https://www.mathworks.com/matlabcentral/fileexchange?q=inpaint+nans and https://www.mathworks.com/matlabcentral/fileexchange/21214-inpainting-nan-elements-in-3-d)
* shadedErrorBar by Rod Cambell (2009) (https://www.mathworks.com/matlabcentral/fileexchange/26311-raacampbell-shadederrorbar and https://github.com/raacampbell/shadedErrorBar)
* sshist by Hideaki Shimazaki (2009) (https://www.mathworks.com/matlabcentral/fileexchange/24913-histogram-binwidth-optimization and http://2000.jukuin.keio.ac.jp/shimazaki)

In addition to several scripts and packages included in the "utils" subfolder.


### Input image requirements (data)

Images follow the basic guidelines from the oLaF software. In short: the optical configuration should be specified in a `LFMconfig.yaml` file, a `whiteImage.tif` image of a uniformly illuminated microlens array, and a sequence of one or more images to reconstruct.

* Good alignment of optics is critical for reconstruction quality. We have found LFDisplay (http://graphics.stanford.edu/software/LFDisplay/) and the WhiteImage to be handy for evaluating alignment.
* Particle size is important - we aim for a particle diameter of 5 px to 10 px.
* Particle seeding density should be a compromise between particle overlap and loss of spatial resolution due to gaps between fiducials. Fewer than around 10 particles in the field of view tend to lead to tracking errors and the code may not run. Overlapping particles tends to lead to reconstruction artifacts, increased uncertainty in centroid finding, and ghost particles.
* Background light in the image should be eliminated as much as possible, to avoid reconstruction artifacts.
* Selecting the correct reconstruction settings (volume height, microlens diameter, etc) is important.  
 
*Health warning* Reconstruction can take a *long* time (particularly for large image sequences, of course) and use a significant amount of storage (50+ GB) - be careful in choosing settings, and make sure to check a single reconstruction before running every image in a video.  


### Running including example case
1. Make sure that the main files are in the current (working) directory for MATLAB.
2. Copy the desired test images `test_images` directory as needed.
3. Run the `main_HRVPTM.m` script and follow prompts. 

*Health warning* Each reconstructed volume image is saved into the data directory alongside the .tifs in .mat containers. This can become a inconvenient amount of data to store and transfer - for the synthetic test cases each image is 1.3 GB, and the sequence for the shear experiment data totals about 81 GB.

## Cite
If used please cite:
Buyukozturk, S., Landauer, A., Summey, L. et al. High-Speed, 3D Volumetric Displacement and Strain Mapping in Soft Materials Using Light Field Microscopy. Exp Mech (2022). https://doi.org/10.1007/s11340-022-00885-z


## Contact and support
For questions, please first check the oLaF and SerialTrack papers and documentation if possible. Add a new question or bug as a GitHub "Issue" if similar issue has not been reported. The authors' contact information can be found at [Franck Lab](francklabbackup.me.wisc.edu), via GitHub, or via the associated paper.
