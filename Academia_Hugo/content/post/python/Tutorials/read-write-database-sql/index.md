---
title:   การอ่านเขียนข้อมูลจากฐานข้อมูล sql
subtitle : ฐานข้อมูล sql เป็นรูปแบบการเก็บข้อมูลที่ใช้กันอย่างกว้างขวาง การเก็บข้อมูลของ sql นั้นมีลักษณะเป็นตารางข้อมูลเป็นแถวๆ คล้ายกับ pandas 
summary: pandas มีคำสั่งที่ช่วยให้ติดต่อกับฐานข้อมูล sql ได้อย่างง่ายดายขึ้น โดยสามารถเอาตารางจาก pandas เขียนลงใน sql และอ่านตารางจาก sql เข้ามาเป็นตารางใน pandas  ความสามารถส่วนใหญ่ในส่วนนี้จะใช้กับมอดูล sqlalchemy เป็นหลัก ดังนั้นจำเป็นต้องติดตั้งมอดูล sqlalchemy ด้วย 

authors:
    - admin
tags: ['Database','SQL','sqlalchemy']
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



> เขียนเมื่อ 2020/06/02 19:13

ฐานข้อมูล sql เป็นรูปแบบการเก็บข้อมูลที่ใช้กันอย่างกว้างขวาง การเก็บข้อมูลของ sql นั้นมีลักษณะเป็นตารางข้อมูลเป็นแถวๆ คล้ายกับ pandas  
  
pandas มีคำสั่งที่ช่วยให้ติดต่อกับฐานข้อมูล sql ได้อย่างง่ายดายขึ้น โดยสามารถเอาตารางจาก pandas เขียนลงใน sql และอ่านตารางจาก sql เข้ามาเป็นตารางใน pandas  ความสามารถส่วนใหญ่ในส่วนนี้จะใช้กับมอดูล sqlalchemy เป็นหลัก ดังนั้นจำเป็นต้องติดตั้งมอดูล sqlalchemy ด้วย  
  
เกี่ยวกับการใช้ sqlalchemy อ่านได้ใน  [https://phyblas.hinaboshi.com/20200529](https://phyblas.hinaboshi.com/20200529)  
  
เพียงแต่ว่าก็อาจไม่ต้องเรียกใช้ sqlalchemy โดยตรง แค่มีลงมอดูล sqlalchamy ไว้ก็สามารถใช้ความสามารถนี้ได้แล้ว  
  
ฐานข้อมูล sql ยังแบ่งออกเป็นหลายแบบ เช่น sqlite, posgresql, mysql ซึ่ง sqlalchemy ก็รองรับฐานข้อมูลหลายชนิด ซึ่งก็ทำให้ใช้ใน pandas ได้ด้วยเช่นกัน ในที่นี้จะใช้ sqlite ซึ่งเป็นฐานข้อมูล sql แบบที่ง่ายที่สุด มีติดตัวอยู่ตั้งแต่แรกไม่ต้องติดตั้งเพิ่ม  เมื่อมีตารางข้อมูลเก็บอยู่ในเดตาเฟรมแล้วต้องการบันทึกลงฐานข้อมูล sql สามารถทำได้โดยใช้เมธอด .to_sql() จากตัวเดตาเฟรมนั้น  
  
การใช้คำสั่งนี้มีการเขียนอยู่หลายวิธี ที่ง่ายที่สุดก็คือใส่ชื่อตารางและตามด้วยชื่อตารางที่เก็บข้อมูลนั้นอยู่  วิธีที่ง่ายที่สุดคือแค่ใส่ชื่อตาราง แล้วตามด้วยชื่อตัวฐานข้อมูลที่จะเก็บตารางข้อมูลนั้นไว้  

```python
df.to_sql(ชื่อตาราง,ชื่อฐานข้อมูล)
```
  
ตัวอย่างการใช้  

```python
import pandas as pd

p = {'สายพันธุ์':['ซันกูส','ฮาบุเนก','ลูนาโทน'],
     'ส่วนสูง':[1.3,2.7,1],
     'น้ำหนัก':[40.3,52.5,168]}
pokedf = pd.DataFrame(p,index=[335,336,337])
pokedf.to_sql('pokemon','sqlite:///pkdata.db')
```

  
ในที่นี้ใช้กับฐานข้อมูล sqlite ในส่วนของชื่อฐานข้อมูลจะเขียนเป็น  `'sqlite:///ชื่อไฟล์'`  แบบนี้  อนึ่ง เดิมทีแล้ว .to_sql() ควรจะใช้กับตัวออบเจ็กต์เชื่อมต่อ ซึ่งใน sqlalchemy เรียกว่า engine  หากเขียนแบบเต็มๆตั้งแต่ขั้นตอนการสร้าง engine ก็อาจเขียนแบบนี้  

```python
import sqlalchemy

engine = sqlalchemy.create_engine('sqlite:///pkdata.db')
pokedf.to_sql('pokemon',engine)
```

  
เพียงแต่ว่าสามารถเขียนย่อเป็นแบบใส่แค่ชื่อฐานข้อมูลไปโดยตรงก็ได้ ดังนั้นจึงสะดวกกว่ามาก ไม่จำเป็นต้อง import sqlalchemy มาโดยตรงเลยด้วย  ส่วนการอ่านข้อมูลจากตารางใน sql ทำได้โดยฟังก์ชัน pd.read_sql_table() วิธีใช้ก็เช่นเดียวกับตอนเขียนข้อมูลลง sql นั่นคือใส่ชื่อตารางกับชื่อฐานข้อมูล  

```python
df = pd.read_sql_table(ชื่อตาราง,ชื่อฐานข้อมูล)
```

  
ตัวอย่างเช่นถ้าต้องการอ่านข้อมูลที่บันทึกลงไปในฐานข้อมูลในตัวอย่างที่แล้ว  

```python
df = pd.read_sql_table('pokemon','sqlite:///pkdata.db')
print(df)
```
```
index	สายพันธุ์	ส่วนสูง	น้ำหนัก
0	335	ซันกูส	1.3	40.3
1	336	ฮาบุเนก	2.7	52.5
2	337	ลูนาโทน	1.0	168.0  
```
  
จากในตัวอย่างที่แล้วทั้งตอนเขียนและอ่านล้วนไม่ได้ใส่ตัวเลือกเสริมอะไรลงไปเลย ทุกอย่างจึงเป็นไปตามค่าตั้งต้น  
  
ซึ่งจะเห็นว่าตอนที่ใช้ .to_sql() นั้นตัวดัชนีก็ถูกเปลี่ยนเป็นคอลัมน์หนึ่งใน sql ไปด้วย โดยชื่อคอลัมน์ดัชนีก็จะกลายเป็นชื่อคอลัมน์ใน sql ด้วย  หากต้องการเปลี่ยนชื่อคอลัมน์ดัชนีใหม่อาจทำได้โดยใส่ในตัวเลือกเสริม index_label เช่น  
  

```python
pk = {'สายพันธุ์':['โซลร็อก','โดจ็อช'],
      'ส่วนสูง':[1.2,0.4],
      'น้ำหนัก':[154,1.9]}
index = pd.Series([338,339],name='หมายเลข')
pokedf = pd.DataFrame(pk,index=index)
pokedf.to_sql('pokemon','sqlite:///pkdt.db',index_label='id')
print(pd.read_sql_table('pokemon','sqlite:///pkdt.db'))
```

```
id	สายพันธุ์	ส่วนสูง	น้ำหนัก
0	338	โซลร็อก	1.2	154.0
1	339	โดจ็อช	0.4	1.9  
```
  
นอกจากนี้ถ้าหากไม่ได้ตั้งชื่อให้คอลัมน์ดัชนี แล้วก็ไม่ได้กำหนด index_label ก็จะถูกตั้งชื่อเป็น index โดยอัตโนมัติ  หากจะให้ทิ้งส่วนดัชนีไปเลยก็ใส่ตัวเลขเสริม index เป็น index=False  
  

```python
pk = {'สายพันธุ์':['นามาซึน','เฮย์งานิ'],
      'ส่วนสูง':[0.9,0.6],
      'น้ำหนัก':[23.6,11.5]}
pokedf = pd.DataFrame(pk,index=[340,341])
pokedf.to_sql('pokemon','sqlite:///pkdex.db',index=False)
print(pd.read_sql_table('pokemon','sqlite:///pkdex.db'))
```

```
 สายพันธุ์	ส่วนสูง	น้ำหนัก
0	นามาซึน	0.9	23.6
1	เฮย์งานิ	0.6	11.5
 ``` 

  
หากชื่อตารางที่ใส่ไปนั้นซ้ำกับที่มีอยู่ในฐานข้อมูลนั้นแล้ว ปกติจะเกิดข้อผิดพลาดขึ้น  
หากไม่ต้องการให้เป็นเช่นนั้น ก็อาจกำหนดไปในตัวเลือกเสริม if_exists เพิ่มเติม โดยถ้า id_exists='replace' ตารางเดิมจะหายไปแล้วเอาข้อมูลใหม่ใส่ลงไปแทน เช่นลองใส่ตารางเดิมซ้ำในฐานข้อมูลเดียวกับตัวอย่างที่แล้ว  

```python
pk = {'สายพันธุ์':['เนนดอล','ลีลีลา'],
      'ส่วนสูง':[1.5,1],
      'น้ำหนัก':[108,23.8]}
pokedf = pd.DataFrame(pk,index=[344,345])
pokedf.to_sql('pokemon','sqlite:///pkdex.db',if_exists='replace')
print(pd.read_sql_table('pokemon','sqlite:///pkdex.db'))
```
  
ได้  
```
index	สายพันธุ์	ส่วนสูง	น้ำหนัก
0	344	เนนดอล	1.5	108.0
1	345	ลีลีลา	1.0	23.8
```
  
จะเห็นว่าข้อมูลเก่าหายไปแล้วกลายเป็นข้อมูลใหม่  ตรงนี้ถ้าไม่ได้ใส่ หรือใส่ if_exists='fail' ก็จะขึ้นมาว่า  

```javascript
ValueError: Table 'pokemon' already exists.
```

  
นอกจากนี้ ถ้า id_exists='append' จะเป็นการเพิ่มข้อมูลเข้าไปในตารางที่มีอยู่แล้ว   เช่น ลองใส่ตารางเดิมซ้ำในฐานข้อมูลเดียวกับตัวอย่างที่แล้ว  

```python
pk = {'สายพันธุ์':['ชิซาริเกอร์','ยาจิลอน'],
      'ส่วนสูง':[1.1,0.5]}
pokedf = pd.DataFrame(pk,index=[342,343])
pokedf.to_sql('pokemon','sqlite:///pkdex.db',if_exists='append')
print(pd.read_sql_table('pokemon','sqlite:///pkdex.db'))
```

  
ได้  

```
index	สายพันธุ์	ส่วนสูง	น้ำหนัก
0	344	เนนดอล	1.5	108.0
1	345	ลีลีลา	1.0	23.8
2	342	ชิซาริเกอร์	1.1	NaN
3	343	ยาจิลอน	0.5	NaN
 ``` 
ข้อมูลที่ใส่ต่อเข้าไปนั้นควรจะมีคอลัมน์ซ้ำกับตารางเดิม หรือจะขาดไปบางคอลัมน์ก็ได้ ค่าที่ขาดจะว่างไว้ แต่ถ้าหากมีคอลัมน์ที่ไม่มีอยู่เดิมก็จะเกิดข้อผิดพลาด  สำหรับชนิดของข้อมูลนั้น ถ้าไม่ได้กำหนดอะไรก็จะเป็นไปตามชนิดของข้อมูลที่สัมพันธ์กับที่อยู่ในเดตาเฟรม  เช่น ตัวอย่างนี้ เมื่อไม่ได้กำหนด dtype ก็จะเป็นแบบนี้

```python
pk = {'สายพันธุ์':['มิโลคารอส','คาคุเรออน'],
      'ส่วนสูง':[6.2,1],
      'น้ำหนัก':[162.0,22.0]}
pokedf = pd.DataFrame(pk,pd.Series([350,352],name='เลข'))

pokedf.to_sql('pokemon','sqlite:///pkdex.db',if_exists='replace')
df = pd.read_sql_table('pokemon','sqlite:///pkdex.db',coerce_float=False)
print(df.values)
```

  
ได้  

```javascript
[[350 'มิโลคารอส' 6.2 162.0]
 [352 'คาคุเรออน' 1.0 22.0]]
```

  
แต่หากต้องการให้เปลี่ยนชนิดข้อมูลเป็นแบบที่ต้องการก็สามารถกำหนดได้โดยตัวเลือกเสริม dtype  การใส่ชนิดข้อมูลนั้นให้ใส่ในรูปของชนิดข้อมูล sqlalchemy (ต้อง import มาใช้)  จากตัวอย่างที่แล้ว ลองกำหนด dtype เข้าไปได้ดังนี้  

```python
import sqlalchemy

dtype = {'ส่วนสูง':sqlalchemy.String,
         'น้ำหนัก':sqlalchemy.Integer,
         'เลข':sqlalchemy.Float}

pokedf.to_sql('pokemon','sqlite:///pkdex.db',if_exists='replace',dtype=dtype)
df = pd.read_sql_table('pokemon','sqlite:///pkdex.db')
print(df.values)
```

  
ได้  

```javascript
[[350.0 'มิโลคารอส' '6.2' 162]
 [352.0 'คาคุเรออน' '1.0' 22]]
```

  
เวลาอ่านข้อมูลจาก sql ด้วย pd.read_sql_table() ก็มีตัวเลือกเสริมมากมายเพื่ออำนวยความสะดวกในการการกำหนดลักษณะการอ่าน  เช่น index_col ใช้กำหนดคอลัมน์ที่จะเป็นดัชนี ถ้าหากไม่กำหนดอะไรไปก็จะไม่มีคอลัมน์ไหนกลายเป็นดัชนี แล้วเป็นตัวเลข 0,1,2 ไป    

```python
pk = {'สายพันธุ์':['ฮินบาส','โปวาเลิน','คาเงะโบวซึ'],
      'ส่วนสูง':[0.6,0.3,0.6],
      'น้ำหนัก':[7.4,0.8,2.3]}
pokedf = pd.DataFrame(pk,pd.Series([349,351,353],name='เลข'))
pokedf.to_sql('pokemon','sqlite:///pkdex.db',if_exists='replace')

print(pd.read_sql_table('pokemon','sqlite:///pkdex.db'))
print(pd.read_sql_table('pokemon','sqlite:///pkdex.db',index_col='เลข'))
print(pd.read_sql_table('pokemon','sqlite:///pkdex.db',index_col='สายพันธุ์'))
```

  
ได้  

```
 เลข	สายพันธุ์	ส่วนสูง	น้ำหนัก
0	349	ฮินบาส	0.6	7.4
1	351	โปวาเลิน	0.3	0.8
2	353	คาเงะโบวซึ	0.6	2.3
```
```
 สายพันธุ์	ส่วนสูง น้ำหนัก เลข	 	 	 
349	ฮินบาส	0.6	7.4
351	โปวาเลิน	0.3	0.8
353	คาเงะโบวซึ	0.6	2.3
```

```

 	 เลข	ส่วนสูง	น้ำหนัก
สายพันธุ์	 	 	 
ฮินบาส	349	0.6	7.4
โปวาเลิน	351	0.3	0.8
คาเงะโบวซึ	353	0.6	2.3
```

ส่วนการเลือกเอาข้อมูลเฉพาะแค่บางคอลัมน์ทำได้โดยใส่ตัวเลือกเสริม columns  
  

```python
pk = {'สายพันธุ์':['ยูเรเดิล','อาโนปธ์','อาร์มัลโด'],
      'ส่วนสูง':[1.5,0.7,1.5],
      'น้ำหนัก':[60.4,12.5,68.2]}
pokedf = pd.DataFrame(pk,index=[346,347,348])
pokedf.to_sql('pokemon','sqlite:///pkdex.db',if_exists='replace')

print(pd.read_sql_table('pokemon','sqlite:///pkdex.db',columns=['index','สายพันธุ์']))
print(pd.read_sql_table('pokemon','sqlite:///pkdex.db',columns=['index','สายพันธุ์'],index_col='index'))
```

  
ได้  

```
 	index	สายพันธุ์
0	346	ยูเรเดิล
1	347	อาโนปธ์
2	348	อาร์มัลโด
 ``` 

```
	 	สายพันธุ์
index	 
346		ยูเรเดิล
347		อาโนปธ์
348		อาร์มัลโดแต่ 
```
pd.read_sql_table() นั้นไม่สามารถกำหนดเงื่อนไขให้ข้อมูลออกมาเฉพาะบางแถวได้ จะอ่านข้อมูลออกมาทุกแถวเสมอ (เหมือนการใส่ where ในโค้ด sql)  
  
ฟังก์ชันอีกตัวที่ใช้สำหรับอ่านข้อมูลคือ pd.read_sql_query() ซึ่งใช้เขียนโค้ด sql เพื่อสั่งอ่านข้อมูลเข้ามาโดยตรง  การจะใช้ฟังก์ชันนี้ได้จึงต้องรู้โค้ด sql ด้วยทำให้อาจใช้ยากกว่า แต่ข้อดีคือเขียนได้ยืดหยุ่นกว่า สามารถเขียน where เพื่อกำหนดเงื่อนไขได้ หรือเขียน order by เพื่อเรียงลำดับข้อมูลได้  การกำหนดคอลัมน์ที่จะใช้เป็นดัชนีก็ทำได้ด้วยการใส่ index_col เช่นกัน  
  
ตัวอย่าง  
  

```python
pk = {'สายพันธุ์':['จูเพ็ตตา','โยมาวารุ','ซามาโยวรุ','โทรปิอุส'],
      'ส่วนสูง':[1.1,0.8,1.6,2],
      'น้ำหนัก':[12.5,35,30.6,100]}
pokedf = pd.DataFrame(pk,index=[354,355,356,357])
pokedf.to_sql('pokemon','sqlite:///pkdex.db',if_exists='replace')

sql = 'select * from pokemon where น้ำหนัก>32'
print(pd.read_sql_query(sql,'sqlite:///pkdex.db'))
sql = 'select สายพันธุ์,น้ำหนัก from pokemon order by น้ำหนัก desc'
print(pd.read_sql_query(sql,'sqlite:///pkdex.db'))
sql = 'select * from pokemon'
print(pd.read_sql_query(sql,'sqlite:///pkdex.db',index_col='index'))
```

  
ได้  

```
 	index	สายพันธุ์	ส่วนสูง	น้ำหนัก
0	355	โยมาวารุ	0.8	35.0
1	357	โทรปิอุส	2.0	100.0
```
```
  	สายพันธุ์	น้ำหนัก
0	โทรปิอุส	100.0
1	โยมาวารุ	35.0
2	ซามาโยวรุ	30.6
3	จูเพ็ตตา	12.5 
```
```

 	สายพันธุ์	ส่วนสูง	น้ำหนัก
index	 	 	 
354	จูเพ็ตตา	1.1	12.5
355	โยมาวารุ	0.8	35.0
356	ซามาโยวรุ	1.6	30.6
357	โทรปิอุส	2.0	100.0
```

หากใน โค้ดมีการใช้เครื่องหมายคำถาม ? ซึ่งแทนตัวพารามิเตอร์ สามารถใส่ค่าลงไปได้โดยเติมลิสต์ของพารามิเตอร์ที่ต้องการแทนใส่ในคีย์เวิร์ด params เช่น  

```python
pk = {'สายพันธุ์':['ชิรีน','อับโซล','โซนาโน'],
      'ส่วนสูง':[0.6,1.2,0.6],
      'น้ำหนัก':[1,47,14]}
pokedf = pd.DataFrame(pk,pd.Series([358,359,360],name='เลข'))
pokedf.to_sql('pokemon','sqlite:///pkdex.db',if_exists='replace')

sql = 'select * from pokemon where สายพันธุ์==?'
print(pd.read_sql_query(sql,'sqlite:///pkdex.db',params=['ชิรีน']))
```

  
ได้  

```
		 เลข	สายพันธุ์	ส่วนสูง	น้ำหนัก
0		358		ชิรีน		0.6	1
```
  
หรือใส่ในรูปของตัวแปรที่ชื่อขึ้นต้นด้วยโคลอน : ก็ได้ กรณีนี้ให้ใส่ params เป็นดิกชันนารี เช่น  

```python
sql = 'select * from pokemon where เลข=:lek'
print(pd.read_sql_query(sql,'sqlite:///pkdex.db',params={'lek': 359}))
```

  
ได้  
```
 	เลข	สายพันธุ์	ส่วนสูง	น้ำหนัก
0	359	อับโซล	1.2		47
```
นอกจากนี้มีฟังก์ชัน `pd.read_sql()` ซึ่งอาจใช้เพื่อแทน `pd.read_sql_table()` หรือ `pd.read_sql_query()` ได้  
  
โดย `pd.read_sql()` จะดูจากค่าที่ใส่ไปเองว่าควรจะเรียก `pd.read_sql_table()` หรือ pd.read_sql_query() ดังนั้นในทางปฏิบัติแล้วถ้าไม่อยากเขียนยาวจะใช้` pd.read_sql()`อย่างเดียวตลอดก็ได้  
  
ตัวอย่าง  

```python
pk = {'สายพันธุ์':['ยุกิวาราชิ','โอนิโกริ','ทามะซาราชิ'],
      'ส่วนสูง':[0.7,1.5,0.8],
      'น้ำหนัก':[16.8,256.5,39.5]}
pokedf = pd.DataFrame(pk,pd.Series([361,362,363],name='เลข'))
pokedf.to_sql('pokemon','sqlite:///pkdex.db',if_exists='replace')

print(pd.read_sql('pokemon','sqlite:///pkdex.db',columns=['เลข','สายพันธุ์']))
sql = 'select * from pokemon where น้ำหนัก<40'

print(pd.read_sql(sql,'sqlite:///pkdex.db'))
```

  
ได้  

```
 	เลข	สายพันธุ์
0	361	ยุกิวาราชิ
1	362	โอนิโกริ
2	363	ทามะซาราชิ

```

```
 	เลข	สายพันธุ์		ส่วนสูง	น้ำหนัก
0	361	ยุกิวาราชิ		0.7		16.8
1	363	ทามะซาราชิ	0.8		39.5

```
เช่นเดียวกับ .to_sql() ฟังก์ชัน pd.read_sql_table(), pd.read_sql_query() และ pd.read_sql() เองก็เดิมทีควรใช้กับ engine ของ sqlalchemy เช่นกัน การเขียนแบบตัวอย่างที่ยกมาจึงเป็นแค่การเขียนย่อ  
  
หากเขียนเต็มๆตั้งแต่สร้าง engine ของ sqlalchemy ก็อาจเขียนได้แบบนี้  

```python
import sqlalchemy

engine = sqlalchemy.create_engine('sqlite:///pkdex.db')
print(pd.read_sql('pokemon',engine))
```

  
นอกจากนี้ pd.read_sql_query() หรือ pd.read_sql() สามารถใช้กับมอดูล sqlite3 ได้ด้วย ดังนั้นจึงอาจเขียนแบบนี้  

```python
import sqlite3

conn = sqlite3.connect('pkdex.db')
print(pd.read_sql('select * from pokemon',conn))
conn.close()
```

  
เพียงแต่ .to_sql() กับ df.read_sql_table จะใช้ได้กับ sqlalchemy เท่านั้น ใช้กับ sqlite3 ไม่ได้  
  
  
  
อ้างอิง  

[https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.to_sql.html](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.to_sql.html)  
[https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.read_sql_table.html](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.read_sql_table.html)  
[https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.read_sql_query.html](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.read_sql_query.html)  
[https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.read_sql.html](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.read_sql.html)  
[https://www.cjavapy.com/article/143](https://www.cjavapy.com/article/143)  
[https://qiita.com/orengeo/items/36e8809e07be7c1b145e](https://qiita.com/orengeo/items/36e8809e07be7c1b145e)

> Reference : [https://phyblas.hinaboshi.com/yancham20](https://phyblas.hinaboshi.com/yancham20)
