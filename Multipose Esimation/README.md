# Jump and Block Detection with Pose Estimation using TensorFlow MoveNet Model

The code leverages a powerful pre-trained model, known
as ”movenet,” to accurately detect essential body keypoints,
including hips, knees, ankles, shoulders, nose, and wrists,
from successive video frames. By precisely tracking the spatial
coordinates of these keypoints over time, the system can
effectively identify instances of jumps and blocks performed
by athletes during sports events.

Pose estimation is a challenging computer vision task be-
cause it involves the detection and localization of key body
joints and parts in an image or video. Various issues raised
when trying to capture data.

* No two bodies are the same: Human bodies are highly
articulated and complex structures and are free to move
and act with incredible behaviors. For this, capturing
keypoints is difficult for various bodies and occlusions.
* Body parts can be occluded in images due to various
reasons, such as objects or other people blocking the
view. Handling occlusions is crucial for accurate pose
estimation, as missing or partially visible joints can
impact the model’s performance.
* In certain poses, body parts may appear close to each
other or overlap, leading to ambiguity in the estimation.
For example, distinguishing between the left and right
hand when they are close together can be challenging.
* When using footage from pre recorded games of volley-
ball or a trainer demonstrating an action the last time
they jumped will not be the same as the next time. Lots
of careful tweaking takes place in order to gather the
events that clearly occurred in the frame and avoid any
erroneous counters

We begin by leveraging the MoveNet model to predict
the positions of the body keypoints in each frame of the
video stream. The model’s deep learning-based architecture
allows it to accurately estimate the coordinates of various body
joints with associated confidence scores. The code processes
a real-time video stream obtained from a video source, such
a recorded video file. It continuously reads frames from the
video stream using Open Computer Vision’s video capture ob-
ject. The frame and returns a set of keypoints along with their
corresponding confidence scores. The keypoints represent the
estimated positions of various body joints, and the confidence
scores indicate the model’s certainty about the correctness of
these predictions.

The code maintains a history of keypoints’ positions for
each person in the frame. To achieve this, it uses dictionaries
called previous positions and counters. The previous positions
dictionary stores the coordinates of key body joints for each
person, while the ”counters” dictionary keeps track of the
number of jumps and blocks for each individual
The actual jump detection is performed by analyzing the
movement of keypoints over a window of frames. Through
testing of pre trained video, it was settled on 10 frames was
good enough to detect when a person was jumping with most
media it analyzed. When enough frames are available in the
window, the code calculates the vertical movement of each
keypoint, such as hips, knees, ankles, shoulders, and head,
relative to their positions in the first frame of the window. If
the movement exceeds a certain threshold the code identifies
it as a jump.
