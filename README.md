# 🔥 Cloudflare Web Application Firewall (WAF) and Security Setup

## 🌍 Overview
This repository provides a complete **step-by-step guide** to setting up and configuring **Cloudflare Web Application Firewall (WAF)**. It helps protect websites against **malicious attacks, bot traffic, and unauthorized access**. This guide includes the process of **creating custom rules**, **understanding firewall settings**, and **applying CAPTCHA verification** to enhance security and performance.

---

# 📌 **How to Create Cloudflare WAF Rules (Step-by-Step Guide)**

## 🚀 **Step 1: Accessing Cloudflare Security Settings**
1. **🔑 Login to Cloudflare**: Go to [Cloudflare Dashboard](https://dash.cloudflare.com/) and log in.
2. **🌐 Select Your Website**: Click on the website you want to protect.
3. **🛡️ Navigate to WAF**: In the left sidebar, go to **Security > WAF (Web Application Firewall)**.
4. **⚙️ Go to Custom Rules**: Click on the **Custom Rules** tab.

## 🏗️ **Step 2: Creating a New Custom Rule**
1. Click on **➕ Create Rule**.
2. Enter a **📝 Rule Name** (e.g., `CAPTCHA SKIP` for bots).
3. Choose a **📌 Field** (e.g., `User Agent` to detect bots).
4. Select an **⚙️ Operator** (e.g., `contains` to match specific bots).
5. Enter a **📥 Value** (e.g., `Googlebot` for Google Search bot).
6. Choose an **🔒 Action** (e.g., `Skip` for trusted bots, `Block` for countries, or `Managed Challenge` for CAPTCHA).
7. Set the **🔄 Placement Order** (first, after another rule, etc.).
8. Click **💾 Save** and ensure the rule is **✅ Enabled**.

---
# 🎯 **Custom Rules Configuration (Basic to Advanced)**

Below are **three essential WAF rules**, explained in three formats: **Table Format, Copyable Code Format, and Detailed Explanation**.

---

## **1️⃣ CAPTCHA SKIP Rule (Allowing Search Engine Bots) 🤖**

### ✅ **📋 Table Format**
| **📌 Field**     | **⚙️ Operator** | **📥 Value**              |
|--------------|------------|----------------------|
| User Agent   | contains   | facebookexternalhit  |
| OR           | contains   | TwitterBot           |
| OR           | contains   | LinkedInBot          |
| OR           | contains   | Googlebot            |
| OR           | contains   | Bingbot              |
| **🔒 Action**   | **Skip**   |                      |
| **🔄 Placement**| **First**  |                      |

### ✅ **📜 Copyable Code Format**
```
Rule Name: CAPTCHA SKIP
Field: User Agent
Operator: contains
Value: facebookexternalhit

OR

Field: User Agent
Operator: contains
Value: TwitterBot

OR

Field: User Agent
Operator: contains
Value: LinkedInBot

OR

Field: User Agent
Operator: contains
Value: Googlebot

OR

Field: User Agent
Operator: contains
Value: Bingbot

Action: Skip
Placement: First
```

### ✅ **📖 Detailed Explanation**
- **🎯 Purpose**: This rule allows legitimate search engine bots to access your website **without being blocked** by CAPTCHA.
- **📌 Field**: `User Agent` checks if the visitor is a bot.
- **⚙️ Operator**: `contains` applies if the bot’s name appears.
- **📥 Values**: Recognized search bots like `Googlebot`, `Bingbot`, etc.
- **🔒 Action**: `Skip` allows these bots to bypass security checks.
- **🔄 Placement**: This rule should be **first** in order.

---

## **2️⃣ COUNTRY BLOCK Rule (Blocking Specific Countries) 🌍**

### ✅ **📋 Table Format**
| **📌 Field**  | **⚙️ Operator** | **📥 Value**           |
|-----------|------------|-------------------|
| Country   | equals     | United Kingdom    |
| OR        | equals     | United States     |
| **🔒 Action**| **Block**  |                   |
| **🔄 Placement**| **After CAPTCHA SKIP** | |

### ✅ **📜 Copyable Code Format**
```
Rule Name: COUNTRY BLOCK
Field: Country
Operator: equals
Value: United Kingdom

OR

Field: Country
Operator: equals
Value: United States

Action: Block
Placement: After CAPTCHA SKIP
```

### ✅ **📖 Detailed Explanation**
- **🎯 Purpose**: Blocks traffic from selected countries to **prevent fraud or unwanted access**.
- **📌 Field**: `Country` checks the visitor’s location.
- **⚙️ Operator**: `equals` applies only to the listed countries.
- **📥 Values**: `United Kingdom`, `United States` (can add more if needed).
- **🔒 Action**: `Block` denies access to these users.
- **🔄 Placement**: Should be **after the CAPTCHA SKIP rule**.

---

## **3️⃣ CAPTCHA ON Rule (Adding Verification for Suspicious Traffic) 🔐**

### ✅ **📋 Table Format**
| **📌 Field**  | **⚙️ Operator** | **📥 Value**           |
|-----------|------------|-------------------|
| Hostname  | wildcard   | mail.kamrul.us    |
| OR        | wildcard   | kamrul.us/SOFT    |
| OR        | wildcard   | kamrul.us        |
| **🔒 Action**| **Managed Challenge** |      |
| **🔄 Placement**| **After COUNTRY BLOCK** | |

### ✅ **📜 Copyable Code Format**
```
Rule Name: CAPTCHA ON
Field: Hostname
Operator: wildcard
Value: mail.kamrul.us

OR

Field: Hostname
Operator: wildcard
Value: kamrul.us/SOFT

OR

Field: Hostname
Operator: wildcard
Value: kamrul.us

Action: Managed Challenge
Placement: After COUNTRY BLOCK
```

### ✅ **📖 Detailed Explanation**
- **🎯 Purpose**: Protects sensitive pages by forcing visitors to pass a CAPTCHA challenge.
- **📌 Field**: `Hostname` applies the rule to specific site sections.
- **⚙️ Operator**: `wildcard` matches similar URLs.
- **🔒 Action**: `Managed Challenge` presents CAPTCHA verification.
- **🔄 Placement**: Runs **after COUNTRY BLOCK rule**.

---

## 🔍 **Final Verification & Troubleshooting**
### ✅ **How to Check if Rules Are Working?**
1. **🛠️ Test the site from different locations** (use VPN for testing country blocks).
2. **🔍 Use browser developer tools** (F12 > Network > Inspect HTTP headers).
3. **📊 Check Cloudflare Security Logs** (Security > WAF > Logs).

---
![image](https://github.com/user-attachments/assets/44600aa6-badf-49a9-af86-d730fc83a50d)


![image](https://github.com/user-attachments/assets/6d3bc950-abf2-466a-8e8f-e2f460cda5f3)

![image](https://github.com/user-attachments/assets/6b6d6519-5f05-4172-9bf9-06050116e852)


![image](https://github.com/user-attachments/assets/426cbd82-9364-4696-a0ec-29e8031707cd)


![image](https://github.com/user-attachments/assets/77beacf1-d5c2-415a-8dbd-466174fa310b)




## 🏆 **License & Contact**
This guide is open-source under the MIT License.
For further support, contact **kamrul.us Admin** or visit [Cloudflare Support](https://support.cloudflare.com/).


![image](https://github.com/user-attachments/assets/1b77b3be-d949-49d5-b183-7192def40bdc)


