<div align="center">

# ⚡ IEC 60870-5-101 Protocol Tester

### 🛰️ A complete master-station tester for commissioning substation gateways & RTUs

Connect over a serial link, watch the live process image, send commands, trace every packet
byte-by-byte, draw the single-line diagram, and hand the client a signed PDF/Word report —
all from a slick browser UI. 🖥️

![Overview dashboard](screenshots/overview.png)

</div>

---

## 📖 What is this?

**IEC 60870-5-101** is the serial telecontrol protocol that links a power-substation
gateway (or RTU) to the control centre. This tool acts as the **controlling station
(master)**: it polls the outstation, decodes every telegram, shows breaker/disconnector
states and measured values in real time, sends commands, and records a full diagnostic
trace an engineer can use to **prove the point-to-point signal list** and troubleshoot faults. 🔍

It runs on a normal Windows PC (Linux/macOS too). A small Python service provides the
protocol engine; the UI is a modern web page that opens automatically in your browser.
Everything stays on your machine — nothing is uploaded anywhere. 🔒

> 🧪 **No hardware? No problem.** A built-in **substation simulator** answers on the other
> end, so you can learn the tool and prepare a whole project before you ever go on site.

---

## ✨ Features

### 🔌 Connectivity
- 📟 Real **RS-232 / RS-485** serial link (any COM port / USB adapter)
- 🧪 Built-in **substation gateway simulator** — works with zero hardware
- ⚙️ Full IEC 101 profile control: link address, common address, COT/IOA lengths,
  balanced / unbalanced, baud / parity, poll interval…

### 🗂️ Project configuration (do it at your desk!)
- 🆕 Create a **new project** and address the whole signal list **before** going to the substation
- 🏷️ Define every **IOA**, its name, type and engineering unit
- 📏 For measurements, choose the mode you expect — **9 (normalized) / 11 (scaled) /
  13 (short float)** — and get a **⚠️ warning** if the gateway sends a different type
- 💾 **Save / open** a whole project (config + points + diagrams) as one `.iecproj` file

### 📊 Live monitoring
- 📈 **Overview dashboard** — glowing gauges for voltage, current, power & frequency,
  a switchgear status board, and a live power-trend chart
- 🧮 **Full point table** — states (🟢 ON / 🔴 OFF), measured values with mini trend
  sparklines, quality flags, cause of transmission and timestamps
- 🖊️ Click to **name any point** on the fly

### 🎮 Command & control
- 🔘 Single / 🔀 Double / 🎚️ Regulating-step / 🎯 Set-point commands
- ✅ **Direct-execute** or **Select-Before-Operate (SBO)**
- 📡 General & counter interrogation, clock sync, read, test

### 🧬 Packet tracer & logging
- 👁️ Every frame **TX / RX**, newest at the bottom, with raw hex
- 🧩 **Byte-level decoder** — each octet colour-coded (start / control / address / ASDU / checksum)
- 📝 Precise, timestamped **diagnostic log** (also written to a rotating log file)

### 🏗️ Single-line diagram (SLD) designer
- 🧰 Drag busbars, breakers, disconnectors, earth switches, transformers, CT/VT, generators, loads
- 🔗 **Bind symbols to live IOAs** — closed breakers turn green and energised wires animate ⚡
- 🔍 Zoom, pan, save & load diagrams

### 📄 Client-ready reports
- 📑 One-click **PDF + Word (.docx)** commissioning report
- 🧾 Header with engineer, project, **AOC / SCC**, substation details
- 📋 All addresses **grouped by type**, plus every switch with a **VALID / INVALID** verdict

### 🔐 Built-in licensing
- Tamper-proof **Ed25519 digitally-signed** licences
- Node-locking to a machine, expiry dates, and a free trial

---

## 🖼️ Screenshots

| Live Monitor | Station Overview |
|:---:|:---:|
| ![Monitor](screenshots/monitor.png) | ![Overview](screenshots/overview.png) |

| Project Configuration | Command & Control |
|:---:|:---:|
| ![Config](screenshots/config.png) | ![Command](screenshots/command.png) |

| Packet Tracer | SLD Designer |
|:---:|:---:|
| ![Tracer](screenshots/tracer.png) | ![SLD](screenshots/sld.png) |

| Commissioning Report | Activation |
|:---:|:---:|
| ![Report](screenshots/report.png) | ![License](screenshots/license.png) |

---

## 🚀 Quick start

### 🪟 Windows
1. 📥 Download / clone this repository and extract it.
2. 🖱️ Double-click **`run.bat`**.
3. ⏳ On the first run it builds a private Python environment and installs the
   dependencies (needs internet once).
4. 🌐 Your browser opens automatically at `http://127.0.0.1:8101`.

> 🐍 Requires **Python 3.9+** installed with “Add Python to PATH”. The app auto-selects a
> free port, so you won't hit the usual Windows port-reservation error.

### 🐧 Linux / macOS
```bash
chmod +x run.sh
./run.sh
```

---

## 🧭 Typical workflow

1. 🗂️ **Office** — create the project, enter the job info, address every point (pick 9/11/13 for analogues), save the `.iecproj`.
2. 🔌 **On site** — open the project, set the serial & link parameters, click **Connect & start**.
3. 🛰️ **Verify** — run a **General Interrogation**; confirm every point is received with the right type, value and quality.
4. 🎮 **Commission** — operate each controllable point (SBO where required) and confirm the return information.
5. 📄 **Report** — generate the PDF & Word report, get signatures, archive the project file and trace.

📚 A full **49-page user manual** is included for every detail.

---

## 🧱 Protocol coverage

- 🧩 **Framing:** FT1.2 — single, fixed & variable frames, checksum
- 🔗 **Link layer:** unbalanced & balanced, reset / status, class-1/2 polling, FCB/FCV, ACD/DFC
- 📥 **Monitor ASDUs:** M_SP, M_DP, M_ST, M_BO, M_ME (normalized / scaled / float, with & without time tags), M_IT counters, M_EI
- 📤 **Control ASDUs:** C_SC, C_DC, C_RC, C_SE, interrogation, counter interrogation, clock sync, read, test
- 🕒 **Time tags:** CP56Time2a, CP24Time2a

---

## 🛠️ Tech stack

🐍 Python · ⚡ FastAPI + Uvicorn · 🔌 pySerial · 🔐 cryptography (Ed25519) ·
📄 python-docx + ReportLab · 🎨 vanilla HTML / CSS / JS (no build step)

---

## 💳 License & Pricing

This is **commercial software**. A valid licence is required to run it.

> 💰 **Annual licence: $30 / year**
>
> 📩 To get a licence, message **[@mostarshed](https://t.me/mostarshed)** on **Telegram**.

You'll receive a licence key — paste it into the activation screen and you're ready to go. ✅
A free trial is included so you can try everything first. 🎁

---

## 🇮🇷 درباره‌ی نرم‌افزار (فارسی)

این نرم‌افزار یک **تستر پروتکل IEC 60870-5-101** برای **تست و راه‌اندازی گیت‌وی پست‌های برق** است. 🔌

با وصل‌کردن کابل سریال، وضعیت کلیدها (بریکر، سکسیونر) و مقادیر اندازه‌گیری (ولتاژ، جریان، توان، فرکانس)
را به‌صورت زنده می‌بینید، فرمان ارسال می‌کنید، همه‌ی پکت‌ها را بایت‌به‌بایت تریس می‌کنید، تک‌خطیِ پست را
می‌کشید، و در پایان یک گزارش رسمی **PDF و Word** برای کارفرما می‌سازید. 📄

✨ **قابلیت‌های کلیدی:**
- 🧪 شبیه‌ساز داخلی — بدون نیاز به سخت‌افزار تست کنید
- 🗂️ ساخت پروژه و **آدرس‌دهی قبل از رفتن به پست** (با انتخاب مد اندازه‌گیر: ۹ / ۱۱ / ۱۳)
- 📊 داشبورد زنده با گیج و نمودار، جدول کامل نقاط، و نشانه‌گذاری نقاطِ نامعتبر
- 🎮 ارسال انواع فرمان به‌صورت مستقیم یا Select-Before-Operate
- 🧬 تریسر پکت با دیکد بایت‌به‌بایت و لاگ دقیق برای عیب‌یابی
- 🏗️ طراحی تک‌خطی پست و اتصال زنده‌ی المان‌ها به IOA
- 📄 گزارش کامل با هدر (مهندس، پروژه، AOC، SCC، مشخصات پست)

🚀 **اجرا:** روی ویندوز فقط کافیست `run.bat` را اجرا کنید؛ خودش نصب و اجرا می‌شود و مرورگر را باز می‌کند.

💳 **تهیه‌ی لایسنس:** هزینه‌ی لایسنس **سالانه ۳۰ دلار** است.
برای تهیه، در تلگرام به آیدی **[@mostarshed](https://t.me/mostarshed)** پیام بدهید. 📩

---

<div align="center">

Made with ⚡ for substation commissioning engineers

📩 License & support: **[@mostarshed](https://t.me/mostarshed)** on Telegram · 💰 $30/year

</div>
