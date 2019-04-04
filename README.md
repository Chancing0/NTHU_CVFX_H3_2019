# NTHU_CVFX_H3_2019

# NTHU_CVFX_HomeWork3_Team20



# Outline

**1.Model**

**2.Generate images with GANPaint**

**3.GAN dissection**

**4.other method**

**5.Compare&Conclusion**

## **1.Model**

研究人員的主要目標是分析如何通過GAN生成器的內部表徵
![](https://i.imgur.com/teeey2i.png)
通過剖析（dissection）來表徵單元
![](https://i.imgur.com/6lB4MsO.png)
使用乾預（intervention）測量因果關係
該模型可以將輸入圖像分割為336個物體類，29個大物體和25個材質類。為了進一步識別專門用於對象部件的單元，我們將每個對象類c擴展為另外的對象部件類ct，cb，cl和cr，分別表示連接組件的邊界框的頂部，底部，左半部分或右半部分.

## **2.Generate images with GANPaint**


|                                      | tree                                 | door                                   | cloud                                | dome                                 |
|--------------------------------------|--------------------------------------|----------------------------------------|--------------------------------------|--------------------------------------|
| ![](https://i.imgur.com/OIeyXKi.png) | ![](https://i.imgur.com/XuUAeVY.png) | ![](https://i.imgur.com/JPwtvPa.png)   | ![](https://i.imgur.com/KQejUBi.png) | ![](https://i.imgur.com/4lQSnMk.png) |
| ![](https://i.imgur.com/2yngK5A.png) | ![](https://i.imgur.com/cfa0BX4.png) | ![](https://i.imgur.com/CcKvf3L.png)   | ![](https://i.imgur.com/LGOCn6R.png) | ![](https://i.imgur.com/EdS8isA.png) |
| ![](https://i.imgur.com/sB34prn.png) | ![](https://i.imgur.com/xCz9lFn.png) | ![](https://i.imgur.com/A9MNzAH.png)   | ![](https://i.imgur.com/djr5ua2.png) | ![](https://i.imgur.com/BOs70TY.png) |








## **3. GAN dissection**

我們比較layer2和layer4的區別，因為我們使用layer7和layer14的時候，圖片有時候一點變化都沒有，於是採用2和4.
對於第一個表格，我們用**No.48**這張圖，分別設定grass，building，tree為想要去除的unit，分別設定50，100，200，500個units看生成出來的成果。


|     ![](https://i.imgur.com/QQoGgOV.png)            | ablate 50ablate  un unitsits                                  | ablate 100 units                                  | ablate 200 units                                  | ablate 500 units                                  |
|-----------------|--------------------------------------|--------------------------------------|--------------------------------------|--------------------------------------|
| layer2 grass    | ![](https://i.imgur.com/TbqRJrW.png) | ![](https://i.imgur.com/ppI5un6.png) | ![](https://i.imgur.com/9KQzQk6.png) | ![](https://i.imgur.com/3mvkkyE.png) |
| layer4 grass    | ![](https://i.imgur.com/8Gp8rbY.png) | ![](https://i.imgur.com/gdjKKlJ.png) | ![](https://i.imgur.com/jtc4KCO.png) | ![](https://i.imgur.com/GoMQ31q.png) |
| layer2 building | ![](https://i.imgur.com/yE6MTMn.png) | ![](https://i.imgur.com/9eyKtgM.png) | ![](https://i.imgur.com/JR9viJb.png) | ![](https://i.imgur.com/AA3zEeq.png) |
| layer4 building | ![](https://i.imgur.com/YiG0iDs.png) | ![](https://i.imgur.com/7HxeAwb.png) | ![](https://i.imgur.com/92Fiqd8.png) | ![](https://i.imgur.com/0x1T3Vv.png) |
| layer2 tree     | ![](https://i.imgur.com/B6qOxNA.png) | ![](https://i.imgur.com/fphSYW4.png) | ![](https://i.imgur.com/oPk4Ijj.png) | ![](https://i.imgur.com/yTuE6N1.png) |
| layer4 tree     | ![](https://i.imgur.com/hn6GfzZ.png) | ![](https://i.imgur.com/rO6amSx.png) | ![](https://i.imgur.com/4k1BN01.png) | ![](https://i.imgur.com/NQeyIvW.png) |


選用**No.87**圖片，設定 sky,building,tree 為屏蔽對象，一樣使用 50，100，200，500為屏蔽數量。

|       ![](https://i.imgur.com/2aYo7LQ.png)          | ablate 50 units                                  | ablate 100 units                                  | ablate 200 units                                  | ablate 500 units                                  |
|-----------------|--------------------------------------|--------------------------------------|--------------------------------------|--------------------------------------|
| layer2 sky      | ![](https://i.imgur.com/I4YAW5I.png) | ![](https://i.imgur.com/RfUhVUC.png) | ![](https://i.imgur.com/oML8HqL.png) | ![](https://i.imgur.com/736Gm1t.png) |
| layer4 sky      | ![](https://i.imgur.com/UoFoA2Y.png) | ![](https://i.imgur.com/6Mwecvf.png) | ![](https://i.imgur.com/AeqaDSi.png) | ![](https://i.imgur.com/g8SYhjf.png) |
| layer2 building | ![](https://i.imgur.com/gbsF9X1.png) | ![](https://i.imgur.com/4kcjMgJ.png) | ![](https://i.imgur.com/rqCZff4.png) | ![](https://i.imgur.com/iDV1fHJ.png) |
| layer4 building | ![](https://i.imgur.com/pWK1rvb.png) | ![](https://i.imgur.com/Goks1TE.png) | ![](https://i.imgur.com/ENCUUOW.png) | ![](https://i.imgur.com/C61B4lT.png) |
| layer2 tree     | ![](https://i.imgur.com/qjs6u9G.png) | ![](https://i.imgur.com/E9mSgtM.png) | ![](https://i.imgur.com/TxK5qR9.png) | ![](https://i.imgur.com/2MvKOOT.png) |
| layer4 tree     | ![](https://i.imgur.com/eONdx9J.png) | ![](https://i.imgur.com/R6Efi1W.png) | ![](https://i.imgur.com/4PxgUny.png) | ![](https://i.imgur.com/es4ticx.png) |

-----

使用interactiva 模式


|                    | ablate 50 units                                  | ablate 100 units                                  | ablate 200 units                                  | ablate 500 units                                  |
|--------------------|--------------------------------------|--------------------------------------|--------------------------------------|--------------------------------------|
| layer2 sky -> wall | ![](https://i.imgur.com/Zmgxom3.png) | ![](https://i.imgur.com/fBbeNaG.png) | ![](https://i.imgur.com/VFkDMK0.png) | ![](https://i.imgur.com/1oUDnGF.png) |
| layer4 sky -> wall | ![](https://i.imgur.com/JrdflZ5.png) | ![](https://i.imgur.com/BpqH1s3.png) | ![](https://i.imgur.com/DteNZY6.png) | ![](https://i.imgur.com/o7AwubU.png) |


|                         | ablate 50 units                                  | ablate 100 units                                  | ablate 200 units                                  | ablate 500 units                                  |
|-------------------------|--------------------------------------|--------------------------------------|--------------------------------------|--------------------------------------|
| layer2 building -> door | ![](https://i.imgur.com/K4b91So.png) | ![](https://i.imgur.com/D2x90nh.png) | ![](https://i.imgur.com/vdntsdU.png) | ![](https://i.imgur.com/PnGDyAY.png) |
| layer4 building -> door | ![](https://i.imgur.com/MkUbtqB.png) | ![](https://i.imgur.com/VzRMkP0.png) | ![](https://i.imgur.com/PJQOp2Y.png) | ![](https://i.imgur.com/wH8B12w.png) |



# **4. other method**
## **Inpainting**

|           Mask              | ![](https://i.imgur.com/hzrEMRo.png)| ![](https://i.imgur.com/reaDKje.png)| ![](https://i.imgur.com/cOQRxBD.png)| ![](https://i.imgur.com/ko0KZMK.png)|
|-------------------------|--------------------------------------|--------------------------------------|--------------------------------------|--------------------------------------|
| ![](https://i.imgur.com/8NtGIRD.png)| ![](https://i.imgur.com/hVo8Ap2.png) | ![](https://i.imgur.com/iKDuYPC.png) | ![](https://i.imgur.com/tzGrDo4.png) | ![](https://i.imgur.com/aPBH3kt.png) |


|            Mask           | ![](https://i.imgur.com/Ck1NpNY.png)| ![](https://i.imgur.com/Xg7xSjr.png)| ![](https://i.imgur.com/CueXhDF.png)| ![](https://i.imgur.com/RxV88P1.png)|
|-------------------------|--------------------------------------|--------------------------------------|--------------------------------------|--------------------------------------|
| ![](https://i.imgur.com/w30Qdsc.jpg)| ![](https://i.imgur.com/dzhoGqr.png) | ![](https://i.imgur.com/K9UqVAO.png) | ![](https://i.imgur.com/RQYaUni.png) | ![](https://i.imgur.com/us2VjYa.png)|


|           Mask         | ![](https://i.imgur.com/yQ36VUa.png)| ![](https://i.imgur.com/GmWlpPM.png)| ![](https://i.imgur.com/sJQCQjM.png)| ![](https://i.imgur.com/MqFbkL5.png)|
|-------------------------|--------------------------------------|--------------------------------------|--------------------------------------|--------------------------------------|
| ![](https://i.imgur.com/DDvgB3E.png) | ![](https://i.imgur.com/PokQ7EB.png) | ![](https://i.imgur.com/TjXgvWS.png) | ![](https://i.imgur.com/YG8fKwJ.png) | ![](https://i.imgur.com/YTfDrhz.png) |

|             Mask       | ![](https://i.imgur.com/is4T09H.png)| ![](https://i.imgur.com/Uof1WPJ.png)| ![](https://i.imgur.com/t5jjbz2.png)| ![](https://i.imgur.com/3HhQ46B.png)|
|-------------------------|--------------------------------------|--------------------------------------|--------------------------------------|--------------------------------------|
| ![](https://i.imgur.com/ASTFrih.png)| ![](https://i.imgur.com/touABAi.png) | ![](https://i.imgur.com/c0fMIxq.png) | ![](https://i.imgur.com/HliXyrx.png) | ![](https://i.imgur.com/6ijHY2T.png) |


----
----

## **5.Compare&Conclusion**


Conclusion:
   對於high layer的內容，在實踐中表現的並不突出。在編號48的圖片中，layer4的表現會比layer2更保守。編號87的圖片上則相反，layer2實際操作上並沒有什麼很大的變化，反倒是layer4效果更佳。



<br/><br/>


