
# 🎓 Blockchain-Based Certificate Issuance & Verification DApp

### **Role-Based Access Control (RBAC) — Admin, Issuer, Student — Public Verification**

This project is a **complete blockchain-powered certificate system** built using:

* **Solidity (Smart Contracts)**
* **Streamlit (Frontend DApp)**
* **Web3.py (Blockchain bridge)**
* **Ganache (Local Ethereum Network)**

It enables **secure, tamper-proof certificate generation, management, and verification** on the blockchain.

---

## 🚀 Features

### **🔐 Role-Based Access Control (RBAC)**

Each user logging in with wallet address is assigned a role:

| Role            | Permissions                                          |
| --------------- | ---------------------------------------------------- |
| **Admin**       | Add/Remove Issuers & Students                        |
| **Issuer**      | Issue & Revoke certificates (only those they issued) |
| **Student**     | View their certificates                              |
| **Public User** | Verify validity of any certificate                   |

---

### **🎓 Certificate Management**

* Issue certificates uniquely identified by **bytes32 hash**
* Store metadata: Name, UID, Course, IssueDate, Student, Issuer
* Students automatically receive linked certificates
* Issuers can revoke their own certificates

---

### **🌍 Public Verification**

Anyone can enter the certificate hash to check:

* Whether certificate exists
* Whether it is valid or revoked

No login required.

---

### **💻 Streamlit Web App**

* Clean UI
* Separate dashboards
* Auto role-detection from wallet address
* Secure access control mirrored from smart contract

---

## 📂 Project Structure

```
├── contract/
│   ├── OCertificate.sol
│   ├── OCertificate.json       # ABI from deployment
│
├── app.py                      # Streamlit frontend
├── README.md                   # This file
├── requirements.txt
└── assets/ (optional)
```

---

## ⚙️ Installation & Setup (Full Working Environment)

Follow these steps exactly to run the system end-to-end.

---

## **1️⃣ Install Dependencies**

### Install Python Packages

```
pip install streamlit web3 hexbytes
```

### Install Ganache

Download Ganache GUI:
[https://trufflesuite.com/ganache/](https://trufflesuite.com/ganache/)

---

## **2️⃣ Start Ganache**

* Create a **New Workspace**
* RPC Server must be:

```
http://127.0.0.1:7545
```

Copy accounts — these will be used as:

* Admin
* Issuers
* Students

---

## **3️⃣ Compile & Deploy Contract (Ganache)**

You can deploy using Remix:

1. Go to [https://remix.ethereum.org](https://remix.ethereum.org)
2. Upload `OCertificate.sol`
3. Select Compiler 0.8.x
4. Deploy using **Injected Provider → Ganache**
5. Copy the deployed **contract address**
6. Download the **ABI JSON** and place it at:

```
contract/OCertificate.json
```

---

## **4️⃣ Configure Streamlit App**

In **app.py**, update:

```python
RPC_URL = "http://127.0.0.1:7545"
CONTRACT_ADDRESS = "YOUR_DEPLOYED_CONTRACT_ADDRESS"
```

Make sure your ABI JSON exists here:

```
contract/OCertificate.json
```

---

## **5️⃣ Run the App**

```
streamlit run app.py
```

Open in browser:
**[http://localhost:8501](http://localhost:8501)**

---

## 🌐 Application Flow

### **👑 Admin Flow**

* Login using Admin wallet
* Add Issuers
* Add Students
* Verify certificates

---

### **🏫 Issuer Flow**

* Login using Issuer wallet
* Issue certificate (Student must be pre-added)
* Revoke certificate

---

### **🎓 Student Flow**

* Login using Student wallet
* View all certificate hashes
* View certificate details

---

### **🔍 Public Verifier Flow**

* No login required
* Enter certificate hash
* Check validity immediately through `verifyCertificate()`

---

## 🧩 Smart Contract Summary

* Implements strict **RBAC**
* Stores certificates in a **bytes32 → struct** mapping
* Maintains **per-student certificate list**
* Provides **public verification**
* Uses access control inside `getCertificate()`:

```
student OR issuer OR admin
```

---

## 🐞 Troubleshooting

### **❗ Certificate not showing for Student**

Check:

* Student is added by Admin before issuance
* Issuer used correct student address
* Student logged in using same Ganache wallet

---

### **❗ “Access Denied” when viewing certificate**

Cause:
You logged in with an address that is NOT:

* the student, OR
* the issuer, OR
* admin

Solution:
Login with the correct wallet.

---

### **❗ Public cannot view certificate details**

This is expected.
Public can ONLY verify validity → not view full metadata.

---

## 📘 Requirements File

`requirements.txt`

```
streamlit
web3
hexbytes
```

---

## 📸 Screenshots (Add yours)

```
assets/
  admin_panel.png
  issuer_panel.png
  student_view.png
  public_verify.png
```

Add screenshots for better presentation.

---

## 📝 License

MIT License (2025)

---

## ⭐ Contribution

PRs and suggestions are welcome!

