# ffmpeg 编辑视频

- 从 GIF 视频中删除第 1 帧，并且确保剩余的帧尽量保持原样
```
ffmpeg -i 4-3-1.gif -filter_complex "[0:v]select='gte(n,1)',split[s0][s1];[s0]palettegen[p];[s1][p]paletteuse" 4-3-1-0.gif
```

