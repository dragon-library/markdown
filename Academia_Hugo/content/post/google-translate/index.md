---
title: Google Translate.
subtitle: Google Translate มีเครื่องมือให้นักพัฒนานำความสามารถไปใช้กับโปรแกรมภายนอก ผ่านโมดูล googletrans เป็นโมดูลที่นำ Google Translate มาใช้งานร่วมกับ Python
summary: Google Translate มีเครื่องมือให้นักพัฒนานำความสามารถไปใช้กับโปรแกรมภายนอก ผ่านโมดูล googletrans เป็นโมดูลที่นำ Google Translate มาใช้งานร่วมกับ Python
authors:
  - admin
tags: ["Google Translate"]
categories: ["Example", "Python"]
date: "2020-05-28T00:00:00Z"
lastMod: "2020-05-28T00:00:00Z"
featured: true
draft: false
image:
  caption: ""
  focal_point: ""
  preview_only: true
---

![](featured.jpeg)

- [Document:](https://pypi.org/project/googletrans/?fbclid=IwAR2nJome20RmcX1UMc6GCrslpIXn-Uj9TgpnJrfS4etUVd4q9SgZKVpuM6w)
- install: `pip install googletrans`
- install: `conda install -c conda-forge googletrans`

---

- author: [Prasert Kanawattanachai](prasert.k@chula.ac.th)
- YouTube: https://www.youtube.com/prasertcbs
- [Chulalongkorn Business School](https://www.cbs.chula.ac.th/en/)

---

```python
from IPython.display import YouTubeVideo
YouTubeVideo('9tR1aqQEwGY', width=720, height=405)
```

{{< youtube 9tR1aqQEwGY >}}

```python
from googletrans import Translator
import pandas as pd

# pandas display options
pd.set_option('display.max_rows', 100)

dlang = pd.read_csv('https://github.com/prasertcbs/basic-dataset/raw/master/google_translate_language_code.csv')
dlang
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }

</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>language</th>
      <th>code</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Afrikaans</td>
      <td>af</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Irish</td>
      <td>ga</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Albanian</td>
      <td>sq</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Italian</td>
      <td>it</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Arabic</td>
      <td>ar</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Japanese</td>
      <td>ja</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Azerbaijani</td>
      <td>az</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Kannada</td>
      <td>kn</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Basque</td>
      <td>eu</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Korean</td>
      <td>ko</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Bengali</td>
      <td>bn</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Latin</td>
      <td>la</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Belarusian</td>
      <td>be</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Latvian</td>
      <td>lv</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Bulgarian</td>
      <td>bg</td>
    </tr>
    <tr>
      <th>15</th>
      <td>Lithuanian</td>
      <td>lt</td>
    </tr>
    <tr>
      <th>16</th>
      <td>Catalan</td>
      <td>ca</td>
    </tr>
    <tr>
      <th>17</th>
      <td>Macedonian</td>
      <td>mk</td>
    </tr>
    <tr>
      <th>18</th>
      <td>Chinese Simplified</td>
      <td>zh-CN</td>
    </tr>
    <tr>
      <th>19</th>
      <td>Malay</td>
      <td>ms</td>
    </tr>
    <tr>
      <th>20</th>
      <td>Chinese Traditional</td>
      <td>zh-TW</td>
    </tr>
    <tr>
      <th>21</th>
      <td>Maltese</td>
      <td>mt</td>
    </tr>
    <tr>
      <th>22</th>
      <td>Croatian</td>
      <td>hr</td>
    </tr>
    <tr>
      <th>23</th>
      <td>Norwegian</td>
      <td>no</td>
    </tr>
    <tr>
      <th>24</th>
      <td>Czech</td>
      <td>cs</td>
    </tr>
    <tr>
      <th>25</th>
      <td>Persian</td>
      <td>fa</td>
    </tr>
    <tr>
      <th>26</th>
      <td>Danish</td>
      <td>da</td>
    </tr>
    <tr>
      <th>27</th>
      <td>Polish</td>
      <td>pl</td>
    </tr>
    <tr>
      <th>28</th>
      <td>Dutch</td>
      <td>nl</td>
    </tr>
    <tr>
      <th>29</th>
      <td>Portuguese</td>
      <td>pt</td>
    </tr>
    <tr>
      <th>30</th>
      <td>English</td>
      <td>en</td>
    </tr>
    <tr>
      <th>31</th>
      <td>Romanian</td>
      <td>ro</td>
    </tr>
    <tr>
      <th>32</th>
      <td>Esperanto</td>
      <td>eo</td>
    </tr>
    <tr>
      <th>33</th>
      <td>Russian</td>
      <td>ru</td>
    </tr>
    <tr>
      <th>34</th>
      <td>Estonian</td>
      <td>et</td>
    </tr>
    <tr>
      <th>35</th>
      <td>Serbian</td>
      <td>sr</td>
    </tr>
    <tr>
      <th>36</th>
      <td>Filipino</td>
      <td>tl</td>
    </tr>
    <tr>
      <th>37</th>
      <td>Slovak</td>
      <td>sk</td>
    </tr>
    <tr>
      <th>38</th>
      <td>Finnish</td>
      <td>fi</td>
    </tr>
    <tr>
      <th>39</th>
      <td>Slovenian</td>
      <td>sl</td>
    </tr>
    <tr>
      <th>40</th>
      <td>French</td>
      <td>fr</td>
    </tr>
    <tr>
      <th>41</th>
      <td>Spanish</td>
      <td>es</td>
    </tr>
    <tr>
      <th>42</th>
      <td>Galician</td>
      <td>gl</td>
    </tr>
    <tr>
      <th>43</th>
      <td>Swahili</td>
      <td>sw</td>
    </tr>
    <tr>
      <th>44</th>
      <td>Georgian</td>
      <td>ka</td>
    </tr>
    <tr>
      <th>45</th>
      <td>Swedish</td>
      <td>sv</td>
    </tr>
    <tr>
      <th>46</th>
      <td>German</td>
      <td>de</td>
    </tr>
    <tr>
      <th>47</th>
      <td>Tamil</td>
      <td>ta</td>
    </tr>
    <tr>
      <th>48</th>
      <td>Greek</td>
      <td>el</td>
    </tr>
    <tr>
      <th>49</th>
      <td>Telugu</td>
      <td>te</td>
    </tr>
    <tr>
      <th>50</th>
      <td>Gujarati</td>
      <td>gu</td>
    </tr>
    <tr>
      <th>51</th>
      <td>Thai</td>
      <td>th</td>
    </tr>
    <tr>
      <th>52</th>
      <td>Haitian Creole</td>
      <td>ht</td>
    </tr>
    <tr>
      <th>53</th>
      <td>Turkish</td>
      <td>tr</td>
    </tr>
    <tr>
      <th>54</th>
      <td>Hebrew</td>
      <td>iw</td>
    </tr>
    <tr>
      <th>55</th>
      <td>Ukrainian</td>
      <td>uk</td>
    </tr>
    <tr>
      <th>56</th>
      <td>Hindi</td>
      <td>hi</td>
    </tr>
    <tr>
      <th>57</th>
      <td>Urdu</td>
      <td>ur</td>
    </tr>
    <tr>
      <th>58</th>
      <td>Hungarian</td>
      <td>hu</td>
    </tr>
    <tr>
      <th>59</th>
      <td>Vietnamese</td>
      <td>vi</td>
    </tr>
    <tr>
      <th>60</th>
      <td>Icelandic</td>
      <td>is</td>
    </tr>
    <tr>
      <th>61</th>
      <td>Welsh</td>
      <td>cy</td>
    </tr>
    <tr>
      <th>62</th>
      <td>Indonesian</td>
      <td>id</td>
    </tr>
    <tr>
      <th>63</th>
      <td>Yiddish</td>
      <td>yi</td>
    </tr>
  </tbody>
</table>
</div>

```python
translator = Translator() # create object/instance from Translator class
r=translator.translate('สวัสดี', dest='ja', src='th')
print(f'{r.text}: {r.pronunciation}')
```

こんにちは！: Kon'nichiwa!

```python
r=translator.translate('こんにちは', dest='ko')
print(f'{r.text}: {r.pronunciation}')
```

```
안녕하세요: annyeonghaseyo
```

```python
r=translator.translate('안녕하세요', dest='th')
print(f'{r.text}: {r.pronunciation}')
```

```
สวัสดี: S̄wạs̄dī
```

```python
r=translator.translate("life is beautiful", dest='th')
r.text
```

```
'ชีวิตช่างสวยงาม'
```

```python
r=translator.translate("life is beautiful", dest='it')
r.text
```

```
'la vita è bella'
```

```python
r=translator.translate("ฉันรักคุณ", dest='ja')
print(f'{r.text}: {r.pronunciation}')
```

```
わたしは、あなたを愛しています: Watashi wa, anata o aishiteimasu
```

```python
r=translator.translate('わたしは、あなたを愛しています', dest='th')
print(f'{r.text}: {r.pronunciation}')
```

```
ฉันรักคุณ: C̄hạn rạk khuṇ
```

```python
words=['water', 'toilet', 'thank you']
translations = translator.translate(words, dest='th')
for t in translations:
    print(f'{t.origin} -> {t.text} ({t.pronunciation})')
```

```
 water -> น้ำ (N̂ả)
toilet -> ห้องน้ำ (H̄̂xngn̂ả)
thank you -> ขอบคุณ (None)
```

```python
words=['hello', 'thank you', 'water', 'toilet', 'thank you', 'egg tart', 'muffin', 'green tea']

for w in words:
    for lang in ['th', 'ja', 'de']:
        t=translator.translate(w, dest=lang)
        print(f'{w} -> {t.text} ({t.pronunciation})')
```

```
  hello -> สวัสดี (S̄wạs̄dī)
  hello -> こんにちは (Kon'nichiwa)
  hello -> Hallo (None)
  thank you -> ขอบคุณ (None)
  thank you -> ありがとうございました (None)
  thank you -> Vielen Dank (thank you)
  water -> น้ำ (N̂ả)
  water -> 水 (Mizu)
  water -> Wasser (None)
  toilet -> トイレ (Toire)
  toilet -> Toilette (None)
  thank you -> ขอบคุณ (None)
  thank you -> ありがとうございました (None)
  thank you -> Vielen Dank (thank you)
  egg tart -> ทาร์ตไข่ (None)
  egg tart -> エッグタルト (None)
  egg tart -> Eitörtchen (egg tart)
  muffin -> มัฟฟิน (Mạffin)
  muffin -> マフィン (Mafin)
   muffin -> Muffin (None)
  green tea -> ชาเขียว (None)
  green tea -> 緑茶 (None)
  green tea -> grüner Tee (green tea)
```

```python
words=['สวัสดี', 'ขอบคุณ', 'ข้าว', 'น้ำ', 'ชา', 'กาแฟ']

for w in words:
    for lang in ['en', 'ja', 'fr']:
        t=translator.translate(w, dest=lang)
        print(f'{w} -> {t.text} | {t.pronunciation} ({lang})')
```

```
สวัสดี -> Hello! | None (en)
สวัสดี -> こんにちは！ | Kon'nichiwa! (ja)
สวัสดี -> salut! | None (fr)
ขอบคุณ -> thank | None (en)
ขอบคุณ -> 感謝 | Kansha (ja)
ขอบคุณ -> remercier | None (fr)
ข้าว -> rice | None (en)
ข้าว -> ご飯 | Gohan (ja)
ข้าว -> riz | None (fr)
น้ำ -> water | None (en)
น้ำ -> 水 | Mizu (ja)
น้ำ -> l'eau | None (fr)
ชา -> tea | None (en)
ชา -> お茶 | Ocha (ja)
ชา -> thé | None (fr)
กาแฟ -> coffee | None (en)
กาแฟ -> コーヒー | Kōhī (ja)
กาแฟ -> café | None (fr)
```

## translate and save to CSV, Excel

```python
words=['สวัสดี', 'ขอบคุณ', 'ข้าว', 'น้ำ', 'ชา', 'กาแฟ', 'โรงแรม', 'ห้องน้ำ', 'สนามบิน', 'ร้านอาหาร']
df=pd.DataFrame(words, columns=['th'])
df
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }

</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>th</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>สวัสดี</td>
    </tr>
    <tr>
      <th>1</th>
      <td>ขอบคุณ</td>
    </tr>
    <tr>
      <th>2</th>
      <td>ข้าว</td>
    </tr>
    <tr>
      <th>3</th>
      <td>น้ำ</td>
    </tr>
    <tr>
      <th>4</th>
      <td>ชา</td>
    </tr>
    <tr>
      <th>5</th>
      <td>กาแฟ</td>
    </tr>
    <tr>
      <th>6</th>
      <td>โรงแรม</td>
    </tr>
    <tr>
      <th>7</th>
      <td>ห้องน้ำ</td>
    </tr>
    <tr>
      <th>8</th>
      <td>สนามบิน</td>
    </tr>
    <tr>
      <th>9</th>
      <td>ร้านอาหาร</td>
    </tr>
  </tbody>
</table>
</div>

```python
df.to_csv('basic_th.csv', index=False)
```

```python
df = pd.read_csv('basic_th.csv')
df
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }

</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>th</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>สวัสดี</td>
    </tr>
    <tr>
      <th>1</th>
      <td>ขอบคุณ</td>
    </tr>
    <tr>
      <th>2</th>
      <td>ข้าว</td>
    </tr>
    <tr>
      <th>3</th>
      <td>น้ำ</td>
    </tr>
    <tr>
      <th>4</th>
      <td>ชา</td>
    </tr>
    <tr>
      <th>5</th>
      <td>กาแฟ</td>
    </tr>
    <tr>
      <th>6</th>
      <td>โรงแรม</td>
    </tr>
    <tr>
      <th>7</th>
      <td>ห้องน้ำ</td>
    </tr>
    <tr>
      <th>8</th>
      <td>สนามบิน</td>
    </tr>
    <tr>
      <th>9</th>
      <td>ร้านอาหาร</td>
    </tr>
  </tbody>
</table>
</div>

```python
lang=['en', 'la', 'fr', 'ja', 'zh-CN', 'fa']
for dest in lang:
    df[dest]=df.apply(lambda r: translator.translate(r['th'], dest=dest).text, axis=1)
df
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }

</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>th</th>
      <th>en</th>
      <th>la</th>
      <th>fr</th>
      <th>ja</th>
      <th>zh-CN</th>
      <th>fa</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>สวัสดี</td>
      <td>Hello!</td>
      <td>Salve!</td>
      <td>salut!</td>
      <td>こんにちは！</td>
      <td>你好！</td>
      <td>سلام!</td>
    </tr>
    <tr>
      <th>1</th>
      <td>ขอบคุณ</td>
      <td>thank</td>
      <td>gratias ago</td>
      <td>remercier</td>
      <td>感謝</td>
      <td>谢谢</td>
      <td>تشکر</td>
    </tr>
    <tr>
      <th>2</th>
      <td>ข้าว</td>
      <td>rice</td>
      <td>rice</td>
      <td>riz</td>
      <td>ご飯</td>
      <td>白饭</td>
      <td>برنج</td>
    </tr>
    <tr>
      <th>3</th>
      <td>น้ำ</td>
      <td>water</td>
      <td>aqua</td>
      <td>l'eau</td>
      <td>水</td>
      <td>水</td>
      <td>اب</td>
    </tr>
    <tr>
      <th>4</th>
      <td>ชา</td>
      <td>tea</td>
      <td>tea</td>
      <td>thé</td>
      <td>お茶</td>
      <td>茶</td>
      <td>چای</td>
    </tr>
    <tr>
      <th>5</th>
      <td>กาแฟ</td>
      <td>coffee</td>
      <td>capulus</td>
      <td>café</td>
      <td>コーヒー</td>
      <td>咖啡</td>
      <td>قهوه</td>
    </tr>
    <tr>
      <th>6</th>
      <td>โรงแรม</td>
      <td>hotel</td>
      <td>deversorium</td>
      <td>Hôtel</td>
      <td>ホテル</td>
      <td>旅馆</td>
      <td>هتل</td>
    </tr>
    <tr>
      <th>7</th>
      <td>ห้องน้ำ</td>
      <td>toilet</td>
      <td>CULTUS</td>
      <td>toilette</td>
      <td>トイレ</td>
      <td>厕所</td>
      <td>توالت</td>
    </tr>
    <tr>
      <th>8</th>
      <td>สนามบิน</td>
      <td>airport</td>
      <td>aeroportus</td>
      <td>aéroport</td>
      <td>空港</td>
      <td>飞机场</td>
      <td>فرودگاه</td>
    </tr>
    <tr>
      <th>9</th>
      <td>ร้านอาหาร</td>
      <td>Restaurant</td>
      <td>popina</td>
      <td>Restaurant</td>
      <td>飲食店</td>
      <td>餐厅</td>
      <td>رستوران</td>
    </tr>
  </tbody>
</table>
</div>

```python
df.to_csv('translation.csv', index=False)
df.to_excel('translation.xlsx', index=False)
```

อีกหนึ่งตัวอย่างการนำไปใช้งาน


```py
‘’’
Create By Joompot Sriyapan
Date 29/3/2019
Name
  Google Translate Example 1
Description
  แปลภาษาอังกฤษเป็นไทยด้วย Python
Required
  python 3.7.3
  googletrans 2.4.0
Pre-programmed
  pip install googletrans
‘’’
from googletrans import Translator
T = Translator()
source = “Hello, world”
try:
  dest = T.translate(source,src=”en”,dest=”th”).text
  print(dest)
except:
  print (“Error!!!”)

```
>Reference : - https://medium.com/@JoTaijiquan/google-translate-with-python-2b4db669f6fa

---------------


## goslate

ิอีกโมดูลหนึ่งคือ goslate เป็นโมดูลที่นำ Google Translate มาใช้งานร่วมกับ Python รองรับทั้ง Python 2 และ Python 3 (License: MIT) https://pypi.python.org/pypi/goslate

สามารถติดตั้งได้ง่าย ๆ โดยใช้คำสั่ง pip ดังนี้ครับ
```
pip install goslate
```
ในการใช้งานสามารถใช้งานได้ง่าย ๆ ดังนี้ครับ

gs.translate('ข้อความ', 'รหัสภาษา เช่น en คือ ภาษาอังกฤษ th คือ ภาษาไทย')

ตัวอย่าง

```
>>> import goslate
>>> gs = goslate.Goslate()
>>> print(gs.translate('hello world', 'th')) #
สวัสดีชาวโลก
>>> print(gs.translate('สวัสดีชาวโลก', 'en'))
Hello world!
```

ตัวอย่างการนำไปประยุกต์ใช้

นำโมดูล SpeechRecognition มาใช้รับเสียงจากชาวต่างชาติ แล้วใช้โมดูล goslate มาแปลเป็นข้อความภาษาไทย

```py
import goslate
import speech_recognition as sr
gs = goslate.Goslate()
r = sr.Recognizer()
with sr.Microphone() as source:                # เรียกใช้  Microphone พื้นฐานของระบบ
    audio = r.listen(source)                   # รับเสียงเข้ามาแล้วประมวลผลส่งไปยัง Google Speech Recognition API
try:
    a = r.recognize(audio)
    b = gs.translate(a, 'th')     # แสดงข้อความจากเสียงด้วย Google Speech Recognition
    print(b)
except LookupError:                            # ประมวลผลแล้วไม่รู้จักหรือเข้าใจเสียง
        print("Could not understand audio")
```

>Reference : https://python3.wannaphong.com/2015/01/python.html