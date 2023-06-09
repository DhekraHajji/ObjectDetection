# ObjectDetection
Computer vision
import cv2 and import numpy as np: These lines import the necessary libraries. cv2 is the OpenCV library for computer vision tasks, and numpy is a library for numerical computing in Python.

net = cv2.dnn.readNet("yolov3.weights", "yolov3.cfg"): This line loads the pre-trained YOLO (You Only Look Once) model using the weights and configuration files specified.

with open("coco.names", "r") as f: classes = [line.strip() for line in f.readlines()]: This code reads the class names from the "coco.names" file and stores them in the classes list. These class names correspond to the objects that the YOLO model can detect.

cap = cv2.VideoCapture("C:\\Users\\Dhekra Hajji\\OneDrive - CXG\\Bureau\\video.mp4"): This line opens a video file for reading. The file path specifies the location of the video file to be processed.

frame_width = int(cap.get(cv2.CAP_PROP_FRAME_WIDTH)) and frame_height = int(cap.get(cv2.CAP_PROP_FRAME_HEIGHT)): These lines retrieve the width and height of the video frames in pixels.

15-16. display_width = 800 and display_height = 600: These lines define the desired width and height for displaying the video frames.

19-20. scale_width = display_width / frame_width and scale_height = display_height / frame_height: These lines calculate the scaling factors for resizing the frames to the desired display size.

output = cv2.VideoWriter("output.mp4", cv2.VideoWriter_fourcc(*"mp4v"), 30.0, (frame_width, frame_height)): This line creates a video writer object to save the processed frames as an output video. The output video will be saved as "output.mp4" using the MP4V codec, with a frame rate of 30 frames per second.
25-58. The code inside the while loop reads each frame from the video capture, resizes it, performs object detection using the YOLO model, and draws bounding boxes and labels around the detected objects.

61-64. output.write(frame): This line writes the processed frame to the output video file.

cv2.imshow("Object Detection", frame): This line displays the processed frame in a window titled "Object Detection".

if cv2.waitKey(1) == ord("q"):: This line checks for a key press. If the "q" key is pressed, the loop is exited.

73-77. These lines release the video capture and output video writer objects, and close any OpenCV windows.
