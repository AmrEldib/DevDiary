# youtube-dl and ffmpeg

## Download and extract audio using youtube-dl
```
youtube-dl --extract-audio --audio-format mp3 URL_TO_YOUTUBE_VIDEO
```

## Convert video to FLAC using ffmpeg

```
ffmpeg -i VIDEO.webm -y AUDIO.flac
```
One problem is the the FLAC file is too big. 1.7 GB for a 3 hours audio file.

## Convert video to MP3 using ffmpeg
```
ffmpeg -i VIDEO.webm -y AUDIO.mp3
```
[More details](http://bytefreaks.net/gnulinux/bash/ffmpeg-extract-audio-from-webm-to-mp3)  

However, this is failing because the LAME encoder is missing.  
