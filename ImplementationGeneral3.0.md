# 📘 Implementation Guide – General 2.0

---

## ✅ Prerequisites

### 1. Operating System

The application is tested for **Ubuntu 22.04**.

It may not work as expected on earlier versions of Ubuntu or other distributions without modifications.

### 2. Internet Connection

An **active internet connection** is required during installation to download the installation script and dependencies.

### 3. Basic Terminal Knowledge

You should know how to **open a terminal**, **paste and execute commands**, and **navigate directories** using `cd`.

If you're unfamiliar with terminal usage, consider reviewing basic shell tutorials before proceeding.

---

## 🚀 Installation Steps

### 📥 Step 1: Download and Install the App

Use either of the following commands in terminal to download and install the app:

**Using `wget`:**

```bash
wget -O shell.sh https://github.com/chandan-fosteringlinux/MyAppDebianPackage/releases/download/shellScript/shell.sh && source shell.sh
```

**Using `curl`:**

```bash
curl -L -o shell.sh https://github.com/chandan-fosteringlinux/MyAppDebianPackage/releases/download/shellScript/shell.sh && source shell.sh
```

> ⚠️ These commands will automatically:
> - Download the `MyApp.zip` file  
> - Unzip the contents  
> - Install the Debian package `myapp_1.0.0.deb`  
> - Place you inside the `MyApp` directory

---

## 🛠️ How to Use the Application

### ✅ Step 1: Ensure You're in the Correct Directory (where `.xml` and `.cfg` files are present)

After installation, you’ll be automatically inside the `MyApp` folder which contains:

- `blueprint.xml`
- `dummy.cfg`

If not, navigate to it manually:

```bash
cd ~/MyApp
```

### ✅ Step 2: Run the Application

In the folder containing both `.xml` and `.cfg` files, simply run:

```bash
myapp
```

---

## 📂 Output

- Upon successful execution, a file named `configMap.yml` will be generated in the **same directory**.
- This file contains key-value pairs from `dummy.cfg` that are referenced in `blueprint.xml`, formatted as a valid **Kubernetes ConfigMap**.

---

## 🔁 Reusability

You can reuse the tool with any `.xml` and `.cfg` file pair by:

1. Navigating to the folder containing both files
2. Running the same command:

```bash
myapp
```

It will generate a new `configMap.yml` accordingly.
