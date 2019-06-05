ISA525700 Computer Vision for Visual Effects<br/>Homework 6
===

## Our video

我們一共拍了兩個影片，第一個影片用來放置一些物件，觀察在不同的做法下，對於相機動態的分析情形，第二個影片則主要用來做特徵點的追蹤，製作以動作為依據的特效。

<a href="http://www.youtube.com/watch?feature=player_embedded&v=NykvRc1kfnk
" target="_blank"><img src="http://img.youtube.com/vi/NykvRc1kfnk/0.jpg" 
alt="Our video (fail to load the image, please click here to see the video)" width="240" height="180" border="10" /></a>

<a href="http://www.youtube.com/watch?feature=player_embedded&v=OPxcWSGy1ME
" target="_blank"><img src="http://img.youtube.com/vi/OPxcWSGy1ME/0.jpg" 
alt="Our video (fail to load the image, please click here to see the video)" width="240" height="180" border="10" /></a>

## Visual effects (with 3D model)

我們分別使用ORB-SLAM2和AE來做特效，在卡納赫拉皮卡丘和小火龍的中間放入愛心，另外，在ORB-SLAM2的部分，我們還有在卡納赫拉皮卡丘的上面加入一個正在飛的蝴蝶的3D模型。

### ORB-SLAM2

ORB-SLAM2利用提取稀疏特徵點的方式來達到定位的效果，在這次作業的部分我們將我們所拍攝的影片作為mono_tum的輸入，希望透過特徵點的提取，將其輸出的相機外部參數作為影片加入特效...等的依據。

#### Build up and Run ORB-SLAM2
![](https://i.imgur.com/jeYo9ij.png)


#### Add visual effect add 3D model
在影片中加入蝴蝶的3D model及愛心image，實作步驟如下：
1. 利用video中獲得frame，30fps的影片則每秒取得30張
2. 如example中的輸入檔，生成Timestamp+檔名的input txt
3. 將兩者作為input，獲得camera參數包含timestamp, position, rotation
4. 因為keyframe過少，撰寫code針對pisition及rotation進行內插
5. 利用unity讀取上步驟結果，作為camera移動及轉動依據
6. 於場景中加入3D物件及image![](https://i.imgur.com/3KLxEmO.png)


#### 結果
<a href="http://www.youtube.com/watch?feature=player_embedded&v=wAc5LuGO5PQ
" target="_blank"><img src="http://img.youtube.com/vi/wAc5LuGO5PQ/0.jpg" 
alt="Our video (fail to load the image, please click here to see the video)" width="240" height="180" border="10" /></a>

### AE

在AE的部分，我們利用Tracker中的3D camera tracker，首先分析出相機的位移以及旋轉，接著利用取得的特徵點將愛心貼到小火龍和皮卡丘之間形成的平面上，如此即可達到我們想要的效果。

### Comparison

ORB_SLAM2_Python

* 優點
    1. 可以將整個過程自動化
    2. 在應用上如AR等，若搭配穩定的旋轉資訊，如九軸感測，能夠達到很好的效果(如github上的unity SLAM的
實作方法簡單、直觀，Python也好寫
需要調整的參數只有一個而且算直觀
不用下載很肥的Unity或後製軟體，即可簡單達到所需效果
缺點

從「座標軸移動的位置」對應到圖片中的pixel沒有既定公式（需肉眼評量）
需要 tune scale
ORB_SLAM2_Unity

優點

有虛擬相機調整xyz軸的相對變動，概念上比較簡單
在插入物件時，使用上比 Python 找 Pixel 直觀
缺點

實際拍攝所用的鏡頭與Unity camera並不完全相同，要調整有難度、不直覺
需要上手此軟體的操作、C#沒python方便
需要好的硬體執行，才不容易當機或卡卡的
## Special effects based on the pose information

這個部分我們利用AE來進行實作，利用Tracker中的Track Motion，分別以卡納赫拉伊布和卡納赫拉皮卡丘的鼻子為特徵點進行追蹤，並依據追蹤結果讓他們手上拿著花花，另外，花花還會噴出星星，其中，卡納赫拉伊布的移動比較平行，我們只追蹤Position，卡納赫拉皮卡丘則有微微旋轉，所以我們還追蹤了Rotation，從影片中可以看到追蹤非常準確，效果非常好。

<a href="http://www.youtube.com/watch?feature=player_embedded&v=66tIZ3vtJ6s
" target="_blank"><img src="http://img.youtube.com/vi/66tIZ3vtJ6s/0.jpg" 
alt="Our video (fail to load the image, please click here to see the video)" width="240" height="180" border="10" /></a>


