<img width="1536" height="1024" alt="3c032fda-977c-4f8d-a3ae-33c1abc6e316" src="https://github.com/user-attachments/assets/376b6c3a-8eee-4d96-a60b-b2a87e99deee" />

# 🚀 Smart Git Commit Guide (Super Easy & User Friendly)

> **Goal:** এমন একটা Git commit system বানানো, যেটা **যে কেউ প্রথম দেখলেই বুঝতে পারে** — beginner হোক বা experienced developer।
>
> এই document টা intentionally **simple language**, **Bangla + English mixed**, এবং **real-life গল্পের মতো** করে লেখা।

---

<a id="top"></a>

## 📌 Table of Contents

1. [Why this guide exists (ছোট গল্প)](#why)
2. [`cmt` আসলে কী?](#cmt-meaning)
3. [GitHub-এ commit দেখতে কেমন হবে](#github-look)
4. [One-time setup (Choose your style)](#setup)
5. [Daily usage (Using `cmt`)](#daily-use)
6. [Daily usage (Using `cmtf` - Fancy)](#daily-use-cmtf)
7. [Commit ঠিক আছে কিনা চেক করা (Verification)](#check)
8. [Date + Time vs Only Date (সহজভাবে)](#date-vs-time)
9. [ভুল হলে কী হবে?](#mistake)
10. [FAQ (সবচেয়ে common প্রশ্ন)](#faq)
11. [শেষ কথা](#end)

---

## 🌱 <a id="why"></a>Why this guide exists (বাস্তব জীবনের গল্প)

ধরেন, আপনি একটা প্রোজেক্টে মনের সুখে কোড করতেছেন। কোনো প্যারা নাই।
হুট করে মনে হলো—commit দিয়ে রাখি। মেসেজ দিলেন:

```
update
```

তখন তো সব ঠিকই ছিল। কাজ শেষ, ল্যাপটপ বন্ধ, ঘুম। 😴

কিন্তু ২ মাস পর... 📅
হঠাৎ ওই কোডে কোনো একটা ঝামেলা হলো। আপনি `git log` চেক করতে গেলেন।
গিয়ে দেখেন—
* `update`
* `fix bug`
* `again fix`
* `last update`

মাথাটা তখন গরম হবে না? 🤯
নিজের কোড দেখে নিজেই কনফিউজড হয়ে যাবেন— *“কিরে ভাই! এইটা কবেকার আপডেট? আর এই ফিক্সটাই বা কিসের?”*

এই ঝামেলা থেকে বাঁচতেই এই গাইড। যাতে ৬ মাস পরেও গিট লগ দেখে মনে হয়—
*“আরে! এইতো ১৬ তারিখে পেমেন্ট গেটওয়ে ফিক্স করছিলাম, বিকেল ৫টায়। সব ক্লিয়ার!”*

শান্তি! 😌

⬆️ [Scroll to top](#top)

---

## 🧠 <a id="cmt-meaning"></a>`cmt` বা `cmtf` আসলে কী?

### 1. `cmt` = Commit with Time (Numeric)
Result: `2026-01-16`

### 2. `cmtf` = Commit with Time Format (Fancy)
Result: `16 January 2026`

মনে রাখার trick:
* **t** → time
* **f** → flower/fancy (সুন্দর করে দেখা)

মানে:
> যেকোনো একটা command দিলেই commit হবে + date/time auto add হবে।

এটা Git-এর default command না।
এটা আমরা নিজেরা বানানো **helper shortcut**।

⬆️ [Scroll to top](#top)

---

## 🖼️ <a id="github-look"></a>GitHub-এ commit দেখতে কেমন হবে?

### Normal case (Date + Time)

```
fix login bug || 2026-01-15 03:01 PM
```

### Simple case (Only Date)

```
cleanup code || 2026-01-15
```

দেখলেই বোঝা যায়:

* কী change
* কবে change

⬆️ [Scroll to top](#top)

---

## ⚙️ <a id="setup"></a>One-time setup (Choose your style)
👉 **যেকোনো একটি Option বেছে নিন (যেটা আপনার ভালো লাগে)**

---

### Option 1: Standard Style (`cmt`)
Output example: `2026-01-16`

```bash
git config --global alias.cmt '!f() {
  if [ "$1" = "-d" ] || [ "$1" = "--date-only" ]; then
    git add -A && git commit -m "${2:-general update} || $(date "+%Y-%m-%d")" && git status
  else
    git add -A && git commit -m "${1:-general update} || $(date "+%Y-%m-%d %I:%M %p")" && git status
  fi
}; f'
```

---

### Option 2: Fancy Style (`cmtf`)
Output example: `16 January 2026`

```bash
git config --global alias.cmtf '!f() {
  if [ "$1" = "-d" ] || [ "$1" = "--date-only" ]; then
    git add -A && git commit -m "${2:-general update} || $(date "+%-d %B %Y")" && git status
  else
    git add -A && git commit -m "${1:-general update} || $(date "+%-d %B %Y %I:%M %p")" && git status
  fi
}; f'
```

---

🎉 Done! যেকোনো একটা copy-paste করে enter টিপলেই setup শেষ।

### 🧠 কোডটা আসলে কী করছে? (Behind the Scenes)

কৌতূহলী হলে জেনে রাখতে পারেন, এই `cmt` command টার ভেতরে আসলে ৩টা কাজ একসাথে হচ্ছে:

1. **`git add -A`**: আপনার সব change (new file, edit, delete) একসাথে ready (stage) করে। আলাদা করে `git add .` করা লাগে না।
2. **`git commit -m "..."`**: আপনার message এর সাথে **Automatic Date & Time** জোড়া লাগিয়ে commit করে দেয়।
3. **`git status`**: সবশেষে ক্লিন স্ট্যাটাস দেখিয়ে দেয়, যাতে আপনি নিশ্চিত হন সব ঠিক আছে।

⬆️ [Scroll to top](#top)

---

## ▶️ <a id="daily-use"></a>Daily ব্যবহার করার নিয়ম (Using `cmt`)
*যদি আপনি Option 1 setup করে থাকেন।*

### ✅ 1. Standard Commit (সবচেয়ে বেশি ব্যবহার হবে)

**Command:**
```bash
git cmt "fix payment bug"
```

**Output (Message):**
`fix payment bug || 2026-01-16 04:20 PM`

---

### ✅ 2. Date Only (Time দরকার নেই)

**Command:**
```bash
git cmt -d "cleanup code"
```

**Output (Message):**
`cleanup code || 2026-01-16`

---

### ✅ 3. Lazy Commit 😄 (Message দেয়ার সময় নেই)

**Command:**
```bash
git cmt
```

**Output (Message):**
`general update || 2026-01-16 04:25 PM`

⬆️ [Scroll to top](#top)

---

## ▶️ <a id="daily-use-cmtf"></a>Daily ব্যবহার করার নিয়ম (Using `cmtf`)
*যদি আপনি Option 2 (Fancy Style) setup করে থাকেন।*

### ✅ 1. Standard Commit

**Command:**
```bash
git cmtf "fix bugs"
```

**Output (Message):**
`fix bugs || 17 January 2026 04:20 PM`

---

### ✅ 2. Date Only

**Command:**
```bash
git cmtf -d "cleanup"
```

**Output (Message):**
`cleanup || 17 January 2026`

---

### ✅ 3. Lazy Commit

**Command:**
```bash
git cmtf
```

**Output (Message):**
`general update || 17 January 2026 04:25 PM`

⬆️ [Scroll to top](#top)

---

## 🔎 <a id="check"></a>Commit ঠিক আছে কিনা চেক করা (Verification)

Commit দেয়ার পর সেটা ঠিকঠাক হলো কিনা তা চেক করার জন্য এই command টি ব্যবহার করুন:

```bash
git log -1
```

এটা দিলে **last commit** এর details দেখাবে।

### Output দেখতে যেমন হবে:

```
commit 1a2b3c4d...
Author: Your Name <email@example.com>
Date:   Thu Jan 16 22:30:00 2026 +0600

    fix payment issue || 2026-01-16 10:30 PM
```

এখানে `|| 2026-01-16 10:30 PM` অংশটা দেখে নিশ্চিত হতে পারবেন যে time ঠিকঠাক add হয়েছে।

⬆️ [Scroll to top](#top)

---

## 🎯 <a id="date-vs-time"></a>Date + Time vs Only Date (সহজভাবে)

| Situation        | Use this    |
| ---------------- | ----------- |
| Important change | Date + Time |
| Small cleanup    | Only Date   |

Rule simple:

> **যত important change, তত detail**

⬆️ [Scroll to top](#top)

---

## 😬 <a id="mistake"></a>ভুল হলে কী হবে?

কিছুই না 😄

* Git commit undo করা যায়
* Message edit করা যায়
* এই system Git-এর default behavior change করে না

Safe & beginner-friendly ✔️

⬆️ [Scroll to top](#top)

---

## ❓ <a id="faq"></a>FAQ (Common questions)

### ❓ এটা GitHub-এ কাজ করবে?

✅ হ্যাঁ। Commit message যেভাবে পাঠাও সেভাবেই store হবে।

### ❓ VS Code snippet কেন না?

Snippet দিয়ে AM/PM পাওয়া যায় না। এইটা reliable solution।

### ❓ Remove করতে চাইলে?

```bash
git config --global --unset alias.cmt
```

⬆️ [Scroll to top](#top)

---

## 🏁 <a id="end"></a>শেষ কথা

এই guide বানানো হয়েছে যেন:

* কেউ ভয় না পায়
* কেউ confuse না হয়
* Public GitHub-এ confidently share করা যায়

> **Clean commit history = confident developer**

Happy coding & happy committing 🚀

⬆️ [Scroll to top](#top)
