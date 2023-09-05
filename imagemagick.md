强制改变图片的高度为528
```
mogrify -resize 960x528! *.png
```

resize 宽度大于1920转成1920,小于则保持不变
```
magick 原路径 -resize 1920>, 目标路径
```

批量转换格式
```
magick mogrify -format jpg -path /Users/jackpan/Downloads/a002  *.jpg
```
