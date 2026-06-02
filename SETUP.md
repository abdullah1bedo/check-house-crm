# Check House CRM - دليل الإعداد

## 🚀 البدء السريع

### 1. تثبيت البرامج المطلوبة
```bash
npm install
```

### 2. إعداد متغيرات البيئة
أنشئ ملف `.env.local` وأضف:
```
VITE_SUPABASE_URL=https://zhjlziafocmxudjlnkdl.supabase.co
VITE_SUPABASE_ANON_KEY=sb_publishable_w3fnZ6uSp_eXO-1Is3IeAQ_00ifzXON
```

### 3. إعداد قاعدة البيانات

روح إلى حسابك في Supabase وأنشئ الجداول التالية:

#### جدول العملاء (clients)
```sql
CREATE TABLE clients (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  name VARCHAR(255) NOT NULL,
  phone VARCHAR(20) NOT NULL,
  email VARCHAR(255),
  kitchen_length DECIMAL(10, 2),
  kitchen_width DECIMAL(10, 2),
  kitchen_height DECIMAL(10, 2),
  material_type VARCHAR(100),
  appliances_type VARCHAR(255),
  video_url VARCHAR(500),
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

#### جدول المشاريع (projects)
```sql
CREATE TABLE projects (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  client_id UUID REFERENCES clients(id) ON DELETE CASCADE,
  status VARCHAR(50) NOT NULL DEFAULT 'التصميم',
  price_per_meter DECIMAL(10, 2),
  quantity DECIMAL(10, 2),
  total_price DECIMAL(15, 2),
  notes TEXT,
  visit_date DATE,
  visit_photos VARCHAR(500),
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

#### جدول الدفعات (payments)
```sql
CREATE TABLE payments (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  project_id UUID REFERENCES projects(id) ON DELETE CASCADE,
  advance_payment DECIMAL(15, 2) DEFAULT 0,
  delivery_payment DECIMAL(15, 2) DEFAULT 0,
  warranty_payment DECIMAL(15, 2) DEFAULT 0,
  payment_date DATE NOT NULL,
  notes TEXT,
  warranty_end_date DATE,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

### 4. تشغيل التطبيق
```bash
npm run dev
```

سيفتح الموقع على: `http://localhost:3000`

## 📦 الإنشاء للإنتاج
```bash
npm run build
```

## 🔒 الأمان

- **لا تشارك الـ API Keys** مع أحد
- استخدم `.env.local` للمتغيرات الحساسة
- تأكد من إضافة `.env.local` إلى `.gitignore`

## 📞 الدعم الفني

للمساعدة في الإعداد أو حل المشاكل، تواصل مع فريق التطوير.
