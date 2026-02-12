# 📧 Email Yönetim Sistemi (Email Management System)

## Kullanıcı İsteği

> "Peki sadece mail atmak değil attığım maile gelen cevaplarıda programdan görmek ve cevap vermek istesem hiç maili açmadan tüm trafiği programdan halletmek? mümkün mü?"

**Cevap:** EVET! Kesinlikle mümkün ve harika bir özellik olacak! 🎉

---

## 🎯 Özellik Özeti

### Ne Eklenecek?

**1. 📥 Email Gelen Kutusu**
- Tüm gelen emailleri görüntüleme
- Tedarikçiye göre filtreleme
- Email zincirlerini / konuşmaları görme
- Okundu/okunmadı işaretleme
- Arşivleme/silme
- Arama fonksiyonu

**2. 💬 Cevaplama Özelliği**
- Program içinden direkt cevap
- Orijinal mesajı alıntılama
- Dosya ekleme
- Metin formatlama
- Cevap gönderme

**3. 🔄 Email Zinciri Görünümü**
- Tam konuşma geçmişi
- Gönderilen ve alınan mesajları takip
- Tedarikçi verisine bağlantı
- Zaman damgaları
- Görsel zincir yapısı

**4. 📊 Email Dashboard**
- Okunmamış sayısı
- Bekleyen cevaplar
- Önemli emailler
- İstatistikler
- Hızlı aksiyonlar

---

## 🖥️ Kullanıcı Arayüzü Tasarımı

```
┌──────────────────────────────────────────────────────────────────┐
│ 📧 Email Gelen Kutusu                  [🔄 Yenile] [🔍 Ara...]  │
├───────────────────────┬──────────────────────────────────────────┤
│ EMAIL LİSTESİ         │ EMAIL GÖRÜNTÜLEYICI                      │
│ (Sol Panel)           │ (Sağ Panel)                              │
├───────────────────────┼──────────────────────────────────────────┤
│                       │                                          │
│ 📩 Tedarikçi A        │ Kimden: tedarikciler@example.com         │
│    Teslimat gecikti   │ Kime: sizin@defacto.com                  │
│    12 Şub 10:30       │ Konu: Re: Teslimat Gecikmesi Takibi     │
│    ▸ 3 mesaj          │ Tarih: 12 Şubat 2024, 10:30             │
│                       │ ───────────────────────────────────────  │
│ ✅ Tedarikçi B        │                                          │
│    Fiyat teklifi      │ Sayın Defacto Ekibi,                     │
│    11 Şub 14:20       │                                          │
│    ▸ 1 mesaj          │ Siparişiniz yarın teslim edilecektir.   │
│                       │ Gecikmeden dolayı özür dileriz.          │
│ 📩 Tedarikçi C        │                                          │
│    Kalite raporu      │ Detaylar ektedir.                        │
│    11 Şub 09:15       │                                          │
│    ▸ 2 mesaj          │ Saygılarımızla,                          │
│                       │ Tedarikçi A                              │
│ ──────────────────    │                                          │
│ [Tümü] [Okunmamış]   │ 📎 Ek: teslimat_raporu.pdf (245 KB)     │
│ [Tedarikçi ▼]        │                                          │
│ [Tarih ▼]            │ ───────────────────────────────────────  │
│                       │ [💬 Cevapla] [➡️ İlet] [🗑️ Sil]        │
│ (200 email)           │ [📁 Arşivle] [⭐ Önemli]                │
└───────────────────────┴──────────────────────────────────────────┘
```

---

## 🔧 Teknik Uygulama

### Gerekli Kütüphaneler

```python
import imaplib              # IMAP email okuma
import smtplib              # SMTP email gönderme (mevcut)
import email                # Email parsing
from email.mime.text import MIMEText
from email.mime.multipart import MIMEMultipart
from email.mime.base import MIMEBase
from email import encoders
import sqlite3              # Lokal email veritabanı
import html2text            # HTML'den text'e çevirme
from datetime import datetime, timedelta
import re                   # Email parsing için
```

### Veritabanı Şeması

```sql
-- Emailler tablosu
CREATE TABLE emails (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    message_id TEXT UNIQUE NOT NULL,
    from_addr TEXT NOT NULL,
    to_addr TEXT,
    cc_addr TEXT,
    subject TEXT,
    body TEXT,
    html_body TEXT,
    date TIMESTAMP NOT NULL,
    read INTEGER DEFAULT 0,
    replied INTEGER DEFAULT 0,
    forwarded INTEGER DEFAULT 0,
    important INTEGER DEFAULT 0,
    archived INTEGER DEFAULT 0,
    supplier_id TEXT,
    folder TEXT DEFAULT 'INBOX',
    raw_email TEXT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Email zincirleri tablosu
CREATE TABLE email_threads (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    thread_id TEXT NOT NULL,
    parent_message_id TEXT,
    child_message_id TEXT,
    level INTEGER DEFAULT 0,
    FOREIGN KEY (parent_message_id) REFERENCES emails(message_id),
    FOREIGN KEY (child_message_id) REFERENCES emails(message_id)
);

-- Ekler tablosu
CREATE TABLE attachments (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    email_id INTEGER NOT NULL,
    filename TEXT NOT NULL,
    content_type TEXT,
    size INTEGER,
    path TEXT,
    downloaded INTEGER DEFAULT 0,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (email_id) REFERENCES emails(id)
);

-- Email kategorileri
CREATE TABLE email_categories (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    email_id INTEGER NOT NULL,
    category TEXT NOT NULL,
    confidence REAL DEFAULT 0.0,
    FOREIGN KEY (email_id) REFERENCES emails(id)
);

-- Indexler
CREATE INDEX idx_emails_date ON emails(date DESC);
CREATE INDEX idx_emails_from ON emails(from_addr);
CREATE INDEX idx_emails_read ON emails(read);
CREATE INDEX idx_emails_supplier ON emails(supplier_id);
CREATE INDEX idx_threads_parent ON email_threads(parent_message_id);
CREATE INDEX idx_threads_child ON email_threads(child_message_id);
```

---

## 📋 Ana Fonksiyonlar

### 1. Email Okuma (IMAP)

```python
def connect_to_imap():
    """Gmail IMAP'a bağlan"""
    try:
        imap = imaplib.IMAP4_SSL('imap.gmail.com')
        imap.login(GMAIL_USER, GMAIL_PASS)
        return imap
    except Exception as e:
        print(f"IMAP bağlantı hatası: {e}")
        return None

def fetch_emails(imap, folder='INBOX', limit=50):
    """Emailleri çek"""
    try:
        imap.select(folder)
        
        # Son 50 emaili getir
        status, messages = imap.search(None, 'ALL')
        email_ids = messages[0].split()
        email_ids = email_ids[-limit:]  # Son 50
        
        emails = []
        for email_id in email_ids:
            status, msg_data = imap.fetch(email_id, '(RFC822)')
            email_body = msg_data[0][1]
            email_message = email.message_from_bytes(email_body)
            
            # Email'i parse et
            parsed_email = parse_email(email_message)
            emails.append(parsed_email)
            
            # Veritabanına kaydet
            save_email_to_db(parsed_email)
        
        return emails
    except Exception as e:
        print(f"Email çekme hatası: {e}")
        return []

def parse_email(email_message):
    """Email'i parse et"""
    email_data = {
        'message_id': email_message.get('Message-ID', ''),
        'from': email_message.get('From', ''),
        'to': email_message.get('To', ''),
        'subject': email_message.get('Subject', ''),
        'date': email_message.get('Date', ''),
        'body': '',
        'html_body': '',
        'attachments': []
    }
    
    # Body'yi çıkar
    if email_message.is_multipart():
        for part in email_message.walk():
            content_type = part.get_content_type()
            
            if content_type == 'text/plain':
                email_data['body'] = part.get_payload(decode=True).decode()
            elif content_type == 'text/html':
                email_data['html_body'] = part.get_payload(decode=True).decode()
            elif part.get_filename():
                # Ek var
                attachment = {
                    'filename': part.get_filename(),
                    'content_type': content_type,
                    'size': len(part.get_payload(decode=True))
                }
                email_data['attachments'].append(attachment)
    else:
        email_data['body'] = email_message.get_payload(decode=True).decode()
    
    return email_data
```

### 2. Email Gönderme (Reply)

```python
def send_reply(original_email_id, reply_body, attachments=None):
    """Email'e cevap gönder"""
    try:
        # Orijinal emaili getir
        original = get_email_from_db(original_email_id)
        
        # Reply oluştur
        msg = MIMEMultipart()
        msg['From'] = GMAIL_USER
        msg['To'] = original['from']
        msg['Subject'] = f"Re: {original['subject']}"
        msg['In-Reply-To'] = original['message_id']
        msg['References'] = original['message_id']
        
        # Body ekle
        body = MIMEText(reply_body, 'plain', 'utf-8')
        msg.attach(body)
        
        # Ekleri ekle
        if attachments:
            for file_path in attachments:
                with open(file_path, 'rb') as f:
                    part = MIMEBase('application', 'octet-stream')
                    part.set_payload(f.read())
                    encoders.encode_base64(part)
                    part.add_header(
                        'Content-Disposition',
                        f'attachment; filename= {os.path.basename(file_path)}'
                    )
                    msg.attach(part)
        
        # Gönder
        with smtplib.SMTP_SSL('smtp.gmail.com', 465) as server:
            server.login(GMAIL_USER, GMAIL_PASS)
            server.send_message(msg)
        
        # Veritabanını güncelle
        mark_email_as_replied(original_email_id)
        save_sent_email(msg, original_email_id)
        
        return True
    except Exception as e:
        print(f"Cevap gönderme hatası: {e}")
        return False
```

### 3. Veritabanı İşlemleri

```python
def save_email_to_db(email_data):
    """Email'i veritabanına kaydet"""
    conn = sqlite3.connect('emails.db')
    cursor = conn.cursor()
    
    try:
        cursor.execute('''
            INSERT OR IGNORE INTO emails 
            (message_id, from_addr, to_addr, subject, body, html_body, date)
            VALUES (?, ?, ?, ?, ?, ?, ?)
        ''', (
            email_data['message_id'],
            email_data['from'],
            email_data['to'],
            email_data['subject'],
            email_data['body'],
            email_data['html_body'],
            email_data['date']
        ))
        
        email_id = cursor.lastrowid
        
        # Ekleri kaydet
        for attachment in email_data.get('attachments', []):
            cursor.execute('''
                INSERT INTO attachments (email_id, filename, content_type, size)
                VALUES (?, ?, ?, ?)
            ''', (email_id, attachment['filename'], attachment['content_type'], attachment['size']))
        
        conn.commit()
    except Exception as e:
        print(f"Veritabanı hatası: {e}")
        conn.rollback()
    finally:
        conn.close()

def get_emails_from_db(filters=None):
    """Veritabanından emailleri getir"""
    conn = sqlite3.connect('emails.db')
    cursor = conn.cursor()
    
    query = 'SELECT * FROM emails WHERE 1=1'
    params = []
    
    if filters:
        if filters.get('unread_only'):
            query += ' AND read = 0'
        if filters.get('supplier'):
            query += ' AND supplier_id = ?'
            params.append(filters['supplier'])
        if filters.get('search'):
            query += ' AND (subject LIKE ? OR body LIKE ?)'
            search_term = f"%{filters['search']}%"
            params.extend([search_term, search_term])
    
    query += ' ORDER BY date DESC LIMIT 100'
    
    cursor.execute(query, params)
    emails = cursor.fetchall()
    conn.close()
    
    return emails
```

---

## 🎨 UI Bileşenleri

### Email List (Sol Panel)

```python
def create_email_list():
    """Email listesi oluştur"""
    # Treeview oluştur
    columns = ('from', 'subject', 'date', 'status')
    email_tree = ttk.Treeview(
        email_list_frame,
        columns=columns,
        show='tree headings',
        selectmode='browse'
    )
    
    # Başlıklar
    email_tree.heading('from', text='Kimden')
    email_tree.heading('subject', text='Konu')
    email_tree.heading('date', text='Tarih')
    email_tree.heading('status', text='Durum')
    
    # Kolonlar
    email_tree.column('from', width=150)
    email_tree.column('subject', width=250)
    email_tree.column('date', width=120)
    email_tree.column('status', width=80)
    
    # Renk kodlama
    email_tree.tag_configure('unread', font=('Segoe UI', 10, 'bold'))
    email_tree.tag_configure('read', font=('Segoe UI', 10))
    email_tree.tag_configure('replied', foreground='#27ae60')
    
    return email_tree

def populate_email_list(email_tree, emails):
    """Email listesini doldur"""
    email_tree.delete(*email_tree.get_children())
    
    for email in emails:
        status_icon = '📩' if email['read'] == 0 else '✅'
        tag = 'unread' if email['read'] == 0 else 'read'
        if email['replied']:
            tag = 'replied'
        
        email_tree.insert(
            '',
            'end',
            text=status_icon,
            values=(
                email['from'],
                email['subject'],
                format_date(email['date']),
                'Okunmadı' if email['read'] == 0 else 'Okundu'
            ),
            tags=(tag,)
        )
```

### Email Viewer (Sağ Panel)

```python
def create_email_viewer():
    """Email görüntüleyici oluştur"""
    # Header frame
    header_frame = ctk.CTkFrame(viewer_panel)
    header_frame.pack(fill=tk.X, padx=10, pady=5)
    
    # From
    from_label = ctk.CTkLabel(header_frame, text="Kimden:", font=("Segoe UI", 12, "bold"))
    from_label.grid(row=0, column=0, sticky=tk.W, padx=5)
    from_value = ctk.CTkLabel(header_frame, text="", font=("Segoe UI", 12))
    from_value.grid(row=0, column=1, sticky=tk.W, padx=5)
    
    # Subject
    subject_label = ctk.CTkLabel(header_frame, text="Konu:", font=("Segoe UI", 12, "bold"))
    subject_label.grid(row=1, column=0, sticky=tk.W, padx=5)
    subject_value = ctk.CTkLabel(header_frame, text="", font=("Segoe UI", 12))
    subject_value.grid(row=1, column=1, sticky=tk.W, padx=5)
    
    # Date
    date_label = ctk.CTkLabel(header_frame, text="Tarih:", font=("Segoe UI", 12, "bold"))
    date_label.grid(row=2, column=0, sticky=tk.W, padx=5)
    date_value = ctk.CTkLabel(header_frame, text="", font=("Segoe UI", 12))
    date_value.grid(row=2, column=1, sticky=tk.W, padx=5)
    
    # Body frame
    body_frame = ctk.CTkFrame(viewer_panel)
    body_frame.pack(fill=tk.BOTH, expand=True, padx=10, pady=5)
    
    body_text = tk.Text(
        body_frame,
        wrap=tk.WORD,
        font=("Segoe UI", 11),
        height=20
    )
    body_text.pack(fill=tk.BOTH, expand=True)
    
    # Action buttons
    action_frame = ctk.CTkFrame(viewer_panel)
    action_frame.pack(fill=tk.X, padx=10, pady=5)
    
    reply_btn = ctk.CTkButton(
        action_frame,
        text="💬 Cevapla",
        command=open_reply_dialog,
        fg_color="#3498db"
    )
    reply_btn.pack(side=tk.LEFT, padx=5)
    
    forward_btn = ctk.CTkButton(
        action_frame,
        text="➡️ İlet",
        command=forward_email,
        fg_color="#95a5a6"
    )
    forward_btn.pack(side=tk.LEFT, padx=5)
    
    delete_btn = ctk.CTkButton(
        action_frame,
        text="🗑️ Sil",
        command=delete_email,
        fg_color="#e74c3c"
    )
    delete_btn.pack(side=tk.LEFT, padx=5)
```

### Reply Dialog

```python
def open_reply_dialog(original_email):
    """Cevap penceresi aç"""
    dialog = tk.Toplevel()
    dialog.title("Email Cevapla")
    dialog.geometry("800x600")
    
    # To field
    to_frame = ctk.CTkFrame(dialog)
    to_frame.pack(fill=tk.X, padx=10, pady=5)
    
    ctk.CTkLabel(to_frame, text="Kime:", width=80).pack(side=tk.LEFT)
    to_entry = ctk.CTkEntry(to_frame, width=600)
    to_entry.insert(0, original_email['from'])
    to_entry.pack(side=tk.LEFT, padx=5)
    
    # Subject field
    subject_frame = ctk.CTkFrame(dialog)
    subject_frame.pack(fill=tk.X, padx=10, pady=5)
    
    ctk.CTkLabel(subject_frame, text="Konu:", width=80).pack(side=tk.LEFT)
    subject_entry = ctk.CTkEntry(subject_frame, width=600)
    subject_entry.insert(0, f"Re: {original_email['subject']}")
    subject_entry.pack(side=tk.LEFT, padx=5)
    
    # Body text
    body_frame = ctk.CTkFrame(dialog)
    body_frame.pack(fill=tk.BOTH, expand=True, padx=10, pady=5)
    
    body_text = tk.Text(body_frame, wrap=tk.WORD, font=("Segoe UI", 11))
    body_text.pack(fill=tk.BOTH, expand=True)
    
    # Quote original
    quote_var = tk.BooleanVar(value=True)
    quote_check = ctk.CTkCheckBox(
        dialog,
        text="Orijinal mesajı alıntıla",
        variable=quote_var
    )
    quote_check.pack(padx=10, pady=5)
    
    # Buttons
    button_frame = ctk.CTkFrame(dialog)
    button_frame.pack(fill=tk.X, padx=10, pady=10)
    
    send_btn = ctk.CTkButton(
        button_frame,
        text="📧 Gönder",
        command=lambda: send_reply_email(dialog, to_entry.get(), subject_entry.get(), body_text.get("1.0", "end-1c")),
        fg_color="#27ae60"
    )
    send_btn.pack(side=tk.LEFT, padx=5)
    
    cancel_btn = ctk.CTkButton(
        button_frame,
        text="❌ İptal",
        command=dialog.destroy,
        fg_color="#95a5a6"
    )
    cancel_btn.pack(side=tk.LEFT, padx=5)
```

---

## 📊 Akıllı Özellikler

### 1. Tedarikçi Tespiti

```python
def detect_supplier_from_email(email_address):
    """Email adresinden tedarikçiyi tespit et"""
    # Veritabanından tedarikçileri getir
    suppliers = get_all_suppliers()
    
    for supplier in suppliers:
        if supplier['email'] and supplier['email'].lower() in email_address.lower():
            return supplier['id']
    
    # Domain eşleşmesi
    domain = email_address.split('@')[-1]
    for supplier in suppliers:
        if supplier['email'] and domain in supplier['email']:
            return supplier['id']
    
    return None
```

### 2. Email Kategorilendirme (AI)

```python
def categorize_email_with_ai(email_subject, email_body):
    """Email'i AI ile kategorize et"""
    prompt = f"""
    Aşağıdaki email'i kategorize et. Kategoriler:
    - Sipariş
    - Teslimat
    - Kalite Sorunu
    - Fiyat Teklifi
    - Genel Soru
    - Şikayet
    - Teşekkür
    
    Konu: {email_subject}
    İçerik: {email_body[:500]}
    
    Sadece kategori adını döndür.
    """
    
    try:
        model = genai.GenerativeModel('gemini-2.0-flash-exp')
        response = model.generate_content(prompt)
        category = response.text.strip()
        return category
    except:
        return "Genel"
```

### 3. Otomatik Öncelik Tespiti

```python
def detect_priority(email_subject, email_body):
    """Email önceliğini tespit et"""
    urgent_keywords = ['acil', 'urgent', 'önemli', 'hemen', 'immediately', 'asap']
    
    subject_lower = email_subject.lower()
    body_lower = email_body.lower()
    
    for keyword in urgent_keywords:
        if keyword in subject_lower or keyword in body_lower:
            return 'Yüksek'
    
    return 'Normal'
```

---

## 🔔 Bildirimler

```python
def check_new_emails():
    """Yeni emailleri kontrol et"""
    imap = connect_to_imap()
    if not imap:
        return
    
    new_emails = fetch_emails(imap, limit=10)
    
    if new_emails:
        # Badge güncelle
        update_email_badge(len(new_emails))
        
        # Desktop notification
        for email in new_emails:
            show_notification(
                f"Yeni Email: {email['from']}",
                email['subject']
            )
    
    # 5 dakikada bir otomatik kontrol
    root.after(300000, check_new_emails)  # 300000 ms = 5 dakika
```

---

## 📈 Faydalar

### Kullanıcılar İçin
- ✅ Tüm email iletişimi tek yerden
- ✅ Uygulama değiştirmeye gerek yok
- ✅ Daha hızlı cevap süreleri
- ✅ Daha iyi email organizasyonu
- ✅ Tedarikçi bağlamı her zaman görünür

### İşletme İçin
- ✅ Merkezi iletişim
- ✅ Daha iyi takip ve denetim
- ✅ Gelişmiş cevap süreleri
- ✅ Veriye dayalı içgörüler
- ✅ Azaltılmış email kaosu

### Uygulama İçin
- ✅ Tam iletişim platformu
- ✅ Profesyonel kurumsal özellik
- ✅ Rekabet avantajı
- ✅ Kullanıcı etkileşimi
- ✅ Hepsi bir arada çözüm

---

## ⏱️ Uygulama Takvimi

### Hafta 1: Temel Email Okuma
- Gün 1-2: IMAP entegrasyonu
- Gün 3-4: Email parsing ve depolama
- Gün 5: Test

### Hafta 2: UI Geliştirme
- Gün 1-2: Inbox tab ve email listesi
- Gün 3-4: Email görüntüleyici panel
- Gün 5: Filtreler ve arama

### Hafta 3: Cevaplama & Zincirler
- Gün 1-2: Cevaplama fonksiyonu
- Gün 3-4: Zincir görselleştirme
- Gün 5: Test ve iyileştirme

### Hafta 4: Cilalandırma & Entegrasyon
- Gün 1-2: Tedarikçi bağlama
- Gün 3-4: Akıllı özellikler
- Gün 5: Final test

**Toplam: Tam sistem için 4 hafta**

---

## 🔒 Güvenlik

**Email Kimlik Bilgileri:**
- Config dosyasında şifrelenmiş saklama
- Gmail için OAuth2 kullan (önerilen)
- Uygulama özel şifreler desteği
- Güvenli IMAP/SMTP bağlantısı

**Veri Gizliliği:**
- Lokal email depolama (şifrelenmiş)
- Yapılandırılabilir saklama süresi
- Kalıcı silme seçeneği
- Yedekleme fonksiyonu

---

## ✅ Uygulama Seçenekleri

### Seçenek A: Tam Uygulama (Önerilen)
- Tam email yönetim sistemi
- Tüm özellikler dahil
- 4 hafta zaman çizelgesi
- Maksimum değer

### Seçenek B: MVP Yaklaşımı
- Sadece temel inbox + cevaplama
- 2 hafta zaman çizelgesi
- Hızlı teslimat
- Özellikler sonra eklenebilir

### Seçenek C: Aşamalı Kullanıma Sunma
- Hafta 1: Sadece inbox görünümü
- Hafta 2: Cevaplama ekle
- Hafta 3: Zincirler ekle
- Hafta 4: Akıllı özellikler ekle

---

## 🎉 Özet

**Sorunuza cevap:** EVET, kesinlikle mümkün!

**Ne alacaksınız:**
- 📥 Program içinde tam email gelen kutusu
- 💬 Email istemcisini açmadan emaillere cevap
- 🔄 Tam email trafik yönetimi
- 🎯 Tedarikçiye bağlı konuşmalar
- 📊 Email istatistikleri ve takip

Bu, uygulamayı tam bir iletişim platformuna dönüştürecek! 🚀

**Onayınızla uygulamaya başlamaya hazırım!**
