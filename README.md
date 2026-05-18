# 🔗 n8n — Merge Node Guide

> n8n এ Merge Node ব্যবহার করে একাধিক Branch একত্রিত করার ধাপে ধাপে গাইড।

---

## 📊 Workflow Overview

```
Google Sheets Trigger
        │
        ▼
     [SWITCH]
        ├── Card   ──► Gmail: Send Message ──┐
        ├── COD    ──► Gmail: Send Message ──┼──► Merge ──► Gmail: Final Message
        └── Wallet ──► Gmail: Send Message ──┘
```

---

## 📋 Google Sheets প্রস্তুত করো

### ✅ ধাপ ১ — Google Sheets এ ফাইল তৈরি করো

Google Sheets ওপেন করো এবং প্রয়োজনীয় কলাম তৈরি করো।

![Create Google Sheet](https://imgur.com/lyjBPG8.png)

---

## ⚙️ Workflow সেটআপ

### ✅ ধাপ ২ — Google Sheets Trigger যোগ করো

- **Nodes Panel** ওপেন করো
- **"Google Sheets"** সার্চ করো
- **"On row added"** সিলেক্ট করো
- Value গুলো সেট করো এবং Close করো

---

### ✅ ধাপ ৩ — Switch Node যোগ করো এবং Condition সেট করো

- Google Sheets Trigger এর **`+`** বাটনে ক্লিক করো
- **"Switch"** সার্চ করো
- Payment Method অনুযায়ী Condition সেট করো *(Card / COD / Wallet)*

![Switch Node Condition](https://imgur.com/igY3BHE.png)

---

## ✉️ Switch Branch — Gmail Nodes

### ✅ ধাপ ৪ — Card Branch এ Gmail যোগ করো

- **Card** এর **`+`** বাটনে ক্লিক করো
- **"Gmail"** সার্চ করো → **"Send a message"** সিলেক্ট করো
- প্রয়োজনীয় Value সেট করো

---

### ✅ ধাপ ৫ — COD Branch এ Gmail যোগ করো

- **COD** এর **`+`** বাটনে ক্লিক করো
- **"Gmail"** সার্চ করো → **"Send a message"** সিলেক্ট করো
- প্রয়োজনীয় Value সেট করো

---

### ✅ ধাপ ৬ — Wallet Branch এ Gmail যোগ করো

- **Wallet** এর **`+`** বাটনে ক্লিক করো
- **"Gmail"** সার্চ করো → **"Send a message"** সিলেক্ট করো
- প্রয়োজনীয় Value সেট করো

---

### ✅ ধাপ ৭ — প্রথমবার Workflow Execute করো

**Execute Workflow** বাটনে ক্লিক করো এবং সব Branch ঠিকমতো কাজ করছে কিনা যাচাই করো।

---

## 🔗 Merge Node যোগ করো

### ✅ ধাপ ৮ — Merge Node সেটআপ করো

- **Nodes Panel** ওপেন করো
- **"Merge"** সার্চ করো
- **Number of inputs** এ **`3`** দাও
- Close করো
- Switch Node এর **তিনটি Branch** এর সাথে **Merge** সংযুক্ত করো

---

### ✅ ধাপ ৯ — Merge এর পর Gmail যোগ করো

- **Merge** এর **`+`** বাটনে ক্লিক করো
- **"Gmail"** সার্চ করো → **"Send a message"** সিলেক্ট করো
- Final Notification এর Value সেট করো

---

### ✅ ধাপ ১০ — Workflow Execute ও Publish করো

**Execute Workflow** ক্লিক করো → সব ঠিক থাকলে **Publish** করো।

> 🎉 Workflow সম্পন্ন! এখন যেকোনো Payment Method এ Order আসলে আলাদা Email যাবে, এবং সবশেষে Merge হয়ে একটি Final Notification পাঠানো হবে।

---

## 📚 Merge Node কী এবং কেন দরকার?

Merge Node হলো n8n এর একটি গুরুত্বপূর্ণ Node যা **একাধিক Branch থেকে আসা Data একত্রিত** করে।

n8n এ Workflow অনেক সময় দুই বা তার বেশি ভাগে ভাগ হয়ে যায়। পরে সেই আলাদা আলাদা Data একসাথে নিয়ে কাজ করতে Merge ব্যবহার করতে হয়।

```
Branch A ──┐
           ├──► Merge ──► পরবর্তী কাজ
Branch B ──┘
```

---

## 🛠️ Merge এর Mode সমূহ

### 1️⃣ Append
দুটো List পাশাপাশি জুড়ে দেয়, কোনো মিলানো ছাড়াই।

```
A: [1, 2]  +  B: [3, 4]  →  [1, 2, 3, 4]
```

---

### 2️⃣ Combine / Merge by Fields
নির্দিষ্ট Field *(যেমন `id` বা `email`)* দিয়ে দুটো Data মিলিয়ে একসাথে করে।

```
A: [{ id: 1, name: "Rahim" }]
B: [{ id: 1, city: "Dhaka" }]
→  [{ id: 1, name: "Rahim", city: "Dhaka" }]
```

---

### 3️⃣ Choose Branch
দুটো Branch এর মধ্যে **শুধু একটির Data** নেয় — বাকিটা বাদ দেয়।

---

### 4️⃣ Wait
দুটো Branch **শেষ হওয়ার জন্য অপেক্ষা** করে, তারপর এগোয়।

---

## 💡 বাস্তব উদাহরণ

ধরো একটি **Order Processing Workflow** বানাচ্ছো:

```
Google Sheets (Customer Info) ──┐
                                 ├──► Merge (by order_id) ──► Email পাঠাও
Shopify (Order Details)     ────┘
```

দুই জায়গা থেকে Data এনে `order_id` দিয়ে মিলিয়ে একটি পূর্ণ তথ্য তৈরি করা হলো।

---

## 📋 Quick Reference

| ধাপ | Node | কাজ |
|-----|------|-----|
| ১ | — | Google Sheets ফাইল তৈরি |
| ২ | Google Sheets | Row Added Trigger সেট |
| ৩ | Switch | Card / COD / Wallet Condition |
| ৪ | Gmail | Card Branch Email |
| ৫ | Gmail | COD Branch Email |
| ৬ | Gmail | Wallet Branch Email |
| ৭ | — | প্রথম Execution যাচাই |
| ৮ | Merge | ৩টি Branch একত্রিত করো |
| ৯ | Gmail | Final Notification Email |
| ১০ | — | Execute ও Publish |

| Merge Mode | কী করে |
|------------|--------|
| **Append** | List জুড়ে দেয় |
| **Combine** | Field দিয়ে Data মেলায় |
| **Choose Branch** | একটি Branch বেছে নেয় |
| **Wait** | সব Branch শেষের অপেক্ষা করে |

---

*Merge Node ব্যবহার করলে জটিল Multi-Branch Workflow কে সহজে একটি জায়গায় নিয়ে আসা যায়।*
