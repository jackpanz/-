```java
String s="<img src=\"file/img/2016/12-28/1234-25521482893088459.jpg\"  title=\"1234.jpg\" alt=\"\" width=\"396\" height=\"271\" style=\"width: 396px; height: 271px;\"/>";
System.out.println(s.replaceAll("(<img.*?)style=\".*?\"", "$1"));
```
