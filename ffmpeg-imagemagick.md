### Cut Video

```
ffmpeg -i input.mkv -ss 1:40:00.0 -c copy -to 1:59:15.30 output.mkv
```

* Also remove sound and convert format

```
ffmpeg -i sintel.avi -ss 0:9:37.0 -c copy -to 0:9:40.50 -an bigFight.mp4
```


### Scale image

* Specify width

```
ffmpeg -i in.png -vf scale=iw/2:-1 out.png
```

* Specify height

```
ffmpeg -i in.png -vf scale=-1:ih/2 out.png
```


### Convert format

```
ffmpeg -i dense.avi -c:v libx264 noDepth.mp4
```


### Images to video

* Numeric filename

```
ffmpeg -framerate 20 -start_number 1 -i %3d_0zz.png -vf fps=20 -pix_fmt yuv420p output.mp4
```

* Character filename

```
ffmpeg -framerate 2 -pattern_type glob -i "*.png" -pix_fmt yuv420p output.mp4
```

* If not divisible by 2 (specify height)

```
ffmpeg -framerate 10 -pattern_type glob -i "*.png" -vf scale=-2:720 -pix_fmt yuv420p output.mp4
```

* If not divisible by 2 (specify width)

```
ffmpeg -framerate 10 -pattern_type glob -i "*.png" -vf scale=1280:-2 -pix_fmt yuv420p output.mp4
```


### Make GIF Loop

```
convert -delay 20 -loop 0 nonloopingImage.gif loopingImage.gif
```


### Overlay A on top of B

```
ffmpeg -i B.png -i A.png -filter_complex "[0:v][1:v] overlay" out.png
```

`[0:v][1:v]` means that we want the first video file we import with `-i` to be under video input file 1. `:v` just means we want video 0 and video 1. `[0:a]` would mean we want the first imported audio track.


* Scale A and then overlay A on top of B

```
ffmpeg -i B.png -i A.png -filter_complex "[1]scale=iw/2:-1[b];[0:v][b] overlay" out.png
```

`[1]` is short for "pick the best matching stream" (`[1:v]` is short for pick the best matching video stream -- same thing in this case) and `[b]` is the label for the scale output which is then fed to the overlay.


### Place two images side by side

```
ffmpeg -i a.jpg -i b.jpg -filter_complex hstack output
```


### Overlay text on image

```
convert in.png -pointsize 40 -fill red -annotate +100+100 'My Text' out.png
```