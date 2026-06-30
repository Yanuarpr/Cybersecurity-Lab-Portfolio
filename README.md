# Snort-IDS-Network-Lab
"Automated Network IDS lab environment built with Snort on Linux Server to detect Nmap scanning, SSH brute force, and web directory scanning attacks."

# 🛡️ Automated Network IDS Lab with Snort

Select Language:  
👉 **[English Version](#-english-version)** | 👉 **[Versi Bahasa Indonesia](#-versi-bahasa-indonesia)**

---

## 🇺🇸 English Version

### 📝 Project Overview
This project demonstrates the deployment and configuration of an **Intrusion Detection System (IDS)** using **Snort** on an isolated Linux Server environment. This lab is designed to monitor, detect, and analyze various network and web application attacks in real-time from the perspective of a *Blue Team / Junior SOC Analyst*.

### 🌐 Network Topology & Environment
The lab is built inside Oracle VirtualBox using an **Internal Network** adapter to ensure total isolation from the production network.
* **IDS / Target Server:** Linux Server (Running Snort IDS & Apache Web Server)
* **Attacker Machine:** Kali Linux / Parrot OS

### 🛠️ Custom Rules Implementation
In addition to community rules, this project focuses on implementing custom signatures (`local.rules`) to detect specific attack behaviors:

1. **Reconnaissance Detection (Nmap Port Scanning)**
   * **Rule:** `alert tcp any any -> any any (msg:"PERINGATAN: Deteksi Nmap Syn Scan"; flags:S; sid:1000002; rev:1;)`
2. **SSH Brute Force Detection (Rate-Limiting Filter)**
   * **Rule:** `alert tcp any any -> any 22 (msg:"PERINGATAN: Potensi Brute Force SSH Dideteksi"; flags:S; detection_filter:track by_src, count 5, seconds 10; sid:1000004; rev:1;)`
3. **Web Directory Scanning (Content Inspection)**
   * **Rule:** `alert tcp any any -> any 80 (msg:"PERINGATAN: Pemindaian Direktori Web Dideteksi"; content:"dirb"; nocase; http_header; sid:1000005; rev:2;)`

### 🚀 Proof of Concept & Incident Analysis
When the attacker machine executes `dirb http://<Target_IP>`, the Snort console on the Linux Server immediately triggers real-time alerts.

<img width="1144" height="520" alt="DIRB" src="https://github.com/user-attachments/assets/242365de-97eb-47bb-bea7-45ca0244f357" />


**Log Analysis:** The system successfully flagged the reconnaissance activity because it matched specific string contents within the HTTP Header during high-frequency requests. This gives security analysts full visibility to perform further mitigation (e.g., IP blocking).

---

## 🇮🇩 Versi Bahasa Indonesia

### 📝 Ringkasan Proyek
Proyek ini mendemonstrasikan pembangunan dan konfigurasi **Intrusion Detection System (IDS)** menggunakan **Snort** pada lingkungan Linux Server terisolasi. Lab ini dirancang untuk memantau, mendeteksi, dan menganalisis berbagai aktivitas serangan jaringan dan aplikasi web secara *real-time* dari sudut pandang seorang *Blue Team / Junior SOC Analyst*.

### 🌐 Topologi Jaringan & Lingkungan Lab
Lab ini dibangun di atas Oracle VirtualBox dengan konfigurasi jaringan menggunakan **Internal Network** untuk memastikan isolasi total dari jaringan produksi.
* **IDS / Target Server:** Linux Server (Konfigurasi: Snort IDS & Apache Web Server)
* **Mesin Penyerang:** Kali Linux / Parrot OS

### 🛠️ Implementasi Aturan Kustom (Custom Rules)
Selain menggunakan aturan bawaan, proyek ini berfokus pada implementasi aturan kustom (`local.rules`) untuk mendeteksi perilaku serangan spesifik:

1. **Deteksi Reconnaissance (Nmap Port Scanning)**
   * **Aturan:** `alert tcp any any -> any any (msg:"PERINGATAN: Deteksi Nmap Syn Scan"; flags:S; sid:1000002; rev:1;)`
2. **Deteksi Brute Force SSH (Penyaringan Berbasis Waktu)**
   * **Aturan:** `alert tcp any any -> any 22 (msg:"PERINGATAN: Potensi Brute Force SSH Dideteksi"; flags:S; detection_filter:track by_src, count 5, seconds 10; sid:1000004; rev:1;)`
3. **Deteksi Web Directory Scanning (Inspeksi Konten)**
   * **Aturan:** `alert tcp any any -> any 80 (msg:"PERINGATAN: Pemindaian Direktori Web Dideteksi"; content:"dirb"; nocase; http_header; sid:1000005; rev:2;)`

### 🚀 Bukti Pengujian & Analisis Insiden
Ketika mesin penyerang menjalankan perintah `dirb http://<IP_Server>`, konsol Snort di Linux Server langsung memicu *alert* secara *real-time*.

<img width="1144" height="520" alt="dirb2" src="https://github.com/user-attachments/assets/b8da17f5-7b6c-45ae-8f0f-4b2eb08f9019" />


**Analisis Log:** Sistem berhasil mengidentifikasi aktivitas pemindaian karena adanya kecocokan konten spesifik pada *HTTP Header* selama permintaan berfrekuensi tinggi ke server web. Ini memberikan visibilitas penuh kepada analis keamanan untuk melakukan tindakan mitigasi lebih lanjut.

---

## 📈 Key Takeaways / Kemampuan yang Dipelajari
* Understanding virtual network architecture and isolation.
* Configuring and optimizing Snort IDS in Console Alert mode.
* Analyzing network packets (TCP/IP) and writing signature-based detection rules.
* Basic log analysis on Apache Web Server.
