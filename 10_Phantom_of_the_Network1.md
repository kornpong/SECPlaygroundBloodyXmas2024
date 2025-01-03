## ข้อ Phantom of the Network เป็นข้อ Web อีกข้อที่อยู่ในหมวด Incident ข้อแรก

> 🏆 **Challenge**: ![Solved](https://img.shields.io/badge/status-unsolved-red)   
> 💪 **Difficulty**:  🟠 MEDIUM  
> 🎯 **Category**: Web Application Security

<img src="./resources/87.png" alt="" style="width:60% !important;">

### **เริ่มการวิเคราะห์:**  
เมื่อทำการตรวจสอบ พบว่าข้อนี้มีการเปิดใช้งาน **2 พอร์ตสำคัญ:** 80 และ 8080 🔎  

#### **ปริศนาแรกบน Web Port 80**  
- บน Port นี้ มีข้อมูล **Hash** 2 ชุดที่สะดุดตา:  
  - `46bdc56266eeb01a426c3c2bedbaaedd8885d7b5081afd15401930e61957cd96`  
  - `6557739a67283a8de383fc5c0997fbec7c5721a46f28f3235fc9607598d9016b`  
  
  <img src="./resources/88.png" alt="" style="width:60% !important;">

- เมื่อทำการ **Decrypt** ได้คำว่า **'xmas'** และ **'2024'**! 🎄🎅  
<img src="./resources/89.png" alt="" style="width:60% !important;">


#### **Port 8080 กับความลับที่ซ่อนอยู่**  
- พบว่ารัน **Apache HTTP Server 2.4.49** ซึ่งมี **CVE-2021-41773** (ช่องโหว่ Path Traversal & Remote Code Execution) 🛠️  
- เลือกใช้ **POC (Proof of Concept)** จาก **exploit-db** เพื่อเริ่มการโจมตี:  
  [https://www.exploit-db.com/exploits/50383](https://www.exploit-db.com/exploits/50383)  
  <img src="./resources/91.png" alt="" style="width:60% !important;">
  <img src="./resources/92.png" alt="" style="width:60% !important;">

---

### **ทำการ Run OS Command:**  
- เมื่อ Exploit สำเร็จ พบว่าไฟล์ Flag น่าจะซ่อนอยู่ที่ `/var/www/flag.txt` 📄✨  
- **แต่!!!** การเข้าถึงไฟล์นี้จำเป็นต้องมีสิทธิ์ **root** 💡  
- ต้องดำเนินการต่อโดยสร้าง **Reverse Shell** เพื่อยกระดับสิทธิ์
<img src="./resources/93.png" alt="" style="width:60% !important;">

---

#### **ด่านถัดไป: การยกระดับสิทธิ์!**  
- ใช้ **linpeas.sh** ซึ่งเป็น **Linux Privilege Escalation Awesome Script**  
  สำหรับตรวจสอบแนวทางในการยกระดับสิทธิ์ 🔍  
  [https://github.com/peass-ng/PEASS-ng/tree/master/linPEAS](https://github.com/peass-ng/PEASS-ng/tree/master/linPEAS)  
  

- ทดสอบทุกวิธีที่ Script ชี้แนะ แต่...  
<img src="./resources/94.png" alt="" style="width:60% !important;">
<img src="./resources/95.png" alt="" style="width:60% !important;">


**ผลลัพธ์ที่ไม่คาดหวัง:**  

- **ไม่สามารถยกระดับสิทธิ์** และ **ไม่สามารถอ่าน Flag ได้!** 🚫🚩  

### **บทสรุปอันขมขื่น** 
 
แม้จะพยายามเต็มที่ แต่ก็ยังไม่สามารถไขปริศนาและหา flag ได้ **ความท้าทายนี้ยังคงต้องรอการไข!** 🧩⏳

---
###### Written by Kornpong.m
###### #SECPlayground   #SECPlaygroundBloodyXMas2024 

<a href="./"><<กลับหน้าหลัก</a>  