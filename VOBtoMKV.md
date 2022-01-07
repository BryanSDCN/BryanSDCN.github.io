[返回主页](index.md)

合并光盘内视频文件：

`copy /b VTS_01_1.VOB+VTS_01_2.VOB+VTS_01_3.VOB+VTS_01_4.VOB+VTS_01_5.VOB+VTS_01_6.VOB+VTS_01_7.VOB+VTS_01_8.VOB input.VOB`

查看输入流信息：

`ffmpeg -i input.VOB`

VOB转MKV：

`ffmpeg -fflags +genpts -i input.VOB -map 0:1 -map 0:2 -c:v copy -c:a copy output.mkv`

截取视频片段：

`ffmpeg -i output.mkv -c copy -ss 00:01:37.950 -to 00:45:23.200 1.mkv`

[返回主页](index.md)

