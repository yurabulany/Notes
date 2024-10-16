https://www.youtube.com/watch?v=WLcW4UWPC5Y&t=44s

## USE Fedora 37 in distrobox, you just need
https://youtu.be/wmRiZQ9IZfc


### ffmpeg command to convert to .mov file (works fine!)
ffmpeg -i <your.mp4> -c:v dnxhd -profile:v dnxhr_sq -c:a pcm_s16le <your.mov>

### Backwards conversion
ffmpeg -i final_cut.mov -c:v libx264 -preset ultrafast -crf 0 final_video.mp4

### Bulk conversion (works fine!)
`for i in *.mp4;do ffmpeg -i "$i" -c:v dnxhd -profile:v dnxhr_sq -c:a pcm_s16le "${i%.mp4}.mov";done`


## Alternative commands
`ffmpeg -i input-video.mp4 -c:v dnxhd -profile:v dnxhr_hq -pix_fmt yuv422p -c:a pcm_s16le output-video.mov`
