# Microservices Patterns 
![image](https://microservices.io/i/MicroservicePatternLanguage.jpg)
https://microservices.io/patterns/index.html
#
ภาพนี้แสดง **The Microservice Architecture Pattern Language** ซึ่งเป็นแผนภาพโครงสร้างที่อธิบายแนวทางและรูปแบบต่าง ๆ สำหรับการออกแบบ **สถาปัตยกรรมไมโครเซอร์วิส (Microservices Architecture)** โดยแบ่งออกเป็นหมวดหมู่หลัก ๆ ดังนี้:

#

### **1. Application Patterns (รูปแบบของแอปพลิเคชัน)**
   - **Decomposition (การแบ่งระบบเป็นส่วนย่อย)**
     - *Decompose by business capability*: แบ่งแอปพลิเคชันตามความสามารถทางธุรกิจ
     - *Decompose by subdomain*: แบ่งตามโดเมนย่อย (ใช้หลัก DDD - Domain Driven Design)
     - *`Self-contained Service`*: บริการที่สามารถทำงานได้ด้วยตนเองโดยไม่ต้องรอผลจากบริการอื่น
     - *`Service per team`*: บริการที่ออกแบบให้ตรงกับโครงสร้างทีม

   - **Database Architecture (สถาปัตยกรรมฐานข้อมูล)**
     - *Shared database*: หลายบริการใช้ฐานข้อมูลเดียวกัน
     - *`Database per service`*: แต่ละบริการมีฐานข้อมูลของตัวเอง

   - **Data Patterns (รูปแบบการจัดการข้อมูล)**
     - *`API Composition`*: รวมข้อมูลจากหลายบริการผ่าน API
     - *CQRS (Command Query Responsibility Segregation)*: แยกคำสั่ง (Command) และการอ่านข้อมูล (Query)

   - **Maintaining Data Consistency (การรักษาความสอดคล้องของข้อมูล)**
     - *Saga*: ใช้ลำดับของธุรกรรมกระจาย (Distributed Transactions) เพื่อรักษาความสอดคล้องของข้อมูล
     - *Domain event*: อิงกับเหตุการณ์ (Event-Driven)
     - *Event Sourcing*: จัดเก็บสถานะของข้อมูลโดยใช้เหตุการณ์แทนค่าล่าสุด
     - *Aggregate*: องค์ประกอบที่ช่วยจัดกลุ่มข้อมูลในโดเมนเดียวกัน

#

### **2. Application Infrastructure Patterns (โครงสร้างพื้นฐานของแอปพลิเคชัน)**
   - **Cross-cutting concerns (ความกังวลที่ครอบคลุมทั้งระบบ)**
     - *Microservice Chassis*: เฟรมเวิร์กที่ช่วยบริหารจัดการไมโครเซอร์วิส
     - *Externalized configuration*: แยกการตั้งค่าระบบออกจากโค้ด
     - *Service Template*: โครงสร้างมาตรฐานสำหรับบริการ 

   - **Security (ความปลอดภัย)**
     - *`Access Token`*: ใช้สำหรับการรับรองสิทธิ์และการเข้าถึงระบบ

#

### **3. Communication Patterns (รูปแบบการสื่อสารระหว่างบริการ)**
   - **Communication Style (รูปแบบการสื่อสาร)**
     - *Remote Procedure Invocation (RPI)*: เรียกใช้ฟังก์ชันของบริการอื่นผ่าน API
     - *Messaging*: ใช้การส่งข้อความแบบอะซิงโครนัส (Asynchronous Messaging)
     - *Domain-specific*: การสื่อสารที่เหมาะสมกับโดเมนเฉพาะ

   - **Reliability (ความน่าเชื่อถือ)**
     - *`Circuit Breaker`*: ป้องกันการเรียกใช้บริการที่ล้มเหลวซ้ำ ๆ

   - **Transactional Messaging (การจัดการธุรกรรมด้วยการส่งข้อความ)**
     - *Transactional Outbox*: จัดการการส่งข้อความให้อยู่ในธุรกรรมฐานข้อมูล
     - *Transaction log tailing*: ใช้บันทึกการเปลี่ยนแปลงในฐานข้อมูลเพื่อตรวจสอบความถูกต้องของธุรกรรม
     - *Polling Publisher*: ตรวจสอบและเผยแพร่ข้อความที่เกี่ยวข้องกับธุรกรรม

#

### **4. Infrastructure Patterns (รูปแบบของโครงสร้างพื้นฐาน)**
   - **Deployment (การปรับใช้บริการ)**
     - *Multiple Services per Host*: รันหลายบริการบนเครื่องเดียวกัน
     - *`Single Service per Host`*: หนึ่งโฮสต์ต่อหนึ่งบริการ
     - *`Service-per-Container`*: บริการแต่ละตัวทำงานในคอนเทนเนอร์ของตัวเอง
     - *Service-per-VM*: บริการแต่ละตัวทำงานใน Virtual Machine ของตัวเอง
     - *Serverless deployment*: ใช้แพลตฟอร์มที่ไม่มีเซิร์ฟเวอร์
     - *Service mesh*: เครือข่ายบริการที่ช่วยจัดการการสื่อสารระหว่างไมโครเซอร์วิส

   - **Discovery (การค้นหาบริการ)**
     - *`Client-side discovery`*: ไคลเอนต์ค้นหาบริการโดยตรงจากรีจิสทรี
     - *Server-side discovery*: ตัวจัดการกลางช่วยไคลเอนต์ค้นหาบริการ
     - *Service registry*: ฐานข้อมูลกลางสำหรับเก็บรายการบริการ
     - *3rd party registration*: การลงทะเบียนบริการผ่านแพลตฟอร์มของบุคคลที่สาม
     - *Self registration*: บริการลงทะเบียนตัวเองเข้ากับระบบ

#
### **5. Observability (การตรวจสอบและเฝ้าระวังระบบ)**
   - *Audit logging*: บันทึกกิจกรรมในระบบ
   - *Distributed tracing*: ติดตามการทำงานของคำขอที่ไหลผ่านหลายบริการ
   - *`Health check API`*: ตรวจสอบสถานะของบริการ
   - *`Exception tracking`*: ติดตามข้อผิดพลาดในระบบ
   - *`Log aggregation`*: รวมบันทึกจากหลายแหล่งเพื่อวิเคราะห์ข้อมูล
   - *Log deployments and changes*: ตรวจสอบการปรับใช้และเปลี่ยนแปลงระบบ

#

### **6. External API (API สำหรับการเข้าถึงจากภายนอก)**
   - *`API gateway`*: จุดศูนย์กลางที่ช่วยจัดการคำขอจากไคลเอนต์ไปยังหลายบริการ
   - *`Backend for frontends (BFF)`*: API ที่ออกแบบเฉพาะสำหรับไคลเอนต์แต่ละประเภท (เช่น มือถือ vs เว็บ)

#

### **7. Testing (การทดสอบ)**
   - *Consumer-driven contract test*: ทดสอบสัญญาการสื่อสารระหว่างบริการ
   - *`Service Component Test`*: ทดสอบแต่ละบริการในสภาพแวดล้อมจำลอง
   - *Client-side UI composition*: รวม UI หลายส่วนจากหลายบริการ
   - *Server-side page fragment composition*: รวม UI หลายส่วนที่ฝั่งเซิร์ฟเวอร์

#

### **สรุป**
ภาพนี้ให้โครงสร้างของ **Microservices Architecture** โดยแสดงรูปแบบหลัก ๆ ในการออกแบบและปรับใช้ระบบไมโครเซอร์วิส ครอบคลุมตั้งแต่การแบ่งบริการ การสื่อสาร การรักษาความสอดคล้องของข้อมูล การปรับใช้ ไปจนถึงการสังเกตการณ์และการทดสอบ 

#
อ้างอิง: https://microservices.io/patterns/index.html
