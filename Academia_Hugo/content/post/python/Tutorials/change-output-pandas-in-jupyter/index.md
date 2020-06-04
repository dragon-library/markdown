---
title:   ปรับเปลี่ยนการแสดงผล pandas ใน jupyter
subtitle : นอกจากแค่ใช้แสดงผลเป็นตารางได้ธรรมดาแล้ว การแสดงผลของเดตาเฟรมใน jupyter นั้นยังสามารถปรับแต่งใส่ลูกเล่นต่างๆได้ด้วย  สำหรับบทความนี้จะพูดถึงการปรับเปลี่ยนรูปแบบการแสดงผล โดยใช้เมธอดต่างๆที่อยู่ภายในตัวเดตาเฟรม 
summary: นอกจากแค่ใช้แสดงผลเป็นตารางได้ธรรมดาแล้ว การแสดงผลของเดตาเฟรมใน jupyter นั้นยังสามารถปรับแต่งใส่ลูกเล่นต่างๆได้ด้วย  สำหรับบทความนี้จะพูดถึงการปรับเปลี่ยนรูปแบบการแสดงผล โดยใช้เมธอดต่างๆที่อยู่ภายในตัวเดตาเฟรม 

authors:
    - admin
tags: ['Jupyter']
categories: ['Tutorials','Pandas']
date: "2020-06-02T00:00:00Z"
lastMod: "2020-06-02T00:00:00Z"
featured: true
draft: false
image:
  caption: ""
  focal_point: ""
  preview_only: true
---


>เขียนเมื่อ 2016/10/23 12:11

ในเนื้อหา  [pandas เบื้องต้นบทที่ ๒](https://phyblas.hinaboshi.com/yancham02)  ได้มีเขียนถึงไปว่าเดตาเฟรมใน jupyter จะแสดงผลในลักษณะตารางที่สร้างขึ้นจากโค้ด html  
  
เกี่ยวกับการติดตั้งและใช้งาน jupyter มีคนเขียนถึงไว้แล้วอ่านได้ใน  
[https://python3.wannaphong.com/2015/09/ติดตั้งเครื่องมือ-python.html](https://python3.wannaphong.com/2015/09/%E0%B8%95%E0%B8%B4%E0%B8%94%E0%B8%95%E0%B8%B1%E0%B9%89%E0%B8%87%E0%B9%80%E0%B8%84%E0%B8%A3%E0%B8%B7%E0%B9%88%E0%B8%AD%E0%B8%87%E0%B8%A1%E0%B8%B7%E0%B8%AD-python.html)  
[http://naiwaen.debuggingsoft.com/2016/08/jupyter-with-python-part2](http://naiwaen.debuggingsoft.com/2016/08/jupyter-with-python-part2)  
  
นอกจากแค่ใช้แสดงผลเป็นตารางได้ธรรมดาแล้ว การแสดงผลของเดตาเฟรมใน jupyter นั้นยังสามารถปรับแต่งใส่ลูกเล่นต่างๆได้ด้วย  
  
สำหรับบทความนี้จะพูดถึงการปรับเปลี่ยนรูปแบบการแสดงผล โดยใช้เมธอดต่างๆที่อยู่ภายในตัวเดตาเฟรม  
  
เนื้อหาแปลและตัดต่อเรียบเรียงจาก  [http://sinhrks.hatenablog.com/entry/2015/11/22/202640](http://sinhrks.hatenablog.com/entry/2015/11/22/202640)  
  
ลองสร้างเดตาเฟรมขึ้นมาอันหนึ่งเพื่อใช้เป็นตัวอย่าง โดยประกอบด้วยคอลัมน์ที่เป็นตัวเลข แล้วก็ที่เป็นตัวหนังสือ
```py
import  pandas  as  pd  
pokemon = pd.DataFrame([  
['ฟุชิงิดาเนะ','พืช/พิษ',0.7,6.9],  
['ฟุชิงิโซว','พืช/พิษ',1.0,13.0],  
['ฟุชิงิบานะ','พืช/พิษ',2.4,155.5],  
['ฮิโตคาเงะ','ไฟ',0.6,8.5],  
['ลิซาร์โด','ไฟ',1.1,19.0],  
['ลิซาร์ดอน','ไฟ/บิน',1.7,101.5],  
['เซนิงาเมะ','น้ำ',0.5,9.0],  
['คาเมล','น้ำ',1.0,22.5],  
['คาเม็กซ์','น้ำ',1.6,101.1]],  
columns=['สายพันธุ์','ชนิด','ส่วนสูง','น้ำหนัก'],  
index=[1,2,3,4,5,6,7,8,9])  
pokemon
```
  
โดยปกติจะได้ตารางเรียบๆออกมาแบบนี้  
  
![](https://phyblas.hinaboshi.com/rup/nayuki/ayu/b01.png)  
  
การปรับการแสดงผลนั้นทำได้โดยพิมพ์คำว่า .style ต่อท้ายตัวแปรที่เก็บเดตาเฟรมอยู่ แล้วตามด้วยเมธอดที่ต้องการ  
  
ในที่นี้จะยกตัวอย่างแค่ส่วนหนึ่งขึ้นมาลองใช้ ได้แก่  
```py
.style.set_properties() ปรับค่าการแสดงผลทุกช่องตารางเหมือนกัน  
.style.apply() ปรับค่าการแสดงผลโดยแยกแต่ละแถวหรือแต่ละคอลัมน์ตามค่าโดยกำหนดด้วยฟังก์ชัน  
.style.applymap() ปรับค่าการแสดงผลโดยแยกตามค่าของแต่ละช่องโดยกำหนดด้วยฟังก์ชัน  
.style.highlight_max() เติมสีให้ช่องที่ค่าสูงสุด  
.style.highlight_min() เติมสีให้ช่องที่ค่าต่ำสุด  
.style.highlight_null() เติมสีให้ช่องที่ค่าเป็น NaN  
.style.background_gradient() เปลี่ยนสีฉากหลังแต่ละช่องตามค่าตัวเลข  
.style.bar() แสดงแผนภูมิแท่งขึ้นภายในตารางตามค่าตัวเลข  
  ```
เริ่มจาก style.set_properties คำสั่งนี้จะปรับการแสดงผลโดยใช้โค้ด css หากใครใช้ css เป็นอยู่แล้วก็สามารถปรับแต่งอะไรต่างๆได้ตามใจชอบโดยไม่ต้องจำอะไรเพิ่มเติม  
  
ค่าคุณสมบัติต่างๆเขียนในรูปแบบ .style.set_properties(คุณสมบัติ1=ค่า1,คุณสมบัติ2=ค่า2,...=...) แบบนี้ได้  
  
ตัวอย่าง ลองเปลี่ยนสีอักษรในตาราง
```py
pokemon.style.set_properties(color='#aa7711')
```
  
![](https://phyblas.hinaboshi.com/rup/nayuki/ayu/b02.png)  
  
เพียงแต่ว่าหากชื่อมีขีด - อยู่ด้วยจะใช้วิธีนี้ไม่ได้ ต้องใช้การเขียนในรูปดิกชันนารีแทน โดยใส่ดอกจันสองอันนำหน้า .style.set_properties(**{คุณสมบัติ1:ค่า1,คุณสมบัติ2:ค่า2,...:...}) แบบนี้  
  
ตัวอย่าง
```py
pokemon.style.set_properties(**{'background-color':'#ff2266','color':'#11ff00','font-size':'20px'})
```
  
![](https://phyblas.hinaboshi.com/rup/nayuki/ayu/b03.png)  
  
การใช้ style.set_properties แบบนี้จะเป็นการเปลี่ยนทุกแถวทุกหลักเหมือนกันหมด แต่ถ้าต้องการกำหนดรูปแบบโดยขึ้นอยู่กับค่าในแต่ละช่องก็ให้ใช้ style.applymap  
  
ก่อนอื่นต้องสร้างฟังก์ชันที่ให้ค่าคืนกลับเป็นโค้ด css จากนั้นจึงนำฟังก์ชันนี้ไปใช้ style.applymap ฟังก์ชันจะถูกเรียกใช้โดยมีค่าของแต่ช่องตารางเป็นอาร์กิวเมนต์  
  
ตัวอย่าง
```py
def  f(x):  
if(type(x)==str):  
return  'color: #00aa00'  
elif(x>50):  
return  'color: #ff0000'  
else:  
return  ''  
pokemon.style.applymap(f)
```
  
![](https://phyblas.hinaboshi.com/rup/nayuki/ayu/b04.png)  
  
แต่หากต้องการแยกเป็นแต่ละคอลัมน์ให้ใช้ style.apply เพียงแต่ว่าค่าที่ฟังก์ชันคืนกลับมาจะต้องเป็นลิสต์ของโค้ด css ที่มีจำนวนสมาชิกเท่ากับจำนวนแถว  
  
ตัวอย่าง
```py
def  f(x):  
z =  'color: #110099; font-size: %dpx'%(50*len(str(x.max()))**-0.5)  
return  [z]*len(x)  
pokemon.style.apply(f)
```
  
![](https://phyblas.hinaboshi.com/rup/nayuki/ayu/b06.png)  
  
หากต้องการแยกเป็นแต่ละแถวก็ใช้ style.apply แล้วใส่ axis=1 เช่น
```py
def  f(x):  
if('พืช'  in  x['ชนิด']):  
return  ['','color: #00ee00','','']  
if('ไฟ'  in  x['ชนิด']):  
return  ['','color: #ee0000','','']  
if(x['ชนิด']=='น้ำ'):  
return  ['','color: #0000ee','','']  
pokemon.style.apply(f,axis=1)
```
  
![](https://phyblas.hinaboshi.com/rup/nayuki/ayu/b05.png)  
  
หากต้องการระบายสีช่องที่มีค่าสูงสุดหรือต่ำสุดให้ใช้ style.highlight_max หรือ style.highlight_min โดยระบุค่าสีที่ต้องการด้วยคีย์เวิร์ด color คำสั่งนี้จะมีผลเฉพาะคอลัมน์ที่เป็นค่าตัวเลขเท่านั้น  
  
ตัวอย่าง
```py
pokemon.style.highlight_max(color='#aaaaff')
```
  
![](https://phyblas.hinaboshi.com/rup/nayuki/ayu/b07.png)  
  
สามารถใส่ซ้อนกันได้หากต้องการแสดงทั้งค่า max และ min
```py
pokemon.style.highlight_max(color='#cc0000').highlight_min(color='#00cc00')
```
  
![](https://phyblas.hinaboshi.com/rup/nayuki/ayu/b08.png)  
  
ส่วน style.highlight_null จะระบายสีช่องที่ค่าเป็น None หรือ NaN
```py
pokemon.loc[10] = [None]*4  
pokemon.style.highlight_null()
```
  
![](https://phyblas.hinaboshi.com/rup/nayuki/ayu/b09.png)  
  
สำหรับ style.background_gradient จะเป็นการใส่สีให้แต่ละช่องของแต่ละแถงโดยเรียงตามค่าตัวเลขโดยเรียงสีตามคัลเลอร์แม็ป ให้ใส่คัลเลอร์แม็ปที่ต้องการลงในคีย์เวิร์ด cmap (เกี่ยวกับคัลเลอร์แม็ปได้อธิบายไว้ใน  [numpy & matplotlib เบื้องต้นบทที่ ๒๔](https://phyblas.hinaboshi.com/numa24))  

```py
pokemon.style.background_gradient(cmap='summer')
```
  
![](https://phyblas.hinaboshi.com/rup/nayuki/ayu/b10.png)  
  
ปกติสีจะถูกใส่ให้กับทุกคอลัมน์ที่เป็นค่าตัวเลข แต่หากต้องการให้ใส่แค่บางคอลัมน์ก็ทำได้โดยใช้คีย์เวิร์ด subset แล้วระบุเฉพาะชื่อคอลัมน์ที่ต้องการ

```py
pokemon.style.background_gradient(cmap='autumn',subset=['น้ำหนัก'])
```
  
![](https://phyblas.hinaboshi.com/rup/nayuki/ayu/b11.png)  
  
สุดท้าย style.bar จะเป็นการสร้างแท่งสีขึ้นมาเป็นฉากหลังในตาราง โดยมีความยาวตามค่า  
  
ตัวอย่าง

```py
pokemon.style.bar(color='#aaffaa')
```
  
![](https://phyblas.hinaboshi.com/rup/nayuki/ayu/b12.png)  
  
การแสดงผลของตารางทั้งหมดมาจากโค้ด html ซึ่งหากต้องการได้ตัวโค้ด html ออกมาในรูปสายอักขระทันทีก็ให้ใช้เมธอด render() พิมพ์ต่อท้ายไปอีก  
  
เช่น

```py
pokemon.style.bar(color='#aaffaa').render()
```
  
แบบนี้จะได้ตัวโค้ด html มา   
  
  
นอกจากนี้แล้วยังมีความสามารถอื่นๆที่ทำได้อีกมากใน jupyter ที่ไม่ได้กล่าวถึงในนี้ สำหรับผู้ที่สนใจก็ไปลองๆใช้และศึกษากันดูเพิ่มเติมได้

Reference : [https://phyblas.hinaboshi.com/20161023](https://phyblas.hinaboshi.com/20161023)