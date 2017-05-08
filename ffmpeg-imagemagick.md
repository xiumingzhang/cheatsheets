### Cut Video

```
ffmpeg -i input.mkv -ss 1:40:00.0 -c copy -to 1:59:15.30 output.mkv
```

* Also remove sound and **convert format**

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

* **Numeric** filename

```
ffmpeg -framerate 20 -start_number 1 -i %3d_0zz.png -vf fps=20 -pix_fmt yuv420p output.mp4
```

* **Character** filename

```
ffmpeg -framerate 2 -pattern_type glob -i "*.png" -pix_fmt yuv420p output.mp4
```

* Filename of **certain length**

```
ffmpeg -framerate 2 -pattern_type glob -i "???.png" -pix_fmt yuv420p -y output.mp4
```

`???.png` matches with all filenames of length 3. `-y` overwrites without asking.

* If **not divisible by 2** (specify height)

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

`[0:v][1:v]` means that we want the first video or image file we import with `-i` to be under the second video or image file.


* **Scale** A before overlaying

```
ffmpeg -i B.png -i A.png -filter_complex "[1]scale=iw/2:-1[b];[0:v][b] overlay" out.png
```

`[1]` is short for "pick the best matching stream" (`[1:v]` is short for pick the best matching video stream -- same thing in this case) and `[b]` is the label for the scale output which is then fed to the overlay.

* **Make transparent** A before overlaying

```
ffmpeg -i B.png -i A.png -filter_complex "[1]format=argb,geq=r='r(X,Y)':a='0.5*alpha(X,Y)'[b];[0:v][b] overlay" out.png
```

`0.5` is the opacity factor. I'm including `format=argb` so that it also works with overlay images that don't have an alpha channel of themselves.


### Horizontally stack two images

```
ffmpeg -i a.jpg -i b.jpg -filter_complex hstack output
```


### Vertically stack two images; need to rescale one

```
ffmpeg -i top.png -i bottom.png -filter_complex '[1][0]scale2ref=iw:iw*(H/W)[2nd][ref];[ref][2nd]vstack' out.png
```

where `H` and `W` should be replaced with the height and width of `bottom.png`, respectively.


### Overlay text on image

```
convert in.png -pointsize 40 -fill red -annotate +100+100 'My Text' out.png
```


### Rotate images in a folder

```
for file in ./*.png; do
    convert "$file" -rotate 90 "${file%.png}"_rotated.png
done
```

### Crop a video

```
ffmpeg -i gump_orig.mp4 -filter:v "crop=1280:520:0:100" gump.mp4
```
