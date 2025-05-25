---
tags:
  - Recording
  - resource
Area: "[[Forex]]"
---


ffmpeg -i "2024-05-27 13-20-32.mkv" -map 0:a output.mp3

for %f in (*.*) do ffmpeg -i "%f" [options] "%~nf_converted.%~xf"

```bash

# Pulling audio out of mkv files and concatenating

Get-ChildItem . -Filter *.mkv | ForEach-Object { ffmpeg -i $_.FullName -map 0:a "$($_.Basename).mp3" }
(Get-ChildItem -File *.mp3 | ForEach-Object { "file '" + $_.Name + "'" }) | Out-File -FilePath "input.txt" -Encoding default
ffmpeg -f concat -safe 0 -i .\input.txt -c copy memo_2024-05-27.mp3  


!whisper --model medium "memo_2024-05-27.mp3"

# Concatenating actual video mkv files

ForEach ($oldvid in Get-ChildItem -File *.mkv) {
	$newvid = [System.IO.Path]::ChangeExtension($oldvid,".mp4")
	ffmpeg -i $oldvid -codec copy $newvid
}

(Get-ChildItem -File *.mp4 | ForEach-Object { "file '" + $_.Name + "'" }) | Out-File -FilePath "input.txt" -Encoding default

ffmpeg -f concat -safe 0 -i .\input.txt -c copy video_2024-06-02.mp4


# Transcribing audio

https://colab.research.google.com/drive/1uoevDiiV3kbU_953r6M7Wp3vegUgpIWv?usp=drive_link

!whisper --model medium "memo_2024-05-27.mp3"


```


