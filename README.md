# nanoFeatures
_MATLAB app to characterize nanoparticles imaged with super-resolution microscopy._

__Manuscript datasets:__ https://zenodo.org/records/10610875

## Installation guide
Clone or download all files in this repository to your local folder, it contains the app file (mlapp) and the secondary scripts called from the main code, is important to keep all the files in the same local folder. Click on the “.mlapp” file and the the GUI will pop-up.
#
## Usage
In the first tab, you select the file(s) you want to analyze and the input type in the dropdown menu:

* __NIKON:__ "txt" file format. The app will read the file as a table and will detect the headers named “Channel_Name”, “X”, “Y” and “Frame”
*	__ONI:__ "csv" file format. The app will read the file as matrix and will get the 1st column as the channel name, 2nd column as frame number, 3rd column as X and 4th column as Y
*	__THUNDERSTORM:__ "csv" file format. The app will read the file as a table and will detect the headers named “Channel”, “Frame”, “x [nm]” and “y [nm]” 

You can also select other filters:

* __Channel alignment:__ For sequential PAINT (multiple files, one for each color in the image), you need to align the coordinates to correct for the drift. You will need to input extra files containing the fiducials for the corresponding images.
* __Silhouette metric:__ this can be used while optimizing your parameters, it is a metric used by DBSCAN to measure how well your nanoparticles are clustered and it should be close to 1. Sometimes is tricky to use this as DBSCAN doesn’t necessarily know how are your nanoparticles shaped, but you can see it easily in the figures that the app will output. This may take a long time if the images are too dense.
#
In the parameters tab you can choose the correct ones for your images. After optimizing these you can analyze files in batch. Scanning diameter is generally the same as the size of your particles, but if your images have a lot of background noise then is better to set it smaller, as this is the diameter that DBSCAN uses to follow the density of points.
#
To speed up the clustering algorithm, I divide the image in 9 sections and analyze it in parallel (the algorithm will check how many cores does your machine have and use as many as possible, with a limit on 9). 
#
Finally, in the graphs tab you will find histograms of the features for only one of the sections of the image, and it will save a csv file in your matlab path folder containing the features (size, aspect ratio, total number of localizations and localizations per channel) for your file(s).

## LICENSE

<a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-sa/4.0/88x31.png" /></a><br />This work is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/">Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License</a>.
