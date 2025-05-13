# 📘 Implementation General 2.0

---

## ✅ Prerequisites

### 1. zip and unzip Installed  
Ensure that `zip` and `unzip` are installed and properly configured on your system.

You can check the version by running:

```bash
zip -v
```

If `zip` is not installed, download it from the official website or use a package manager:

```bash
sudo apt update
sudo apt install zip unzip
```

# 🛠️ Steps to Use the Application

## 1. Download the Zip File

Download the provided `MyApp.zip` file to your local machine.

## 2. Navigate to the Zip File Location

Open a terminal and navigate to the directory where `MyApp.zip` is located:

```bash
cd /path/to/your/zipfile
```

## 3. Unzip the Package

Extract the contents of the zip file using:

```bash
unzip MyApp.zip
```

## 4. Enter the MyApp Folder

Change directory to the unzipped folder:

```bash
cd MyApp
```

## 5. Install the Debian Package

Install the application using the following command:

```bash
sudo apt install ./myapp_1.0.0.deb
```

## 6. Run the Application

Inside the `MyApp` folder, you will find two files: `blueprint.xml` and `dummy.cfg`. Run the application using:

```bash
myapp
```

## 📂 Output

If executed successfully, a file named `configMap.yml` will be generated in the same directory. This file will include all key-value pairs from `dummy.cfg` that are referenced in `blueprint.xml`, formatted as a Kubernetes ConfigMap.

## 🔁 Reusability

Now, you can generate `configMap.yml` files from any `.xml` file containing keys and any `.cfg` file containing key-value pairs by simply navigating to the folder containing both files and executing:

```bash
myapp
```
