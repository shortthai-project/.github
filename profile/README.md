# 🔗 ShortThai Project (ระบบย่อลิงก์ของคนไทย)

ยินดีต้อนรับสู่ **ShortThai Project**! ระบบย่อ URL (URL Shortener) ประสิทธิภาพสูงที่ออกแบบด้วยสถาปัตยกรรม Microservices เพื่อรองรับการขยายตัว (Scalability) และการทำงานที่รวดเร็ว

## 🏗️ System Architecture & Repositories

โปรเจคของเราแบ่งออกเป็น 4 Services หลัก และ 1 Infrastructure เพื่อให้แต่ละส่วนทำงานเป็นอิสระต่อกัน:

* 🌐 **[Frontend (Web)](https://github.com/shortthai-project/frontend):** ส่วนติดต่อผู้ใช้งาน (User Interface) สำหรับจัดการและสร้างลิงก์
* ⚙️ **[Backend (API)](https://github.com/shortthai-project/api):** ระบบ API หลักสำหรับจัดการ Business Logic ทั้งหมด
* 🚀 **[Redirector](https://github.com/shortthai-project/redirector):** Service ขนาดเล็กที่เน้นความเร็วสูงสุด (High Throughput) ทำหน้าที่รับ Short URL แล้ว Redirect ไปยัง URL ต้นทาง
* 👷 **[Worker](https://github.com/shortthai-project/worker):** Background Service สำหรับประมวลผลงานแบบ Asynchronous เช่น การเก็บสถิติการคลิก (Analytics)
* 🛠️ **[Infra](https://github.com/shortthai-project/infra):** ศูนย์รวมการตั้งค่า Infrastructure, Docker Compose, Database Schema และ Script สำหรับ Development/Production

---

## 💻 Getting Started (สำหรับนักพัฒนา)

เพื่อให้การทำงานร่วมกันและการตั้งค่าสภาพแวดล้อม (Environment) เป็นไปอย่างราบรื่นและไม่เกิดข้อผิดพลาดในการอ้างอิง Path ของ Docker ขอให้นักพัฒนาทุกคนทำตามขั้นตอนต่อไปนี้

### 1. สร้าง Workspace และ Clone Repositories

กรุณา Clone ทุก Repository ให้อยู่ใน**ระดับเดียวกัน (Sibling Directory)** โดยเปิด Terminal แล้วรันคำสั่งต่อไปนี้:

```bash
# สร้างโฟลเดอร์หลักสำหรับโปรเจค
mkdir shortthai-project
cd shortthai-project

# Clone ทุก Services
git clone https://github.com/shortthai-project/frontend.git
git clone https://github.com/shortthai-project/api.git
git clone https://github.com/shortthai-project/redirector.git
git clone https://github.com/shortthai-project/worker.git
git clone https://github.com/shortthai-project/infra.git
```

#### โครงสร้างโฟลเดอร์ของคุณควรจะออกมาเป็นแบบนี้

```plaintext
shortthai-project/
 ├── frontend/      (UI)
 ├── api/           (Core API)
 ├── redirector/    (Fast Redirect)
 ├── worker/        (Background Jobs)
 └── infra/         (Docker & Configs)
```

### 2. การรันระบบเพื่อพัฒนา (Local Development)

หลังจากวางโครงสร้างโฟลเดอร์เรียบร้อยแล้ว คุณสามารถรันระบบทั้งหมดได้ผ่าน Repo infra:

```bash
# เข้าไปที่โฟลเดอร์ infra
cd infra

# คัดลอกไฟล์ Environment Variables (ถ้ามี)
cp .env.example .env

# รันระบบทั้งหมดด้วย Docker Compose
docker-compose up -d --build
```
