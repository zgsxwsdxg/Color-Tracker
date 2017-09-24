# Color Tracker

Color tracking module with OpenCV 3.

It also has an "alert callback function" when the object crosses a line. You can set this line with `alert_y` and
the callback function with `alert_callback_function`.

## Sample

TODO: sample gif

## Setup & install

You will need:

- Python 3
- OpenCV 3
- Numpy

Install:

`python setup.py install` OR `pip install git+https://github.com/gaborvecsei/Color-Tracker.git`

## Basic Usage

```shell
>>> import color_tracker
>>> color_tracker.__version__
'0.1.0'
```

There are 2 callbacks:

- *tracking callback*: called at every frame
- *alert callback*: called only when it crossed the "alert line"

You can find sample scripts at the `Examples` folder

```python
import cv2
import color_tracker


def tracking_callback(frame, debug_frame, object_center):
    cv2.imshow("debug frame", debug_frame)
    key = cv2.waitKey(1)
    if key == 27:
        tracker.stop_tracking()
    print("Object center: {0}".format(object_center))


webcam = color_tracker.WebCamera(video_src=0)
webcam.start_camera()

kernel = cv2.getStructuringElement(cv2.MORPH_ELLIPSE, (11, 11))

tracker = color_tracker.ColorTracker(camera=webcam, max_nb_of_points=20, debug=True)
tracker.set_tracking_callback(tracking_callback=tracking_callback)
tracker.track(hsv_lower_value=(0, 100, 100),
              hsv_upper_value=(10, 255, 255),
              min_contour_area=1000,
              kernel=kernel)

webcam.release_camera()
```

## Color Range Detection

Just run this little script and you can get the necessary information for the color detection.

(You can find this also in the `Examples` folder)

```python
import color_tracker

cam = color_tracker.WebCamera(video_src=0)
cam.start_camera()

detector = color_tracker.HSVColorRangeDetector(camera=cam)
lower, upper, kernel = detector.detect()

print("Lower HSV color is: {0}".format(lower))
print("Upper HSV color is: {0}".format(upper))
print("Kernel is: {0}".format(kernel))
```

## About

Gábor Vecsei

- [Personal Blog](https://gaborvecsei.wordpress.com/)
- [LinkedIn](https://www.linkedin.com/in/gaborvecsei)
- [Twitter](https://twitter.com/GAwesomeBE)
- [Github](https://github.com/gaborvecsei)
- vecseigabor.x@gmail.com