# fruit-NeRF

This project implements a custom NeRF (Neural Radiance Fields) model for creating a 3d model using the input images of frruit images taken in my bedroom. The NeRF model taken a bunch of images and its camera poses information to create a 3d model of the scene. COLMAP was used to generate the pose information from the fruit images.

### Results
- results as the training progresses,

![](https://github.com/tusharparimi/fruit-NeRF/blob/main/training_newfruit_50.gif)

- final 360-degree scene,

![](https://github.com/tusharparimi/fruit-NeRF/blob/main/rgb_video_newfruit.gif)

### Extracting camera poses from COLMAP and implementing NERF:
- Download and install the COLMAP using the pre-built binaries or from source.
- Download the colmap2nerf.py script from NVlab’s [instant-ngp](https://github.com/NVlabs/instant-ngp/tree/master/scripts) github.
- Make sure you have the colmap2nerf.py script and your custom images folder in the same directory.
- From your terminal run your colmap2nerf.py script with required arguments including the path to the folder containing your input images for which you want to get the camera poses. 
Example command-
python colmap2nerf.py --colmap_matcher exhaustive --run_colmap --aabb_scale 16 --images imagesfoldername
- This should result in a bunch of files in the same directory. The camera poses can be found in transform.json file that has info about each image frame like its path and computed pose matrix.
- Useful [documentation](https://github.com/NVlabs/instant-ngp/blob/master/docs/nerf_dataset_tips.md#colmap)
- Once you successfully have the transform.json file with all the pose matrices for each image frame. You can use the same nerf [code](https://github.com/tusharparimi/fruit-NeRF/blob/main/nerf_fruit.ipynb) to train your nerf model. You may have to change a bit of the code as now you are reading images from an image folder and camera poses, focal length from transform.json file.
- You actually need to compute the focal length as the transform.json file only has the camera_angle_x(beta) and camera_angle_y(alpha) values.

<img width="236" alt="image" src="https://github.com/tusharparimi/fruit-NeRF/assets/93556280/23f14f39-c9d3-407c-9953-a4f59fbad5ed">

 
