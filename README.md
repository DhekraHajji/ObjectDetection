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


Create a blob from the frame: The cv2.dnn.blobFromImage function prepares the frame for input to the neural network. It resizes the frame to a specific size (416x416 pixels), normalizes the pixel values to the range [0, 1], and converts the frame to a blob format that the network can process. The resulting blob is stored in the blob variable.

Set the input blob for the network: The net.setInput method sets the input blob as the input to the neural network. It prepares the network to perform a forward pass with the provided input.

Perform forward pass: The net.forward method performs a forward pass through the network using the input blob. It computes the output layer activations given the input and returns the output predictions. The output is stored in the outs variable.

Initialize lists for storing bounding boxes, confidences, and class IDs: Three empty lists (boxes, confidences, and class_ids) are created to store the information about the detected objects in the frame.

Process the output detections: The code iterates over each output layer's detections (out) obtained from the outs. For each detection, it extracts the class scores, identifies the class with the highest score (class_id), and retrieves the corresponding confidence (confidence).

Filter detections based on confidence threshold: If the confidence of the detected object is greater than 0.5, it is considered a valid detection. The code then proceeds to calculate the bounding box coordinates and scale them to the original frame dimensions.

Add bounding box information to lists: The top-left corner (x, y) and the width and height (bbox_width, bbox_height) of the bounding box are calculated based on the detected object's center coordinates and size. The calculated values are added to the respective lists (boxes, confidences, class_ids) for later use.

Apply non-maximum suppression: The cv2.dnn.NMSBoxes function performs non-maximum suppression on the detected bounding boxes to remove overlapping boxes with lower confidence. It returns the indices of the selected boxes after suppression, which are stored in the indices variable.

Draw bounding boxes and labels on the frame: Random colors are assigned to each class label using np.random.uniform. For each selected index, the code retrieves the corresponding bounding box coordinates, confidence, class ID, and color. It then draws a rectangle and the class label on the frame using cv2.rectangle and cv2.putText, respectively.

The resulting frame with bounding boxes and labels is displayed and written to the output video. This process is repeated for each frame in the video capture until there are no more frames left.

61-64. output.write(frame): This line writes the processed frame to the output video file.

cv2.imshow("Object Detection", frame): This line displays the processed frame in a window titled "Object Detection".

if cv2.waitKey(1) == ord("q"):: This line checks for a key press. If the "q" key is pressed, the loop is exited.

73-77. These lines release the video capture and output video writer objects, and close any OpenCV windows.
