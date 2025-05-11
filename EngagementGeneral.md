# 📘 How to Use the ConfigMap Generator JAR

Follow the steps below to correctly execute the `configmap-generator-1.0.0-SNAPSHOT-runner.jar` and generate a ConfigMap from your `blueprint.xml` and `dummy.cfg` files:

---

## ✅ Prerequisites

### 1. Java 17 Installed
Ensure that Java Development Kit (JDK) version **17** is installed and properly configured on your system.

You can check the version by running:

```bash
java -version
```

If Java 17 is not installed, download it from the official website or use a package manager:

```bash
sudo apt update
sudo apt install openjdk-17-jdk
```

### 2. Required Files
Ensure the following files are available in the **same directory**:

- `blueprint.xml`: The XML file containing the Camel route definitions.
- `dummy.cfg`: The configuration file containing key-value pairs for placeholder resolution.

---

## 🛠️ Steps to Run the Application

### 1. Copy the JAR File
Place the executable JAR file `configmap-generator-1.0.0-SNAPSHOT-runner.jar` in the same folder as your `blueprint.xml` and `dummy.cfg`.

### 2. Open Terminal
Launch a terminal or command prompt and navigate to the folder containing the JAR and required files. Example:

```bash
cd /path/to/your/executablesJar
```

### 3. Execute the JAR File
Run the JAR file using the following command:

```bash
java -jar configmap-generator-1.0.0-SNAPSHOT-runner.jar
```

---

## 📂 Output

- If execution is successful, a file named `configMap.yml` will be generated in the same directory.
- This file will contain all key-value pairs from `dummy.cfg` that are referenced in the `blueprint.xml` file, structured as a Kubernetes ConfigMap.

---
