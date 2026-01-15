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
4. [One-time setup (খুব সহজ)](#setup)
5. [Daily ব্যবহার করার নিয়ম](#daily-use)
6. [Date + Time vs Only Date (সহজভাবে)](#date-vs-time)
7. [ভুল হলে কী হবে?](#mistake)
8. [FAQ (সবচেয়ে common প্রশ্ন)](#faq)
9. [শেষ কথা](#end)

---

## 🌱 <a id="why"></a>Why this guide exists (একটা ছোট গল্প)

ধরো আজ তুমি একটা feature বানালে। ৩ মাস পরে আবার সেই code touch করলে — তখন মনে থাকবে?

Commit message যদি এমন হয়:

```
update
```

তাহলে future-you বলবে: 😐 *“এইটা আমি কেন করছিলাম?”*

এই guide বানানো হয়েছে যেন:

* Commit message দেখেই বুঝা যায় **কখন** change হয়েছে
* History clean থাকে
* কাউকে explain করতে না হয়

⬆️ [Scroll to top](#top)

---

## 🧠 <a id="cmt-meaning"></a>`cmt` আসলে কী?

### `cmt` = **Commit with Time**

মনে রাখার খুব সহজ trick:

* **cm** → commit
* **t** → time

মানে:

> `git cmt` লিখলেই commit হবে + date/time auto add হবে

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

## ⚙️ <a id="setup"></a>One-time setup (খুব সহজ)

👉 **এই অংশটা শুধু একবারই করতে হবে**

### Step 1: Terminal খুলুন

* Mac → Terminal
* Windows → Git Bash
* Linux → Terminal

### Step 2: নিচের command টা copy–paste করুন

```bash
git config --global alias.cmt '!f() {
  if [ "$1" = "-d" ] || [ "$1" = "--date-only" ]; then
    git add -A && git commit -m "${2:-general update} || $(date "+%Y-%m-%d")" && git status
  else
    git add -A && git commit -m "${1:-general update} || $(date "+%Y-%m-%d %I:%M %p")" && git status
  fi
}; f'
```

🎉 Done! আর কিছু করতে হবে না।

⬆️ [Scroll to top](#top)

---

## ▶️ <a id="daily-use"></a>Daily ব্যবহার করার নিয়ম

### ✅ Most common (সবচেয়ে বেশি ব্যবহার হবে)

```bash
git cmt "fix payment issue"
```

👉 Date + Time automatically add হবে

---

### ✅ Sometimes (Time দরকার নেই)

```bash
git cmt -d "small refactor"
```

👉 Only date থাকবে

---

### ✅ Lazy day 😄 (message না দিলেও চলবে)

```bash
git cmt
```

👉 Default message + date/time

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
