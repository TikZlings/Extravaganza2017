# Generating a video

This is a possible solution to generate a video from an animated `.gif` file. We could generate the set of `.png` images directly from the `.pdf` file instead of an intermediate `.gif` format, but let us not break the current work flow!

1. Extract all frames from the animated `.gif` as a set of `.png` images (all frames will be named `frame` followed by an integer reference indicating the current frame being extracted):

```
$ convert duck.gif frame%05d.png
```

2. Generate an `.avi` video from the frame set (the video filter is intended to slow down the animation; observe that the float value indicates the speed factor: if less than 1, the speed will be faster, or slower otherwise):

```
$ ffmpeg -i frame%05d.png -filter:v "setpts=3.0*PTS" duck.avi
```


3. Remove all `.png` images used to compose the video:

```
$ rm frame*.png
```

And we have a `duck.avi` video!

