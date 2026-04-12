## n8n-Merge-Node-05

#### Go--->Google Sheets--->Create file
![](https://imgur.com/lyjBPG8.png)
#### Open nodes panel--->search: Google Sheets---> click: On row added--->value set kore then close.
#### Google Sheets Trigger e + sign click koro--->search: Switch--->condition set koro.
![](https://imgur.com/igY3BHE.png)
#### Switch er Card er + sign click koro--->search: Gmail--->Click: Send a message--->value set koro
#### Switch er COD er + sign click koro--->search: Gmail--->Click: Send a message--->value set koro
#### Switch er Wallet er + sign click koro--->search: Gmail--->Click: Send a message--->value set koro
#### Execution workflow click koro
#### Open nodes panel--->search: Merge--->Number of inputs e 3 daw--->close koro--->Switch er shathe adjust koro.
#### Merge er + sign click koro--->search: Gmail--->Click: Send a message--->value set koro
#### Execution workflow click koro. Publish koro. done!.

n8n-এ Merge Node কী?
Merge node হলো n8n-এর একটি গুরুত্বপূর্ণ node যা একাধিক workflow branch থেকে আসা data একত্রিত করে।

কেন Merge দরকার?
n8n-এ অনেক সময় workflow দুটো বা তার বেশি ভাগে ভাগ হয়ে যায়। পরে সেই আলাদা আলাদা data একসাথে নিয়ে কাজ করতে হলে Merge ব্যবহার করতে হয়।
Branch A ──┐
           ├──→ Merge → পরবর্তী কাজ
Branch B ──┘

Merge-এর Mode গুলো
1. Append
দুটো list পাশাপাশি জুড়ে দেয়, কোনো মিলানো ছাড়াই।
A: [1, 2]  +  B: [3, 4]  →  [1, 2, 3, 4]
2. Combine / Merge by Fields
নির্দিষ্ট field (যেমন id বা email) দিয়ে দুটো data মিলিয়ে একসাথে করে।
A: [{id:1, name:"Rahim"}]
B: [{id:1, city:"Dhaka"}]
→  [{id:1, name:"Rahim", city:"Dhaka"}]
3. Choose Branch
দুটো branch-এর মধ্যে শুধু একটির data নেয় — বাকিটা বাদ।
4. Wait
দুটো branch-ই শেষ হওয়ার জন্য অপেক্ষা করে, তারপর এগোয়।

বাস্তব উদাহরণ
ধরুন আপনি একটি order processing workflow বানাচ্ছেন:
Google Sheet (customer info) ──┐
                                ├──→ Merge (by order_id) → Email পাঠাও
Shopify (order details)    ────┘
দুই জায়গা থেকে data এনে order_id দিয়ে মিলিয়ে একটি পূর্ণ তথ্য তৈরি করা হলো।
