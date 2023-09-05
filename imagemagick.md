```
convert -resize 200x100 src.jpg dest.jpg
```
按照200x100比例找出原图最适合的图形，在缩放到200x100的尺寸

```
convert -resize 200 src.jpg dest.jpg
```
得到图片宽为200，高根据原始图片比例计算而来

```
convert -resize x100 src.jpg dest.jpg
```
得到的图片高为100，宽根据原始图片比例计算而来

```
convert -resize 200x100! src.jpg dest.jpg
```
强制改变图片尺寸为200x100,会变形

```
convert -resize "1920x1080>" src.jpg dest.jpg

convert -resize "1920>" src.jpg dest.jpg

convert -resize "x1080>" src.jpg dest.jpg
```
宽度大于1920或者高度大于1080的图，按照宽度1920或者高度1080进行等比例缩放，宽度优先比较，如果小于则不变

```
convert -resize "1920x1080<" src.jpg dest.jpg

convert -resize "1920<" src.jpg dest.jpg

convert -resize "x1080<" src.jpg dest.jpg
```
宽度小于1920或者高度小于1080的图，按照宽度1920或者高度1080进行等比例缩放，宽度优先比较，如果大于则不变


```
convert -resize "10x1000<!" src.jpg dest.jpg
```
