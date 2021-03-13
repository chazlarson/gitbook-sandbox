```ini
[MP4]
ffmpeg = /usr/bin/ffmpeg
ffprobe = /usr/bin/ffprobe
threads = 20
output_directory =
copy_to =
move_to =
; 'output_extension' and under 'output_format' - These need to be mp4.
output_extension = mp4
output_format = mp4
; 'delete_original' - optional if you want a orignal version and a direct play friendly versions set to False
delete_original = True
; 'relocate_moov' - optional True (for "easier" streaming) makes conversion longer
relocate_moov = False 
video-codec = h264, x264, h265, x265, hevc, HEVC
; 'video-bitrate' - is in bytes. For example, 4000 is 4mbps file.
video-bitrate =
video-crf =
video-max-width =
video-profile =
; Leave 'h264-max-level' blank to copy, set to 4.0 or 4.1 if you have an old device, most you can set in plex to play a higher level without a problem - in client settings.
h264-max-level =
use-qsv-decoder-with-encoder = True
use-hevc-qsv-decoder = False
enable_dxva2_gpu_decode = False
; 'ios-audio = True' if you want a stereo audio stream.
ios-audio = False
ios-first-track-only = False
ios-audio-filter = pan=stereo|c0=0.25*c0+c2+0.6*c3|c1=0.25*c1+c2+0.6*c3
ios-move-last = False
max-audio-channels =  8
audio-codec = ac3, aac
audio-language =
audio-default-language =
audio-channel-bitrate = 0
audio-filter =
audio-copy-original = True
audio-first-track-of-language = False
subtitle-codec = mov_text
subtitle-language =
subtitle-default-language = nil
subtitle-encoding =
fullpathguess = True
convert-mp4 = True
; 'tagfile' - optonal; 'True' - tags the file for finding metadata. Plex doesn't struggle with this so pointless, makes conversion longer.
tagfile = False
tag-language = eng
download-artwork = nil
; 'download-subs = True' if you want subs, never tried it, you need a dependency (I don't think this is installed by default)* 
download-subs = False
embed-subs = True
embed-only-internal-subs = True
```