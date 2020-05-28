---
title: Google Text-to-Speech.
subtitle: Text to Speech หรือ Speech synthesis เป็นเทคโนโลยีสังเคราะห์เสียงพูด โดยแปลงจากตัวอักษรให้กลายเป็นเสียงพูด โดย Text to Speech เป็นส่วนหนึ่งของสาขาการประมวลผลภาษาธรรมชาติ (Natural Language Processing) สำหรับ Text to Speech ภาษาไทย ปัจจุบันนี้ที่ยังมีให้บริการ API ตอนนี้มีเฉพาะของ Google Text to Speech
summary: Text to Speech หรือ Speech synthesis เป็นเทคโนโลยีสังเคราะห์เสียงพูด โดยแปลงจากตัวอักษรให้กลายเป็นเสียงพูด โดย Text to Speech เป็นส่วนหนึ่งของสาขาการประมวลผลภาษาธรรมชาติ (Natural Language Processing) สำหรับ Text to Speech ภาษาไทย ปัจจุบันนี้ที่ยังมีให้บริการ API ตอนนี้มีเฉพาะของ Google Text to Speech
authors:
  - admin
tags: ["gTTS","Text to Speech"]
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

doc: https://gtts.readthedocs.io/en/latest/module.html  
install: `pip install gTTS` 

author: Prasert Kanawattanachai  
YouTube: https://www.youtube.com/prasertcbs  
Chulalongkorn Business School  

{{< youtube SmdVSqSg0B0 >}}

```python

from IPython.display import Audio
import gtts
from gtts import gTTS
```

## รหัสภาษา

```py
gtts.lang.tts_langs(tld='com')
```

```
{'af': 'Afrikaans',
 'sq': 'Albanian',
 'ar': 'Arabic',
 'hy': 'Armenian',
 'bn': 'Bengali',
 'bs': 'Bosnian',
 'ca': 'Catalan',
 'hr': 'Croatian',
 'cs': 'Czech',
 'da': 'Danish',
 'nl': 'Dutch',
 'en': 'English',
 'eo': 'Esperanto',
 'et': 'Estonian',
 'tl': 'Filipino',
 'fi': 'Finnish',
 'fr': 'French',
 'de': 'German',
 'el': 'Greek',
 'gu': 'Gujarati',
 'hi': 'Hindi',
 'hu': 'Hungarian',
 'is': 'Icelandic',
 'id': 'Indonesian',
 'it': 'Italian',
 'ja': 'Japanese',
 'jw': 'Javanese',
 'kn': 'Kannada',
 'km': 'Khmer',
 'ko': 'Korean',
 'la': 'Latin',
 'lv': 'Latvian',
 'mk': 'Macedonian',
 'ml': 'Malayalam',
 'mr': 'Marathi',
 'my': 'Myanmar (Burmese)',
 'ne': 'Nepali',
 'no': 'Norwegian',
 'pl': 'Polish',
 'pt': 'Portuguese',
 'ro': 'Romanian',
 'ru': 'Russian',
 'sr': 'Serbian',
 'si': 'Sinhala',
 'sk': 'Slovak',
 'es': 'Spanish',
 'su': 'Sundanese',
 'sw': 'Swahili',
 'sv': 'Swedish',
 'ta': 'Tamil',
 'te': 'Telugu',
 'th': 'Thai',
 'tr': 'Turkish',
 'uk': 'Ukrainian',
 'ur': 'Urdu',
 'vi': 'Vietnamese',
 'cy': 'Welsh',
 'zh-cn': 'Chinese (Mandarin/China)',
 'zh-tw': 'Chinese (Mandarin/Taiwan)',
 'en-us': 'English (US)',
 'en-ca': 'English (Canada)',
 'en-uk': 'English (UK)',
 'en-gb': 'English (UK)',
 'en-au': 'English (Australia)',
 'en-gh': 'English (Ghana)',
 'en-in': 'English (India)',
 'en-ie': 'English (Ireland)',
 'en-nz': 'English (New Zealand)',
 'en-ng': 'English (Nigeria)',
 'en-ph': 'English (Philippines)',
 'en-za': 'English (South Africa)',
 'en-tz': 'English (Tanzania)',
 'fr-ca': 'French (Canada)',
 'fr-fr': 'French (France)',
 'pt-br': 'Portuguese (Brazil)',
 'pt-pt': 'Portuguese (Portugal)',
 'es-es': 'Spanish (Spain)',
 'es-us': 'Spanish (United States)'}

 ```

## การใช้ gTTS

 ```py
tts = gTTS('hello', lang='en')
tts.save('speech.mp3')

tts = gTTS('สวัสดีครับ', lang='th')
tts.save('speech.mp3')

tts = gTTS('ถึงม้วยดินสิ้นฟ้ามหาสมุทร ไม่สิ้นสุดความรักสมัครสมาน', lang='th')
tts.save('speech.mp3')

tts = gTTS('こんにちは', lang='ja')
tts.save('speech.mp3')

tts = gTTS('非常感谢你', lang='zh-cn')
tts.save('speech.mp3')

tts = gTTS('北，南，东，西', lang='zh-cn')
tts.save('speech.mp3')

tts = gTTS('la vita è bella', lang='it')
tts.save('speech_it.mp3')
Audio('speech_it.mp3', autoplay=True)

 ```

## การเปิดเล่นไฟล์เสียงโดยตรงบน Jupyter Notebook

 ```py
 Audio('speech.mp3', autoplay=True)
```