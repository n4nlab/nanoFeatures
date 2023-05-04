# nanoFeatures
_MATLAB app to characterize nanoparticles imaged with super-resolution microscopy._

## Installation guide
Clone or download all files in this repository to your local folder, it contains the app file (mlapp) and the secondary scripts called from the main code, is important to keep all the files in the same local folder. Click on the “.mlapp” file and the the GUI will pop-up.
#
In the first tab, you select the file(s) you want to analyze and the input type in the dropdown menu:

* NIKON:

   Txt file format
   The app will read the file as a table and will detect the headers named “Channel_Name”, “X”, “Y” and “Frame”
*	ONI:

   Csv file format
   The app will read the file as matrix and will get the 1st column as the channel name, 2nd column as frame number, 3rd column as X and 4th column as Y
*	THUNDERSTORM:

   Csv file format
   The app will read the file as a table and will detect the headers named “Channel”, “Frame”, “x [nm]” and “y [nm]” 

For your STORM files you will most likely need the “NIKON” option. You can also select other filters:
•	Density filter: as for now this is comented in the code (ignored), because it takes forever in matlab and is much faster to first density filter the images in thunderstorm (thus the thunderstorm option in the dropdown menu). Don’t use this option 😉
•	Channel alignment: in case you image different colors sequentially (multiple files for one image), you need to align the coordinates. You will need to input an extra file containing the fiducials so the algorithm can calculate the drift. Let me know if you need to use this and I will explain further.
•	Silhouette metric: this can be used while optimizing your parameters, it is a metric used by DBSCAN to measure how well are your nanoparticles clustered and it should be close to 1. Sometimes is tricky to use this as DBSCAN doesn’t necessarily know how are your nanoparticles shaped and you can see it easily in the figures that the app will output. Also, if your files are too dense in localizations it will also take forever.

 

In the parameters tab you can choose the correct ones for your images. I recommend optimizing these before analyzing the files in batch. Scanning diameter is generally the same as the size of your particles, but if your images have a lot of background noise then is better to set it smaller, as this is the diameter that DBSCAN uses to follow the density of points (with the gif is easier to understand). The rest of parameters I think are clear, but let me know if you need any help.
 

To speed up the clustering algorithm, I divide the image in 9 sections and analyze it in parallel (the algorithm will check how many cores does your machine have and use as many as possible with a limit on 9). Finally, in the graphs tab you will find histograms of the features for only one of the sections of the image, and it will save a csv file in your matlab path folder containing the features (size, aspect ratio and total number of localizations and localizations per channel) for your file. If you input many files, it will analyze them using the same parameters and you will obtain a features csv file for each one of your input files.
