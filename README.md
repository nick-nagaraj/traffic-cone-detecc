# traffic-cone-detecc
Uses Tensorflow Object Detection API to retrain SSD MobileNet v2 to localize traffic cones

# Procedure
1. First converted the video into a series of images using a video to image python script. 
2. Labeled a series of distinct images using LabelMe.
3. Through the number of json files, converted them into individual csv files. (There might be an easier way to do this, however I certainly had no such luck with python scripts)
4. Combined each csv file into a single csv file.
5. Used an online csv editor to match the format that the csv_to_tfrecord python script requires(Have added my own for reference). Namely adding the image name, and resolution of the image (Same as resolution of the video)
6. Divided dataset into training and testing.
7. Created a seperate tfrecord file for both training and testing.
8. Created a labelmap.pbtxt file. I have included my own as reference. As I am only trying to detect cones, I only have one class.
8. Chose an appropriate model to retrain (SSD MobileNet v2 trained on COCO dataset)
9. Downloaded the CKPT for the respective model.
10. Edit the config file including required paths, and a few training parameters. Adjust this according to your needs.
11. Moved 'train.py' file from the legacy folder to the object detection folder.
12. Run training. Would highly recommend doing this on collab. Took roughly 30 minutes for training as opposed to completely not running at all on my local build.
13. Once training is complete, either export the frozen_inference_graph using the built in script or use the model-XXXX.ckpt. 
14. Run a driver program that uses the exported frozen_inference_graph to generate bounding boxes around predictions (Requires OpenCV 3 or below. Does not work on OpenCV 4)
15. Smile at the results!

# Notes
1. Switching between models is incredibly easy, as just replace the model name by the model you wish to add. Make sure to edit the config file as required.
2. GPU training is advised.
3. Do not skimp on training data. This approach requires an abundance of training data.
