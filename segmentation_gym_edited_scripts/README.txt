Here is what each script is used for:

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