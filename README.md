# YOLO to CoreML

**目標: 訓練自己的YOLO model並轉成iOS可以使用的coreML model。**

## Agenda

-  先認識基本的工具
	- [darknet](#1)
	- [darkflow](#2)
	- [tf-coreml](#3)

-  流程
	- [1. 安裝 darknet](#4)
	- [2. 安裝 darkflow]()
	- [3. 準備自己的數據]()
	- [4. 利用darkflow針對自己的數據進行客製化訓練]()
	- [5. 利用darkflow將客製化的模型輸出成tensorflow]()
	- [6. 利用tf-coreml將tensorflow轉成CoreML]()

<h2 id="1">darknet</h2>

- [官方網頁](https://pjreddie.com/darknet/)
- [github](https://github.com/pjreddie/darknet)

- darknet主要功用
	- 有很多已經訓練好現成可以用的模型。
	- 這些模型都分別被拆成兩種檔案.cfg跟.weight。
		- .cfg檔案: 定義了神經網路的架構。
			- 例如，yolov3.cfg就是對應了yolov3的神經網路結構。
		- .weight檔案: 訓練好的權重參數。
			- 權重參數是先人辛苦訓練出來的精華，神經網路的架構越複雜，檔案就會越大。
			- 例如，我決定使用YOLO_V3當作我的模型，你會發現在cfg的目錄有一個yolov3.cfg檔案，再去官網下載對應的yolov3.weight。

**到這裡，只要先了解.cfg跟.weight是做啥的就可以了。如果你把darknet clone下來後，觀察darknet的目錄，會發現一個cfg的目錄，裡面放了很多.cfg檔。**	

<h2 id="2">darkflow</h2>	

- [github](https://github.com/thtrieu/darkflow)

- darkflow主要功用
	- 可以直接載入darknet已經訓練好的模型。
	- 可以重新進行訓練這些模型(ex. 客製化自己想要的模型)
	- 可以輸出tensorflow graph的模型(.pb)

**darkflow在整個tutorial中扮演很重要的角色，因為客製化的模型就是在這裡執行。**


<h2 id="3">tf-coreml</h2>	

- [github](https://github.com/tf-coreml/tf-coreml)

- tf-coreml主要功用
	- 將darkflow產生的Tensorflow graph的模型(.pb)變成coreML模型(.mlmodel)。

**目前，應該有大概猜到流程該怎麼做了，先從darknet選定要用的模型.cfg跟.weight，然後將這兩個東西丟到darkflow，並搭配我們自己的數據，進行客製化的模型訓練，最後再利用tf-coreml轉成iOS可以用的model。EASY !!**


<h2 id="4">1. 安裝 darknet</h2>	
```
// 下載
git clone https://github.com/pjreddie/darknet.git
// 進入目錄
cd darknet
// 安裝
make

```
觀察darknet的目錄，會發現一個cfg的目錄，裡面放了很多.cfg檔。

![1](https://github.com/htaiwan/yolo_coreml/blob/master/Assets/1.png)

安裝遇到的雷
	
- ModuleNotFoundError: No module named 'cv2' -> conda install -c conda-forge opencv



