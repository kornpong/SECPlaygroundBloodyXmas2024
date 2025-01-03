## ข้อ Santa's Math

> 🏆 **Challenge**: ![Solved](https://img.shields.io/badge/status-unsolved-red)   
> 💪 **Difficulty**:  🟢 EASY  
> 🎯 **Category**: Web Application Security

<img src="./resources/76.png" alt="" style="width:60% !important;">

### เริ่มการวิเคราะห์...
ทำการสแกน path ด้วย Dirsearch พบ path ที่น่าสงสัย: **/assets/** และ **/robots.txt** 🔍

<img src="./resources/77.png" alt="" style="width:60% !important;">
<img src="./resources/78.png" alt="" style="width:60% !important;">

**ที่หน้าแรกก็พบกับหน้าเว็บปริศนา!** เมื่อเข้าไป พบ prompt สำหรับกรอก Password และเห็นไฟล์ชื่อ **index.js** ซึ่งดูเหมือนจะเป็น **JavaScript Obfuscate**! 🕵️‍♂️

<img src="./resources/79.png" alt="" style="width:60% !important;">

**ถอดรหัสเวลา**:
เมื่อทำการ **deobfuscate** โค้ด พบ key ที่ซ่อนอยู่: **'Santa@2024'** 🔑🎅

<img src="./resources/80.png" alt="" style="width:60% !important;">
<img src="./resources/81.png" alt="" style="width:60% !important;">

หลังผ่าน prompt... หน้าเว็บเปลี่ยนเป็นแบบ **Interactive** ให้กรอกผลลัพธ์ของ **การบวกเลข** 👩‍🏫 ➕

<img src="./resources/82.png" alt="" style="width:60% !important;">

**จุดพลิกเกม!**
เมื่อถึงคำถาม: `0.1 + 0.2` 🖩 

ต้องตอบผลลัพธ์เป็น: **0.30000000000000004** (เนื่องจาก Floating-Point Precision ในโปรแกรมคอมพิวเตอร์) 🤯

---

**เซอร์ไพรส์!**
หลังตอบคำถามถูก Popup เด้งขึ้นพร้อมข้อความ:
> \"Congratulations this is your flag !\"

แต่... **ดราม่า:** 
> \"I have the flag, but I won't give it to you because I'm a chill person.\" 🧊😎

<img src="./resources/83.png" alt="" style="width:60% !important;">
<img src="./resources/84.png" alt="" style="width:60% !important;">

ลองค้นต่อใน **Cookies** ไม่เจออะไรเลย 🧹🔍

สังเกตเห็นไฟล์รูปชื่อ **chill.png**! ✨

เมื่อทำการเปิดดู **Information** ของรูป **ยังไม่พบเบาะแสอะไรอีก!** 📂❓

<img src="./resources/85.png" alt="" style="width:60% !important;">
<img src="./resources/86.png" alt="" style="width:60% !important;">

**บทสรุป:** แม้จะทำจนสุดความสามารถ แต่ยังหา **Flag** ไม่เจอ 🚩⏳
ประสบการณ์ครั้งนี้ยังถือว่าเป็นการเรียนรู้ที่สนุกและน่าตื่นเต้น! 💡🎉

---
###### Written by Kornpong.m
###### #SECPlayground   #SECPlaygroundBloodyXMas2024 

<a href="./"><<กลับหน้าหลัก</a>