Here are my scripts and edits made for use with Doodleverse segmentation_gym, which can be found at https://github.com/Doodleverse/segmentation_gym.
The files make_dataset_revised.py and train_model_revised.py are not original code, instead patched versions of code that can be found at this repository above
Below are the descriptions of each script:

-----------------------------------------------------------------------------------------------------------------------------
-----------------------------------------------------------------------------------------------------------------------------
-----------------------------------------------------------------------------------------------------------------------------
For the scripts inside segmentation_gym_edited_scripts
-----------------------------------------------------------------------------------------------------------------------------
Gemini_Manual_Shuffler: Gemini assisted script used to manually shuffle imagery before running make_dataset.py, as make_dataset.py from segmentation gym failed to do so.
-----------------------------------------------------------------------------------------------------------------------------
Gemini_Multispectral_Data_Cleaner: Gemini assisted script to be run after make_dataset.py but before train_model_revised.py, as make_dataset.py created incompatible-size .npz files for train_model_revised.py when using more than 3 bands for training.
-----------------------------------------------------------------------------------------------------------------------------
make_dataset_revised.py: Patched make_dataset.py script from segmentation gym
-----------------------------------------------------------------------------------------------------------------------------
train_model_revised.py: Patched train_model.py script from segmentation gym
-----------------------------------------------------------------------------------------------------------------------------
Note that none of the segmentation gym environment files are present among other files; the original code for segmentation gym and accompanying files can be found at https://github.com/Doodleverse/segmentation_gym 
-----------------------------------------------------------------------------------------------------------------------------
-----------------------------------------------------------------------------------------------------------------------------
-----------------------------------------------------------------------------------------------------------------------------



-----------------------------------------------------------------------------------------------------------------------------
-----------------------------------------------------------------------------------------------------------------------------
-----------------------------------------------------------------------------------------------------------------------------
For the scripts inside Non_Ubuntu_Scripts
-----------------------------------------------------------------------------------------------------------------------------
Binary_Mask_Maker: Used to create a binary mask file based on a source tif and a polygon shapefile. Returns a binary mask tif.
-----------------------------------------------------------------------------------------------------------------------------
Image_Augmentor: Contains the following functions/scripts in order:

tif_to_png_mask_and_rgb(img_dir, output_dir) --- RGB tif to 24-bit PNG
tif_to_png_ndvi(img_dir, output_dir) --- NDVI tif to PNG
tif_to_png_slope(img_dir, output_dir) --- Slope tif to PNG
rgba_to_rgb(rgba_directory, rgb_directory) --- RGBA imagery to RGB PNG
augmentation_script(image_path, mask_path) --- Augmentation script to create augmented copies of PNG imagery
section_divider(input_path, output_path) --- Divider script that splits images into sections (4x4)
section_creator(input_path, section_sum = 16) --- Sorts divided images into dictionary for use in recombination script
section_recombination_four_by_four(input_path, output_path, section_sum = 16) --- Recombination script reversing the prior script
Only works for 4x4 image tiles as the name suggests
multispectral_to_rgb_png(input_dir, rgb_dir, rgb_bands = [1,2,3]) --- More sophisticated multispectral tif to PNG, using min-max scaling across every divided tif image in a folder to create a range to scale each image's RGB values to 0-255. Essentially considers the color of a massive divided tif instead of each individual section's pixel values to determine the range in which the rgb values will be scaled to. Utilizes QGIS' method of displaying RGB imagery.
This one is important to review
filterer_and_divider(large_dir, filtered_dir, section_filtered_dir, size=1024, bands=3) --- Filters out images that are either not square or have all 0 values for their first band
overlay_mask_on_image(image, mask, alpha=0.5) --- Overlays a mask png onto an image png

This notebook also describes the workflow of image processing, starting from a folder of Worldview-2 .tif tiles received from QGIS retile. From there, image tiles are converted into min-max scaled rgb pngs and divided further into 256x256 image tiles. Lastly, segmentation is performed using Segmentation Gym, and mask tiles are recombined to 1024x1024 using the recombination script. These images will then be taken to the Georeference_Gym_Model_Masks to be integrated with original tif tiles.
-----------------------------------------------------------------------------------------------------------------------------
Georeference_Gym_Model_Masks: Contains two scripts to georeference the masks produced by Segmentation Gym and recombined by Image_Augmentor. The first one is a general script, while the second one is adjusted to match the specific naming convention introduced by one of my tests.
-----------------------------------------------------------------------------------------------------------------------------
Retile_Missing_Data_Filter: Used for some runs; filters out missing data generated by gdal_retile in QGIS
-----------------------------------------------------------------------------------------------------------------------------
-----------------------------------------------------------------------------------------------------------------------------
-----------------------------------------------------------------------------------------------------------------------------

Note: I do not have a script for tiling the large base raster, as I do that in QGIS; may be a script to write to better automate in the future for larger scale tasks.
