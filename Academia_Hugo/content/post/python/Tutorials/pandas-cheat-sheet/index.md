---
title:   Pandas Cheat Sheet 
subtitle : Pandas เป็น Library ใน Python ที่ทำให้เราเล่นกับข้อมูลได้ง่ายขึ้น เหมาะมากสำหรับทำ  Data Cleaning / Wrangling
summary: Pandas ถือเป็นเครื่องมือหลักในการทำ Data Wrangling บน Python และสามารถนำไปใช้ประโยชน์คู่กับ Package อื่น เช่น เอาไปเตรียมข้อมูลก่อนทำ Model ใน SKLearn ได้ด้วย

authors:
    - admin
tags: ['Cheat Sheet']
categories: ['Tutorials','Pandas']
date: "2020-05-31T00:00:00Z"
lastMod: "2020-05-31T00:00:00Z"
featured: true
draft: false
image:
  caption: "Image by www.reddit.com"
  focal_point: ""
  preview_only: true
---



>[November 5, 2017](https://blog.datath.com/2017/11/05/)

![](featured.jpg)

>Image by www.reddit.com

Pandas ถือเป็นเครื่องมือหลักในการทำ Data Wrangling บน Python และสามารถนำไปใช้ประโยชน์คู่กับ Package อื่น เช่น เอาไปเตรียมข้อมูลก่อนทำ Model ใน SKLearn ได้ด้วย

วันนี้แอดมินเลยเอาคำสั่ง Pandas ที่ใช้บ่อย ๆ มารวบรวมให้renameหาง่าย ๆ ตั้งแต่อ่านไฟล์ข้อมูล เลือกข้อมูล แก้ไขข้อมูล ไปจนถึงเซฟไฟล์ข้อมูลเพื่อนำไปใช้ต่อเลยทีเดียว หวังว่าจะเป็นประโยชน์กับทุกท่านนะครับ :)

และเนื่องจากหน้านี้เป็น Cheatsheet รวมเทคนิคเยอะแยะมากมาย ถ้าไล่อ่านกันอาจจะหายาก ผมเลยเตรียมสารบัญมาให้ด้านล่างนี้ครับ

**Contents**  [hide](https://blog.datath.com/cheatsheet-pandas/#)

[1  Pandas คืออะไร?](https://blog.datath.com/cheatsheet-pandas/#Pandas_khux_xari)

[2  เทคนิคการใช้ Pandas](https://blog.datath.com/cheatsheet-pandas/#thekhnikh_kar_chi_Pandas)

[2.1  วิธีเช็ค Version Pandas](https://blog.datath.com/cheatsheet-pandas/#withi_chekh_Version_Pandas)

[2.2  วิธีการโหลดไฟล์ CSV (Import)](https://blog.datath.com/cheatsheet-pandas/#withi_kar_hold_fil_CSV_Import)

[2.3  วิธีสุ่มข้อมูลสำหรับเช็ค (Sample)](https://blog.datath.com/cheatsheet-pandas/#withi_sum_khxmul_sahrab_chekh_Sample)

[2.4  วิธีเช็คข้อมูลหาความผิดปกติใน DataFrame เบื้องต้น](https://blog.datath.com/cheatsheet-pandas/#withi_chekh_khxmul_hakhwam_phid_pkti_ni_DataFrame_beuxng_tn)

[2.5  วิธีแปลงประเภทข้อมูล (Data Type) ใน Data Frame](https://blog.datath.com/cheatsheet-pandas/#withi_paelng_prapheth_khxmul_Data_Type_ni_Data_Frame)

[2.6  วิธีเช็ค Summary ของแต่ละคอลัมน์ (count, min, max, mean)](https://blog.datath.com/cheatsheet-pandas/#withi_chekh_Summary_khxng_taela_khxlamn_count_min_max_mean)

[2.7  วิธีเช็ค Summary (count, min, max, mean) แบบแยกกลุ่ม](https://blog.datath.com/cheatsheet-pandas/#withi_chekh_Summary_count_min_max_mean_baeb_yaek_klum)

[2.8  วิธีสร้าง DataFrame ใหม่](https://blog.datath.com/cheatsheet-pandas/#withi_srang_DataFrame_him)

[2.9  วิธีเลือกหลายคอลัมน์จาก DataFrame](https://blog.datath.com/cheatsheet-pandas/#withi_leuxk_hlay_khxlamn_cak_DataFrame)

[2.10  วิธีเลือกคอลัมน์ตามเงื่อนไขที่ต้องการ](https://blog.datath.com/cheatsheet-pandas/#withi_leuxk_khxlamn_tam_ngeuxnkhi_thi_txngkar)

[2.11  วิธีเลือกแถวตามเงื่อนไขที่ต้องการ](https://blog.datath.com/cheatsheet-pandas/#withi_leuxk_thaew_tam_ngeuxnkhi_thi_txngkar)

[2.12  วิธีเพิ่มคอลัมน์ใหม่](https://blog.datath.com/cheatsheet-pandas/#withi_pheim_khxlamn_him)

[2.13  การสลับ Row <-> Column (Transpose)](https://blog.datath.com/cheatsheet-pandas/#kar_slab_Row_-_Column_Transpose)

[2.14  การต่อ DataFrame](https://blog.datath.com/cheatsheet-pandas/#kar_tx_DataFrame)

[2.15  การต่อ DataFrame แบบ Join](https://blog.datath.com/cheatsheet-pandas/#kar_tx_DataFrame_baeb_Join)

[2.16  การหาค่า Mean, Sum, Max (Aggregate) แบบทั้ง DataFrame](https://blog.datath.com/cheatsheet-pandas/#kar_ha_kha_Mean_Sum_Max_Aggregate_baeb_thang_DataFrame)

[2.17  การ Aggregate แบบตามกลุ่มที่ต้องการ](https://blog.datath.com/cheatsheet-pandas/#kar_Aggregate_baeb_tam_klum_thi_txngkar)

[2.18  การรัน Function เดียวกันทุกแถว หรือทุกคอลัมน์](https://blog.datath.com/cheatsheet-pandas/#kar_ran_Function_deiywkan_thuk_thaew_hrux_thuk_khxlamn)

[2.19  รันคำสั่งที่เขียนเองกับทุกแถวใน 1 คอลัมน์](https://blog.datath.com/cheatsheet-pandas/#ran_kha_sang_thi_kheiyn_xeng_kab_thuk_thaew_ni_1_khxlamn)

[2.20  รันคำสั่งที่เขียนเองกับทุกค่า](https://blog.datath.com/cheatsheet-pandas/#ran_kha_sang_thi_kheiyn_xeng_kab_thuk_kha)

[2.21  คำนวณ Correlation & Covariance](https://blog.datath.com/cheatsheet-pandas/#khanwn_Correlation_Covariance)

[2.22  คำนวณ Cross Tabulation](https://blog.datath.com/cheatsheet-pandas/#khanwn_Cross_Tabulation)

[2.23  วิธีหาค่า Unique ในแต่ละคอลัมน์](https://blog.datath.com/cheatsheet-pandas/#withi_ha_kha_Unique_ni_taela_khxlamn)

[2.24  วิธีเช็คว่ามีแถวไหนข้อมูลซ้ำมั้ย (Duplicated)](https://blog.datath.com/cheatsheet-pandas/#withi_chekh_wa_mi_thaew_hin_khxmul_sa_may_Duplicated)

[2.25  วิธีการนับจำนวน Duplicate](https://blog.datath.com/cheatsheet-pandas/#withi_kar_nab_canwn_Duplicate)

[2.26  วิธีการลบ Duplicate](https://blog.datath.com/cheatsheet-pandas/#withi_kar_lb_Duplicate)

[2.27  วิธีการลบแถว และลบคอลัมน์](https://blog.datath.com/cheatsheet-pandas/#withi_kar_lb_thaew_laea_lb_khxlamn)

[2.28  วิธีการลบแถวที่มี Missing Value](https://blog.datath.com/cheatsheet-pandas/#withi_kar_lb_thaew_thi_mi_Missing_Value)

[2.29  วิธีแทนค่า Missing Value ด้วยค่าเฉลี่ย (Mean Imputation)](https://blog.datath.com/cheatsheet-pandas/#withi_thaen_kha_Missing_Value_dwy_kha_cheliy_Mean_Imputation)

[2.30  การลูปข้อมูลแต่ละคอลัมน์ และแต่ละแถว](https://blog.datath.com/cheatsheet-pandas/#kar_lup_khxmul_taela_khxlamn_laea_taela_thaew)

[2.31  วิธีเปลี่ยน DataFrame จากแบบ Wide เป็น Long (Melt)](https://blog.datath.com/cheatsheet-pandas/#withi_peliyn_DataFrame_cak_baeb_Wide_pen_Long_Melt)

[2.32  วิธีการเปลี่ยนชื่อคอลัมน์ (Rename)](https://blog.datath.com/cheatsheet-pandas/#withi_kar_peliyn_chux_khxlamn_Rename)

[2.33  วิธีการใส่คำนำหน้าคอลัมน์ (Prefix)](https://blog.datath.com/cheatsheet-pandas/#withi_kar_si_khana_hna_khxlamn_Prefix)

[2.34  วิธีการแทนค่าใน DataFrame](https://blog.datath.com/cheatsheet-pandas/#withi_kar_thaen_kha_ni_DataFrame)

[2.35  วิธีการ Export DataFrame เป็นไฟล์ CSV](https://blog.datath.com/cheatsheet-pandas/#withi_kar_Export_DataFrame_pen_fil_CSV)

[3  สรุปการใช้งาน Pandas](https://blog.datath.com/cheatsheet-pandas/#srup_kar_chi_ngan_Pandas)

## Pandas คืออะไร?

Pandas เป็น Library ใน Python ที่ทำให้เราเล่นกับข้อมูลได้ง่ายขึ้น เหมาะมากสำหรับทำ  [Data Cleaning / Wrangling](https://www.facebook.com/datasciencechill/photos/a.251751741876557.1073741828.250303472021384/388914871493576/?type=3)  ครับผม

วิธีการใช้งาน Pandas คือ โหลดไฟล์ข้อมูล เช่น CSV เข้าไป แล้วเราจะได้ข้อมูลในรูปแบบตาราง (DataFrame) ที่แบ่งข้อมูลตามแถวและคอลัมน์ หรือเหมือน Excel ที่เราใช้กันนั่นเอง

[![](https://cdn.shortpixel.ai/client/to_webp,q_lossy,ret_img,w_998/https://blog.datath.com/wp-content/uploads/2017/11/example-dataframe-pandas.jpg)](https://blog.datath.com/cheatsheet-pandas/example-dataframe-pandas/)

ตัวอย่าง DataFrame ของ Pandas เป็นตารางเหมือน Excel เลยครับ

ป.ล. Pandas ไม่เกี่ยวกับหมีแพนด้านะฮะ จริง ๆ แล้วมาจากคำว่า PANel DAta ซึ่งหมายถึงข้อมูลที่มีหลายมิตินั่นเอง

## เทคนิคการใช้ Pandas

อย่างที่[แอดมินเคยเล่า](https://www.facebook.com/datasciencechill/photos/a.251751741876557.1073741828.250303472021384/388914871493576/?type=3) ว่าการทำ Data Wrangling เป็นงานที่ค่อนข้างถึกครับ วันนี้เลยรวบรวมโค้ดต่าง ๆ ในการใช้ Pandas มาให้ ซึ่งน่าจะครอบคลุมการใช้งานประมาณ 80 – 90% แล้วครับผม

โค้ดบางส่วนมาจากคลาส Data Wrangling ที่แอดมินเรียน และจากเว็บไซต์ [MyCheatSheet](https://mycheatsheets.com/pandas) ครับ

### วิธีเช็ค Version Pandas

โค้ดนี้เหมือนไม่สำคัญ แต่จริง ๆ แล้วสำคัญมากเวลาเราอ่าน Documentation ครับ เพราะถ้าเกิดมีอะไรพัง เราจะเทียบได้ว่า Pandas ของเราเป็นเวอร์ชั่นตามใน Documentation มั้ย

print  ("Pandas version",pandas.__version__)

### วิธีการโหลดไฟล์ CSV (Import)

จุดเริ่มต้นของการทำ Data Exploration & Analysis ใน Pandas ก็คือการโหลดไฟล์ข้อมูลแบบ CSV มาใช้งานนั่นเองครับ

เราสามารถใช้คำสั่ง .head หรือ .tail เพื่อดูข้อมูลแถวบนสุด หรือแถวล่างสุดได้

# Read DF
```py
csvdf = pd.read_csv('data.csv')
```
# Sometimes reading CSV for Excel need encoding
```py
csvdf = pd.read_csv('data.csv',encoding = "ISO-8859-1")
```
# Print head and tail
```py
csvdf.head()

csvdf.tail()
```
### วิธีสุ่มข้อมูลสำหรับเช็ค (Sample)

ปกติเราเช็คข้อมูลว่าถูกต้องมั้ยด้วย head กับ tail ซึ่งเป็นการเช็คจากด้านบนหรือด้านล่าง อีกวิธีที่น่าสนใจ คือ เช็คแบบสุ่มข้อมูลขึ้นมานั่นเองครับ ทำได้ง่าย ๆ โดยใช้
```py
csvdf.sample()
```
### วิธีเช็คข้อมูลหาความผิดปกติใน DataFrame เบื้องต้น

หลังจากโหลดข้อมูลมาแล้ว เราอยากรู้ว่าข้อมูลมีกี่แถว, Missing value เท่าไหร่, แต่ละคอลัมน์เป็น Data Type อะไรบ้าง ก็รันคำสั่งนี้ได้เลย มีประโยชน์มากครับ
```py
df.info()
```
![](https://cdn.shortpixel.ai/client/to_webp,q_lossy,ret_img,w_525/https://blog.datath.com/wp-content/uploads/2017/11/sample-info-pandas.jpg)

df.info() จะแสดงสรุปข้อมูลมาให้

นอกจากนั้นยังมีคำสั่ง df.dtypes (ไม่มีวงเล็บ) สำหรับดู Data Type แต่ละคอลัมน์อย่างเดียว

### วิธีแปลงประเภทข้อมูล (Data Type) ใน Data Frame

บางครั้งประเภทข้อมูลของคอลัมน์เป็น String แต่เราต้องการ Integer หรือเราต้องการ Date เราสามารถแปลงข้อมูลได้ง่าย ๆ ดังนี้เลยครับ
```py
df['hour'] = pd.to_numeric(df['hour']) # แปลงเป็น Numeric

df['hour'] = df['hour'].astype('int') # อีกวิธีในการแปลงค่า สามารถใช้วิธีนี้แปลงเป็น float ได้
```

### วิธีเช็ค Summary ของแต่ละคอลัมน์ (count, min, max, mean)

ถ้าเราอยากรู้ Distribution คร่าว ๆ ของแต่ละคอลัมน์ว่าเป็นอย่างไร สามารถใช้คำสั่ง describe() ได้

df.describe()

### วิธีเช็ค Summary (count, min, max, mean) แบบแยกกลุ่ม

บางครั้งเราไม่ได้ต้องการรู้ Summary ของทั้งคอลัมน์ แต่อยากให้แยกตามแต่ละค่าในคอลัมน์นั้น ๆ ครับ ซึ่งมีประโยชน์มากเวลาเราทำ Data Analysis แล้วอยากรู้ว่าบางกลุ่มมีอะไรผิดปกติหรือเปล่า
```py
test = df.groupby(['Gender'])

test.describe()
```
### วิธีสร้าง DataFrame ใหม่

วิธีสร้างแบบง่ายที่สุด ถ้าต้องการข้อมูลหลายรูปแบบ เราสามารถใช้ Dictionary แบบนี้เลยครับ
```py
dataframe = pandas.DataFrame({

'C1': pandas.date_range('20170101', periods=4),

'C2' : [10,20,30,40],

'C3': pandas.Categorical(['A','B','C','D']),

'C4': 1})
```
แต่ถ้าเราต้องการแค่เป็นแบบตัวเลขทั่วไป ใช้ Numpy แบบนี้ได้เลย
```py
array = numpy.array([(1,2,3), (4,5,6),(7,8,9)])

dataframe = pandas.DataFrame(array,columns=['C1','C2','C3'])
```
### วิธีเลือกหลายคอลัมน์จาก DataFrame

ปกติถ้าเราต้องการเลือกแค่ 1 Column ก็เขียนแบบนี้ได้เลย
```py
df['C1']
```
แต่ถ้าต้องการเลือกหลายคอลัมน์ ให้ทำแบบนี้
```py
df[['C1','C2']]
```
### วิธีเลือกคอลัมน์ตามเงื่อนไขที่ต้องการ

บางทีเราอยาก Filter เฉพาะคอลัมน์ที่มีค่าตามที่เราต้องการโดยใช้ .loc ได้ โดยสามารถเลือก Filter แบบ .all() (ทุกค่าในคอลัมน์ต้องตรงตามเงื่อนไข) หรือ .any() (บางค่าในคอลัมน์ต้องตรงตามเงื่อนไข)
```py
dataframe2 = dataframe.loc[:,(dataframe>50).any()]

dataframe3 = dataframe.loc[:,(dataframe>50).all()]
```
เราสามารถใช้หาคอลัมน์ที่มี Missing Values หรือหาคอลัมน์ที่ไม่มี Missing Values เลยก็ได้
```py
dataframe2 = dataframe.loc[:,dataframe.isnull().any()]

dataframe3 = dataframe.loc[:,dataframe.notnull().all()]
```
### วิธีเลือกแถวตามเงื่อนไขที่ต้องการ
```py
dataframe[dataframe['C1']>50] # เงื่อนไขแบบง่าย ๆ

dataframe2 = dataframe.loc[dataframe.C1.isin([1,2,3])] # เงื่อนไขแบบซับซ้อน
```
ถ้ามีหลายเงื่อนไขเราสามารถใช้ & (and) หรือ | (or) ได้
```py
dataframe[(dataframe['C1']>50) & ((dataframe['C2']<25) | (dataframe['C2']>75))]
```
หรือใช้ Query เป็นเงื่อนไขได้ด้วย มีประโยชน์มากเวลาเรามีเงื่อนไขแปลก ๆ ไม่ต้องเขียนลูปขึ้นมาเองเลยครับ
```py
dataframe2 = dataframe.query('C1 > C2')
```
### วิธีเพิ่มคอลัมน์ใหม่

สามารถเพิ่มคอลัมน์ใหม่ได้ 2 แบบ คือ

1.  เพิ่มโดยอิงจากคอลัมน์เดิม (เช่น เอาคอลัมน์เดิม + 10 หรือ เอาคอลัมน์ A – คอลัมน์ B มีประโยชน์มากตอนทำ Feature Engineering)
2.  เพิ่มคอลัมน์โดยตั้งค่า Fix ไปเลยสำหรับทุกแถว ส่วนใหญ่จะใช้วิธีนี้เวลาเราอยากได้ค่าอะไรแปลก ๆ ที่ต้องเขียนลูปเพื่อใส่ค่า ก็สร้างคอลัมน์แบบ Fix ค่าก่อน แล้วต่อด้วยลูป
```py
df['new'] = dataframe['old'] + 10 # use old values

df['new2'] = 5 # apply the same value
```
### การสลับ Row <-> Column (Transpose)

ถ้าเราต้องการ Transpose (อารมณ์เหมือน Vector) เราสามารถใช้คำสั่งนี้ได้เลย
```py
dataframe.T
```
### การต่อ DataFrame

การต่อ Data Frame คือการเอา Data Set 2 ชุดมาต่อกันในแถวตั้งหรือแนวนอน สำหรับการต่อแบบปะติดไปเลย

มี 2 คำสั่งที่เหมือนกัน คือ concat กับ append แต่ให้ใช้ concat ไปเลย เพราะ append เป็นคำสั่งที่ไม่ Memory Efficient
```py
pd.concat([df1,df2], axis=1) # รวมกัน 2 คอลัมน์ (axis = 0 คือแถว, axis = 1 คือคอลัมน์)

pd.concat([df1,df2,df3)] # รวมมากกว่า 2 คอลัมน์ก็ได้

pd.concat(…, ignore_index=True) # รวมเสร็จแล้ว reset index ให้ด้วย ควรใช้ ไม่งั้นจะเจอ row ID ซ้ำกันตอนรวมร่าง

pd.concat(…, join='inner') # รวมร่างเฉพาะคอลัมน์ที่ df1 กับ df2 มีทั้งคู่

pd.concat(…, keys=['source1', 'source2']) # เพิ่มคอลัมน์เข้าไปด้วยเพื่อระบุว่า Row แต่ละอันมาจาก Data Frame อันไหน

pd.concat(…, join_axes=[df2.index]) # เลือกรวมร่างเฉพาะ row index ที่เรากำหนดได้
```
### การต่อ DataFrame แบบ Join

ถ้าต้องการต่อ DataFrame แบบ Advance หน่อย เราก็สามารถ Join DataFrame ได้เหมือน Join Table ใครเขียน SQL มาก่อนน่าจะถนัดเลย
```py
pd.merge(df1, df2, left_on="col1", right_on="col2", how="inner")
```
เราสามารถเปลี่ยนตรง how=”inner” เป็น “outer”, “left”, “right” เพื่อเปลี่ยนเป็น Outer Join, Left Join, Right Join ได้อีกด้วย

### การหาค่า Mean, Sum, Max (Aggregate) แบบทั้ง DataFrame

Pandas สามารถสั่ง Aggregate เพื่อหาค่า Mean, Sum, และ Max ได้เลย เหมาะมากเวลาเราต้องการรวบข้อมูลก่อนเอาไป Visualize หรือต้องการทำ Feature Engineering ก็ได้
```py
newdf = df.agg(['sum', 'max','mean'])
```
### การ Aggregate แบบตามกลุ่มที่ต้องการ

บางทีเราอยาก Aggregate ข้อมูลตามการจัดกลุ่มในคอลัมน์อื่น เช่น เราอยากได้รายจ่ายทั้งหมดของแต่ละคน (ต้อง aggregate sum ของคอลัมน์รายจ่าย โดยแบ่งกลุ่มตามคอลัมน์ User ID) ใช้แบบนี้
```py
aggregate = dataframe.groupby('C1').sum()
```
### การรัน Function เดียวกันทุกแถว หรือทุกคอลัมน์

เวลาเราอยากรันคำสั่งอะไรสักอย่างสำหรับทุกแถว หรือทุกคอลัมน์ เราสามารถเขียนได้แบบนี้

# sum for columns
```py
sum_columns = dataframe[['C1','C2']].apply(sum,axis=0)
```
# sum for rows
```py
sum_rows = dataframe[['C1','C2']].apply(sum,axis=1)
```
เหมือนกับฟังก์ชั่น apply() ใน R นั่นเอง

### รันคำสั่งที่เขียนเองกับทุกแถวใน 1 คอลัมน์

ถ้าต้องการรันคำสั่ง (Function) ที่เขียนเอง สำหรับทุกแถวในคอลัมน์อันใดอันหนึ่ง ใช้แบบนี้ได้
```py
dataframe['C1'] = dataframe['C1'].map(lambda x: x-100)
```
### รันคำสั่งที่เขียนเองกับทุกค่า

ถ้าต้องการรันคำสั่งที่เขียนเองกับทุกค่าใน DataFrame ใช้โค้ดนี้
```py
function_result = dataframe.applymap(lambda x: x*10)
```
หรือใช้ transform ก็ได้
```py
new_dataframe = dataframe.transform(lambda x: x*100)
```
### คำนวณ Correlation & Covariance

เวลาเราอยากรู้ว่าค่าต่าง ๆ ใน Data Set เรา Correlate กันมั้ย
```py
dataframe.corr() # Correlation

dataframe.cov() # Covariance
```
แต่ค่าที่ออกมาเป็นตัวเลขอาจจะดูยากนิดนึง เราสามารถพลอตสวย ๆ ด้วย Seaborn ได้ครับ สามารถใช้โค้ดด้านล่างนี้ได้เลย
```py
import seaborn as sns

corr = modeldf.corr()
```
# Set up the matplotlib figure
```py
f, ax = plt.subplots(figsize=(15, 8))
```
# Generate a custom diverging colormap
```py
cmap = sns.diverging_palette(10, 10, as_cmap=True)
```
# Draw the heatmap with the mask and correct aspect ratio
```py
sns.heatmap(corr, annot=True)
```
![](https://cdn.shortpixel.ai/client/to_webp,q_lossy,ret_img,w_861/https://blog.datath.com/wp-content/uploads/2017/11/seaborn-correlation-heatmap.jpg)
Correlation Plot สวย ๆ ด้วย Seaborn

### คำนวณ Cross Tabulation

Cross Tabulation มีประโยชน์มากเวลาเราอยากรู้ว่ามี Data ที่ตรงกับกรุ๊ป A ของคอลัมน์ 1 และกรุ๊ป B ของคอลัมน์ 2 เท่าไหร่ เช่น มีนักเรียนผู้ชาย (คอลัมน์ gender) กี่คนในมัธยมปลาย (คอลัมน์ education) แบบนี้เป็นต้น

หรือถ้าใครใช้ PivotTable ใน Excel มาก่อน ก็เหมือนกันเลยครับ
```py
aggregate = pandas.crosstab(dataframe.C1, dataframe.C2)
```
### วิธีหาค่า Unique ในแต่ละคอลัมน์

คำสั่งนี้มีประโยชน์มาก เอาไว้ใช้เช็คว่าแต่ละคอลัมน์มีค่าแปลก ๆ มั้ย

ตัวอย่างการใช้งานก็คือ เราอยากรู้ว่า มีบ้านไหนที่มีจำนวนห้องนอนแปลก ๆ มั้ย (เช่น 50 ห้องนอน หรือ -5 ห้องนอน) ก็หาค่า unique จากคอลัมน์ “bedrooms”
```py
dataframe['C1'].unique()
```
### วิธีเช็คว่ามีแถวไหนข้อมูลซ้ำมั้ย (Duplicated)

อันนี้มีประโยชน์มาก เอาไว้ใช้เช็คว่ามีข้อมูลแปลก ๆ มั้ย เช่น ทุกคอลัมน์ซ้ำกันหมด (อันนี้มีโอกาสว่าเป็นข้อมูลซ้ำ อาจจะต้องลบออก) หรือซ้ำกันบางคอลัมน์ (อันนี้ต้องเช็คอีกทีว่าคืออะไร)
```py
dataframe.duplicated() # หาอันที่เหมือนกันทุกคอลัมน์

dataframe.duplicated('C1') # หาอันที่ซ้ำกันเฉพาะคอลัมน์ C1

dataframe.duplicated(['C1', 'C2']) # หาอันที่ซ้ำกันเฉพาะคอลัมน์ C1 และ C2
```
ปกติแล้วถ้ามีไอเทมซ้ำ คำสั่งนี้จะไม่แสดงไอเทมแรกในกลุ่มที่ซ้ำ (เช่น ถ้า C1=5 มี 2 แถว มันจะแสดงเฉพาะแถวที่ 2) เราสามารถใส่ Argument  **keep=False**  เข้าไปเพื่อบังคับให้มันแสดงทุกแถวได้

นอกจากนั้นเรายังสามารถนับจำนวนแถวที่ Duplicate และลบทิ้งได้ด้วย

### วิธีการนับจำนวน Duplicate
```py
len(df[ df.duplicated(['A', 'B', 'C'], keep = False)  ])
```
### วิธีการลบ Duplicate

เอาไว้ใช้ตอนเราเจอว่าทุกคอลัมน์ซ้ำกันหมดเลย ซึ่งเป็นเคสที่บอกว่าข้อมูลน่าจะซ้ำ ลบออกได้ (ขึ้นอยู่กับข้อมูลด้วยนะครับ บางข้อมูลอาจจะไม่ได้แปลว่าซ้ำแล้วลบได้):

# Remove the duplicates
```py
df.drop_duplicates(['A', 'B', 'C'], inplace=True)
```
# Reset dataframe index after drop_duplicates.
```py
df.reset_index(drop=True, inplace=True)

len(df)
```
สำหรับโค้ดข้างบน จะเห็นว่าเราต้อง reset index หลังลบ duplicate ด้วยนะครับ

### วิธีการลบแถว และลบคอลัมน์

ลบคอลัมน์สามารถทำได้แบบนี้
```py
dataframe = dataframe.drop('C1', axis=1)

df.drop(['C1'], axis=1, inplace=True) # แบบนี้ก็ได้

df.drop(['C1', 'C2', 'C3'], 1, inplace=True) # ลบทีละหลายคอลัมน์ก็ได้
```
ส่วนการลบแถวจะลำบากหน่อย เพราะต้องใส่ Row Index (เลขที่อยู่ซ้ายสุดเวลาเราปรินท์ DataFrame)
```py
dataframe = dataframe.drop(5, axis=0)

dataframe.reset_index(drop=True) # Reset index
```
ลบแถวแล้วอย่าลืมเช็คด้วยว่าที่ลบไปถูกต้องมั้ย และหลังจากลบแถวต้อง Reset Index ด้วย

### วิธีการลบแถวที่มี Missing Value

**ข้อควรระวัง:**  การที่อยู่ ๆ เราลบแถวที่มี Missing Value ทิ้งไปเลยอาจจะไม่ใช่วิธีที่ดีที่สุดในการทำ Data Analysis เสมอไปนะครับ บางเคสการ Impute (คำนวณหาค่าไปใส่) จะดีกว่าครับ
```py
dataframe2 = dataframe.dropna(axis=0)
```
### วิธีแทนค่า Missing Value ด้วยค่าเฉลี่ย (Mean Imputation)

วิธีหนึ่งในการแทนค่าที่หายไป คือการทำสิ่งที่เรียกว่า Mean Imputation หรือหาค่าเฉลี่ยของคอลัมน์นั้น แล้วเอามาแทนค่าที่หายไปนั่นเองครับ

ข้อดีของการทำ Mean Imputation คือ สามารถทำได้ง่าย แต่ก็ต้องระวังเรื่องข้อเสีย เช่น ทำแบบนี้จะเป็นการไม่สนใจความสัมพันธ์ระหว่างตัวแปร ทำให้เกิด Bias สูง ควรใช้เฉพาะเวลา Missing Value ไม่เยอะเท่านั้นครับ

สามารถรันโค้ดด้านล่างเพื่อทำ Mean Imputation ได้ง่าย ๆ เลย
```py
import numpy as np

meanAge = np.mean(df.Age) # Get mean value

df.Age = df.Age.fillna(meanAge) # Fill missing values with mean
```
### การลูปข้อมูลแต่ละคอลัมน์ และแต่ละแถว

การลูปมีประโยชน์มากถ้าเราต้องการเขียนฟังก์ชั่นแปลก ๆ ใช้เองที่ Pandas ไม่รองรับ (หรืออาจจะรองรับแต่เราหาไม่เจอ เขียนเองง่ายกว่า) สามารถลูปได้ทั้งแต่ละคอลัมน์ และแต่ละแถว
```py
for col_idx,data in dataframe.iteritems():

	print  ("column:",col_idx)
	print  ("column data:")
	print  (data,"\n")
```
การลูปข้อมูลแต่ละแถว
```py
for col_idx,data in dataframe.iterrows():

print  ("row:",col_idx)
print  ("row data:")
print  (data,"\n")
```
### วิธีเปลี่ยน DataFrame จากแบบ Wide เป็น Long (Melt)

การ Melt Data มีประโยชน์มากเวลาเราต้องการเอาข้อมูลไปพลอต Data Visualization หรือเราต้องการ Aggregate ครับ

dataframe2 = dataframe.melt()

### วิธีการเปลี่ยนชื่อคอลัมน์ (Rename)

บางทีเราต้องการเปลี่ยนชื่อเพื่อให้สั้นลง ให้พิมพ์สะดวกขึ้น สามารถทำได้ดังนี้
```py
dataframe.rename(columns={'old':'new'},inplace=True)
```
### วิธีการใส่คำนำหน้าคอลัมน์ (Prefix)

อันนี้มีประโยชน์มากตอนเรามีข้อมูลหลาย ๆ ชุด และต้องการ Merge โดยอยากให้ชื่อคอลัมน์ไม่ซ้ำกัน
```py
thisdata = thisdata.add_prefix('data_')
```
### วิธีการแทนค่าใน DataFrame

เหมาะมากเวลาต้องการแก้ Typo Error เช่น เราอยากได้ค่า Bangkok แต่เรารู้ว่ามีคนเขียนเป็น BKK อะไรแบบนี้ (รันคำสั่ง .unique เพื่อดูก่อน)

เราสามารถ Replace ทั้ง DataFrame ได้เลยแบบนี้
```py
dataframe2 = dataframe.replace(1, -100)
```
เราสามารถ Replace หลายค่าพร้อมกันได้ด้วยครับ และสามารถกำหนด Column ที่ต้องการให้แทนค่าได้ด้วย
```py
df['city'].replace({

'BKK':'Bangkok',

'BNK':'Bangkok'

}, inplace=True)
```
### วิธีการ Export DataFrame เป็นไฟล์ CSV

หลังจากที่เราจัดการ Data เรียบร้อยแล้ว ก็สามารถ Export เป็น CSV เอาไปใช้ต่อกับโปรแกรมอื่น หรืองานส่วนอื่น ๆ ได้ (แอดทำบ่อยเพราะบางทีต้องสลับ Python <-> R รัว ๆ)
```py
dataframe.to_csv('dataframe.csv')
```
> Reference : [https://blog.datath.com/cheatsheet-pandas/](https://blog.datath.com/cheatsheet-pandas/)