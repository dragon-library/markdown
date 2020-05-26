---
title:  การใช้งาน Python ควบคุม Google sheet
subtitle: วิธีการดึงขอมูลหรือเเก้ไขปรับปรุง ข้อมูลใน Google sheet ด้วย Python
summary: Google Sheets คือ App ในกลุ่มของ Google Drive ซึ่งเป็นนวัตกรรมของทาง Google ซึ่งมีลักษณะการทำงานที่คล้ายกับ Microsoft Excel มีการสร้าง Column Row สามารถใส่ข้อมูลลงไปใน Cell ได้และที่สำคัญคือไม่ต้องติดตั้งที่เครื่อง สามารถใช้งานบน Web ได้ โดย ไฟล์ที่เราทำนั้นจะถูกบันทึกไว้ใน Google Drive ทำให้สามารถเปิดใช้งานได้ ไม่ว่าจะอยู่ที่ใด
authors:
    - admin
tags: ['Google sheet']
categories: ['Articles','Python']
date: "2020-05-26T00:00:00Z"
lastMod: "2020-05-26T00:00:00Z"
featured: false
draft: false
---

{{< expand "การปฏิบัติพิธีการในการนำของที่ปบรรจุในเขตปลอดอากเสรีและขอใช้สิทธิชดเชย" "+" >}}

การปฏิบัติพิธีการในการนำของที่ผลิตในประเทศเข้าไปบรรจุในเขตปลอดอากร/เขตประกอบการเสรีและขอใช้สิทธิชดเชยค่าภาษีอากรเมื่อส่งออก
 
{{< /expand >}}

วันนี้ Stackpython จะมาบอกวิธีการดึงขอมูลหรือเเก้ไขปรับปรุง ข้อมูลใน Google sheet ด้วย Python

> **Google Sheets** คือ App ในกลุ่มของ Google Drive ซึ่งเป็นนวัตกรรมของทาง Google ซึ่งมีลักษณะการทำงานที่คล้ายกับ Microsoft Excel มีการสร้าง Column Row สามารถใส่ข้อมูลลงไปใน Cell ได้และที่สำคัญคือไม่ต้องติดตั้งที่เครื่อง สามารถใช้งานบน Web ได้ โดย ไฟล์ที่เราทำนั้นจะถูกบันทึกไว้ใน Google Drive ทำให้สามารถเปิดใช้งานได้ ไม่ว่าจะอยู่ที่ใด

การเปิดช่องทางการเข้าถึง Google Sheet และกำหนดสิทธิ์ให้กับ Application ของเราที่ต้องการจะเข้าถึงข้อมูลผ่านตัว Google Sheet API มีวิธีดังต่อนี้

# เริ่มสร้างโปรเจคท์

มาเริ่มสร้างโปรเจ็กต์ เพื่อเตรียมช่องทางการเข้าถึงข้อมูลใน Google Sheet ก่อนอื่นให้เข้า แพลตฟอร์ม Google Cloud และ เข้าเมนูเลือกไปที่ IAMและผู้ดูแลระบบ -> เลือกจัดการทรัพยากร



![](https://miro.medium.com/max/1010/1*B-8JhFOxSPNzS_YvnKyYkw.jpeg)

1.  ไปที่สร้างโปรเจ็กต์ -> ตั้งชื่อ โปรเจ็กต์ และกดสร้าง เมื่้อเสร็จจะมีเมนูที่เราสร้าง เด้งขึ้นมามุมบนขวามือ



![](https://miro.medium.com/max/481/1*Xvvl-04_xd_9hB4NoDMB_w.jpeg)

----------



![](https://miro.medium.com/max/573/1*ORIPGVLdBciSiLY6wNXkkw.jpeg)

----------

![](https://miro.medium.com/max/1857/1*2OEXIhG7UdnHU-UhXu2m8g.jpeg)

2. เข้าที่เมนูอีกครั้ง แล้วเลือกไปที่ API และบริการ -> เลือกหน้าแดชบอร์ด จากนั้นคลิกที่ เลือกโปรเจ็กต์ เเละทำการเลือกโปรเจ็กต์ที่เราสร้างไว้ -> ไปที่ข้อมูลรับรอง



![](https://miro.medium.com/max/684/1*NCkuG-2dECOjn0jF7OUeWQ.jpeg)

----------


![](https://miro.medium.com/max/664/1*f9fB3ZUvhFvoK0KVRwyilg.jpeg)

----------



![](https://miro.medium.com/max/646/1*IQcnaLGi5Zmh1IWupObhtg.jpeg)

3. เมื่ออยู่ในหน้า ข้อมูลเข้าสู่ระบบ เราจะสร้างข้อมูลรับรองเป็นบัญชีบริการ เลือกที่สร้างข้อมูลรับรอง -> บัญชีบริการ



![](https://miro.medium.com/max/977/1*WaTYoR-tLZiIWuaneKEDrQ.jpeg)

4. จากนั้นตั้งชื่อเเละกดสร้าง -> ให้เลือกบทบาทเป็นโปรเจ็กต์ ผู้เเก้ไข -> กดสร้างคีย์ และเลือก JSON มันจะโหลดไฟร์มาให้เราเก็บไว้ เมื่อกดปุ่มเสร็จสิ้น จะกลับมาที่หน้าหลัก ข้อมูลเข้าสู่ระบบ จะเห็นรายการ บัญชีบริการที่เราสร้างไว้ แสดงขึ้นมาด้านล่าง



![](https://miro.medium.com/max/603/1*ovcm3dpKY5aoyDVQqN6PSQ.jpeg)

----------

![](https://miro.medium.com/max/60/1*esC5aZctoqTXXQg0Ax1C7w.jpeg?q=20)

![](https://miro.medium.com/max/666/1*esC5aZctoqTXXQg0Ax1C7w.jpeg)

----------



![](https://miro.medium.com/max/566/1*ugDF6u6bSYbb2oTZ-YFUzg.jpeg)

----------



![](https://miro.medium.com/max/1245/1*thceZKxNiBRuE3ubrRKR6g.jpeg)

5. ให้ทำการแก้ไขชื่อไฟล์ JSON ที่โหลดออกมาเป็นชื่อ creds.json ->ให้ Copy ข้อมูลส่วน client_email ไว้ เพื่อจะนำไปตั้งสิทธิให้เข้าถึง Google Sheet ที่เราต้องการโดย การกดปุ่ม แชร์ที่ Google Sheet และใส่ข้อมูล email เป็น ข้อมูล client_email ส่วนที่เรา Copy มาและกดส่ง เพื่อ setApplication ให้มีสิทธิเข้าถึง Google Sheet นี้ได้


![](https://miro.medium.com/max/976/1*lSGFDrXKueBxUzup1rbjBg.jpeg)

----------



![](https://miro.medium.com/max/1373/1*Zb3v9LhlixBG_FLdHePO5w.jpeg)

6. จากนั้นให้ไป ไลบรารี ค้นหา Google Sheets API และ Google Drive API เพื่อเปิดใช้งาน ->ไปที่ Google Drive API กดสร้างข้อมูลเข้าสู้ระบบ และเลือก Google Drive API , เว็บเซิร์ฟเวอร์ , ข้อมูลแอปพลิเคชัน , ไม่ ฉันไม่ได้ใช้ แล้วกดฉันต้องใช้ข้อมูลรับรองใด -> กดเสร็จสิ้น



![](https://miro.medium.com/max/683/1*BVXwlChWgLsE0gZEhl6vUA.jpeg)

----------



![](https://miro.medium.com/max/713/1*wWKcSYdI9QvkfVU7-VGqsA.jpeg)

----------

![](https://miro.medium.com/max/60/1*902gITott4GzZPizfYXHrg.jpeg?q=20)

![](https://miro.medium.com/max/718/1*902gITott4GzZPizfYXHrg.jpeg)

----------

![](https://miro.medium.com/max/60/1*-Wd0W_b5x8Lr2-DSCKXC3A.jpeg?q=20)

![](https://miro.medium.com/max/899/1*-Wd0W_b5x8Lr2-DSCKXC3A.jpeg)

----------



![](https://miro.medium.com/max/782/1*mNWIXH-tLQ75_xqnXTkh-g.jpeg)

# เขียนไพธอนดึงข้อมูลจาก Google Sheet

ขั้นตอนต่อไป เราจะมาเขียน Python ให้ดึงแก้ไขข้อมูลออกมาจาก Google Sheet กัน ก่อนอื่นต้องสร้าง virtualenvironment ใน folderที่เราเก็บไฟร์ที่โหลดมาไว้ (แนะนำให้สร้างใหม่เเละเก็บไว้ด้วยกัน) จากนั้นสร้าง file.py เพื่อใช้ในการเขียนโค้ด -> Install Library ที่จำเป็น oauth2client และ gspread ด้วยคำสั้ง pip install oauth2client , pip install gspread



![](https://miro.medium.com/max/1124/1*3J4YoVhZIADMzm5bDyu5XA.jpeg)

----------



![](https://miro.medium.com/max/746/1*UTSCogrqZM-IZSF9jj3Z6A.jpeg)

----------



![](https://miro.medium.com/max/803/1*nNisxjig9TrEuEw5HPiTIA.jpeg)

----------


![](https://miro.medium.com/max/790/1*P4burFRy-e6ji3--szg2xQ.jpeg)

โอเครเรามาดูโค้ดกัน(อันแรกเป็นการดึงข้อมูลมาแสดง)
```py
import gspread
from oauth2client.service_account import ServiceAccountCredentials
from pprint import pprint
scope = ["https://spreadsheets.google.com/feeds",'https://www.googleapis.com/auth/spreadsheets',"https://www.googleapis.com/auth/drive.file","https://www.googleapis.com/auth/drive"]
cerds = ServiceAccountCredentials.from_json_keyfile_name("cerds.json", scope)
client = gspread.authorize(cerds)
sheet = client.open("ชื่อไฟล์งาน").worksheet('แผ่นที่จะเรียกเปิด') # เป็นการเปิดไปยังหน้าชีตนั้นๆ
data = sheet.get_all_records()  # การรับรายการของระเบียนทั้งหมด
pprint(data)
```
ตัวอย่างผลลัพธ์



![](https://miro.medium.com/max/1862/1*2GLtVjbNW6c4P8ZpF7mQMQ.jpeg)

(ต่อไปจะเป็นการแก้ไขข้อความ)
```py
import gspread
from oauth2client.service_account import ServiceAccountCredentials
from pprint import pprint
scope = ["https://spreadsheets.google.com/feeds",'https://www.googleapis.com/auth/spreadsheets',"https://www.googleapis.com/auth/drive.file","https://www.googleapis.com/auth/drive"]
cerds = ServiceAccountCredentials.from_json_keyfile_name("cerds.json", scope)
client = gspread.authorize(cerds)
sheet = client.open("ชื่อไฟล์งาน").worksheet('แผ่นที่จะเรียกเปิด') # เป็นการเปิดไปยังหน้าชีตนั้นๆ
cell=sheet.cell(4,2).value
pprint(cell)
sheet.update_cell(4,2,"แก้ไข")
cell=sheet.cell(4,2).value
pprint(cell)
```
ตัวอย่างผลลัพธ์



![](https://miro.medium.com/max/1862/1*iN2NI0OPHKF-dNf85cEI8Q.jpeg)

นอกจากนี้ยังมีคำสั่งอีกมาก เช่น
```py
 sheet.row_value(*) #ใส่เลขที่ต้องการแทน *­­­­­­­­ 
 sheet.col_value(*) #ใส่เลขที่ต้องการแทน *
 sheet.delete_row(*) #ใส่เลขที่ต้องการแทน *
 sheet.delete_columns(*) #ใส่เลขที่ต้องการแทน *
 sheet.insert_row([&],*)#ใส่เลขที่ต้องการแทน *และข้อความแทน &
```
ลองไปใช้กันดูนะครับ

> ขอบคุณมากครับที่เข้ามาอ่านบทความของทางเพจ Stackpython ทั้งนี้ หากสงสัยตรงไหนเกี่ยวกับเนื้อหาในบทความสามารถติดต่อสอบถามทางเพจเราได้เลยครับ

Reference : [Medium](https://medium.com/@stackpython/%E0%B8%81%E0%B8%B2%E0%B8%A3%E0%B9%83%E0%B8%8A%E0%B9%89%E0%B8%87%E0%B8%B2%E0%B8%99-python-%E0%B8%84%E0%B8%A7%E0%B8%9A%E0%B8%84%E0%B8%B8%E0%B8%A1-google-sheet-665a6dca077d)