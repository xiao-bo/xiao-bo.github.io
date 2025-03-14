---
layout: post
title:  "Python 變數名稱原理"
author: bowen
categories: [ Software Development]
excerpt: 你是否有想過，為什麼Python跟其他語言不一樣，不用事先宣告變數型態呢？是Python比較厲害嗎？還是其他語言比較笨呢？

---
你是否有想過，為什麼Python跟其他語言不一樣，不用事先宣告變數型態呢？是Python比較厲害嗎？還是其他語言比較笨呢？

在C語言或一般需要編譯器語言的世界中，所有的變數都要事先宣告，OS會挖一塊記憶體空間，裡頭放著此變數的資料。宣告完後，程式才能在編譯階段，將此變數link到此記憶體空間，執行階段才能利用此變數。

所以大家常常聽到的Pointer，便是記憶體空間的位置。

在Python世界裡頭，變數不用事先宣告，變數名稱只是個名牌，變數是綁到值上面，所以多個變數，可能綁到同一個值，值有記憶體位置，但是變數沒有，很抽象吧？

可以想像值都是一個個的包裹，但要給予名牌（變數名稱），此包裹（值）才會有固定的記憶體位置，此時變數名稱若被指到另一個值，原本包裹（值）的記憶體位置並不會改變，改變的是變數指向的位置（另一個包裹），所以變數名稱可以一直跳來跳去，但若是一個值很久沒被指到，就會被Operation System所回收，清空記憶體

#### 第一個例子

a和b的值都是5，此時代表包裹（5）被兩個名牌黏到，因此兩個名牌的記憶體位置都相同，但a被指到12後，因為名牌a去指到另一個包裹（5），所以記憶體位置也就不同。

    a = 5
    b = 5
    a ## print 5
    type(a) ## print int
    id(a) ## 記憶體位置為 4414393248
    id(b) ## 記憶體位置為 4414393248
    a = 12 
    id(a) ## 記憶體位置為 4414393472
    id(b) ## 記憶體位置為 4414393248

#### 第二個例子

b = b + 1 等於把 5的值取出來+1，產生出一個新資料，再將新資料指向b，並非將5改成6

    a = 5
    b = b + 1 ## b = 6
    id(b) ## 記憶體位置為4414393280 
    id(a) ## 記憶體位置為4414393248
    a = a + 1 ## a = 6
    id(a) ## 記憶體位置為4414393280

從這兩個例子，可以顯示Python的變數名稱的原理。

若是有誤，歡迎討論唷！

備註：

參考「Python 技術者們 ： 實踐！ 帶你一步一腳印由初學到精通 」，非常感謝此書作者：施威銘研究室。

以前筆者沒有仔細的去研究Python，近期才買一本書來細細讀，才發現Python雖然入門門檻極低，但天花板很高，蘊含了非常多的細節，故將一些有意思的部份整理出來，Po在Medium上，希望能幫助更多人，

如果對此書有興趣，歡迎去購買唷！（絕對沒業配，也並非是研究室一員）