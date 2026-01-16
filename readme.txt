cut:
ffmpeg -i in.mp4 -ss 00:00:01 -t 00:00:22 -vcodec copy -acodec copy out.mp4

extract:
ffmpeg -i in.mp4 -vn -acodec copy out.m4a

convert:
ffmpeg -i in.m4a -vn -ar 44100 -ac 2 -ab 128k -f mp3 out.mp3

concat:
foreach ($i in Get-ChildItem .\*.mp3) {echo "file '$i'" >> list.txt} | ffmpeg -f concat -safe 0 -i list.txt -c copy out.mp3

mass rename:
dir | rename-item -NewName {$_.name -replace "search","replace"}

stream:
ffmpeg -hide_banner -i "%SRC%" -c:a aac -b:a 32k -ac 2 -ar 48000 -f flv "%RTMP_URL%%STREAM_KEY%"
