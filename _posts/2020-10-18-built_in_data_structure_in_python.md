---
layout: post
title:  "Python內建的資料結構"
author: bowen
categories: [ Software Development]
excerpt: 此篇會介紹Python內建的資料結構，如List、Tuple、Set、Dict、String的特性和筆者常用的一些操作，以及Function、Method的差別。


---
此篇會介紹Python內建的資料結構，如List、Tuple、Set、Dict、String的特性和筆者常用的一些操作，以及Function、Method的差別。

## 大綱：

* Python內建常用的資料結構
* Function、Metho的差別

## Python內建常用的資料結構有：

* List
* Tuple
* Set
* Dict
* String

而這些資料結構中的資料項目，會被稱為元素（Element ）

## List:

可儲存一串資料的結構，就像是C語言的陣列（Array）一樣，非常直觀，

但不同的是，Python中的同一個List，可以儲存不同型態的元素，（C語言的陣列都必須是固定型態），此外，Python不必事先宣告長度，長度隨著元素數量動態增長。

List常用的幾個操作

* 負號索引（Index）：C語言如果要取得array的最後一個元素，通常會使用 array.length-1 當成索引取得，例如 a[a.length-1] 。但是在Python中，可以直接使用 a[-1]，相較於 array.length-1 ，不只簡潔，且更易讀。
* 找尋元素：當想要找一個元素是否有在此List中，可以直接使用 a in s 判斷是a元素是否在s List中。比起二分搜尋法或線性搜尋法，此寫法簡潔有力。
* 切片（Slice）

語法如下

    a = [0,1,2,3,4,5,6,7,8,9] 
    a[2:]  #索引2到最後的數都列出來，
    # [2,3,4,5,6,7,8,9]a[2:4] # 只列出n到m-1唷！
    # [2,3] a[2:6:3] # 從索引2到6，間隔3個、3個取資料
    # [2,5]a[:6] # 列出到索引6為止
    # [0,1,2,3,4,5]a[::-1] # 反向列出
    # [9,8,7,6,5,4,3,2,1,0]

此外，List有索引，因此屬於有序的資料結構（這會在後面在重複提到）

## Tuple

Tuple和List的特性大致相同，一樣都是有序集（有索引的概念），但是Tuple的元素是不可更動（Immutable），也就是說，一旦宣告元素的值後，就不能再更改元素的值，這種不可更動的特性，使得Tuple的資料結構簡單，使用Tuple儲存變數所佔用的記憶體空間比較小，執行速度也快很多。

此外，可以存放原始資料或一些重要的常數，避免程式在運行時被更動到。

Tuple的語法如下

    a = (123, 456)
    b = (1) # 要注意的是，如果Tuple只有一個元素，會被轉型
    type(b)
    # <class 'int'>
    
    b = (1,) # 故要在1後面加一個逗號
    type(b) 
    # <class 'tuple'>

## Set

一堆資料的集合，也就是一堆元素的集合，但跟前兩者的不同是，Set沒有順序的概念（沒有Index），就如同離散數學所說到的，集合是無序集。

Set的元素也是不可更動（Immutable），且因為沒有順序，故元素都是唯一且不可重複（Unique），要是插入同樣的元素進去，則會被合併。

例如

    a = {1,2,3,1}
    print(a) 
    # {1,2,3} 不會出現兩個1

因為Set的元素是不可更動的，因此List這種資料結構，也無法被放入到Set中。

此外，要搜尋Set的元素，可以直接使用

    2 in {1,2,3,4}
    # True

## Dict

Dictionary（字典）非常類似Set，但Dict的元素是有 Key:Value組成，就像是單字：解釋，因此可以用Key去找到對應的Value，因此key必須唯一且不重複（Unique），但是值可以重複。

就像是一間飲料店，同樣的一杯飲料只會有一種價格，不能標兩種價格，例如紅茶20元，就不會出現客人點了紅茶，結帳卻要付30元的狀況，但不同的飲料是可以賣相同價格的，如同紅茶綠茶都是20元（拜託別說紅茶有大杯小杯XD）

寫成程式碼：

    menu = {'牛奶':40,'紅茶':20, '拿鐵':50, '綠茶':20}

當客人點了拿鐵，可以直接使用下列方法得到價格

    print(menu['拿鐵'])
    # 50

此外，Dict具有Hash Table的特性，相同資料的Hash 值會相同，但是在Dict中，每個元素的Key都不一樣，故在Hash時不會發生碰撞，因此在Dict中找某個元素時，搜尋時間會是O（1）!

找的語法如同List，但搜尋時間為O（1）。

    '紅茶' in menu
    True

## String

字串竟然也是屬於一種有順序的資料結構！訝異吧？

操作方式類似List，但其元素是不可改變的

    a = '12345'
    a[1] # '1'
    a[1] = 4 
    # TypeError: 'str' object does not support item assignment
    a[:2] #  '12'

如果想要改變字串內容，一般來說都會直接Assign到變數或者覆蓋原本的字串

    a = '12345'
    a = a[:2]+'9'+a[2:] 
    print(a) # '129345'

到目前為止，只是大致介紹Python內建的資料結構，接下來是一些觀念釐清，也是這篇文我最想提的部份，但是在釐清觀念以前，想再整理一下上述資料結構的特性

無序集：set, dictionary

有序集：String, list, tuple

不可改變： set, dict, tuple, String

可改變：list

## Function和Method的差別

#### Function

Python具有許多內建的Function，像是 len(), max(), min()，使用上也很直覺，也不會改變到資料結構的內容

    a = [4,2,1,3]
    len(a) # 4
    min(a) # 1
    max(a) # 4
    sorted(a) # [1,2,3,4]
    reversed(a) # [4,3,2,1]

其中有趣的為 sorted() 和 reversed() ，這兩個都是在回傳新的List。

#### Method

Method就是資料結構（類別）專有的Method，所以String、List、Tuple、Set、Dict各自有其專屬的Method，為什麼要專屬呢？因為這些資料結構的特性不一樣，所以需要各自開發專屬的Method。

以sorted()和sort()為例子來說，sorted回通用的Function，可用在很多的資料結構上（String、List、Tuple、Set、Dict），但sort()為List專屬的method，因為sort()會對 List本身做就地排序，如同下方程式碼所示

    a = [4,2,1,3]
    b = sorted(a) # 會回傳一個List為 [1,2,3,4]
    print(b) # [1,2,3,4]
    print(a) # [4,2,1,3]
    b = a.sort() # 會將List a就地排序，並不會回傳
    print(b) # (空值，沒有回傳，所以b的值為空）
    print(a) # [1,2,3,4]

但是Tuple就沒有sort的Method，因為Tuple具有不可更動的特性，所以沒辦法做就地排序。而Dict和Set是無序集，就地排序毫無意義。

所以才會看到sorted()和sort()這種容易混淆的method，但仔細深入後，會發現細節藏在魔鬼裡

PS：以上所說的資料結構，都是屬於類別的一種，所以Method也可以說是類別裡的方法 （但不一定是 Class Method，可能是Instance Method，端看此Class如何封裝的）

備註：

參考「Python 技術者們 ： 實踐！ 帶你一步一腳印由初學到精通 」，非常感謝此書作者：施威銘研究室。

以前筆者沒有仔細的去研究Python，近期才買一本書來細細讀，才發現Python雖然入門門檻極低，但天花板很高，蘊含了非常多的細節，故將一些有意思的部份整理出來，Po在Medium上，希望能幫助更多人，

如果對此書有興趣，歡迎去購買唷！（絕對沒業配，也並非是研究室一員）
