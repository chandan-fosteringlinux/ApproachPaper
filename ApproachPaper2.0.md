# 🧾 ConfigMap Generator – Approach Document (Quarkus + Systemd + Freemarker)

---

## 🖼️ Architecture Diagram

```plaintext
+-----------------------+     +--------------------+
| blueprint XML files   |     | dummy.cfg          |
| (1 or more)           |     | (key-value pairs)  |
+-----------------------+     +--------------------+
           |                          |
           |                          |
           v                          v
  +----------------------------------------------------+
  |        ConfigMap Generator (Java 17 + Quarkus)     |
  |----------------------------------------------------|
  | 1. Load application.properties from /home/usr/...  |
  | 2. Extract {{keys}} from XML                       |
  | 3. Load dummy.cfg                                  |
  | 4. Match keys and apply logic                      |
  | 5. Use Freemarker to render ConfigMap YML          |
  | 6. Write log to /var/log/configmap-generator.log   |
  +----------------------------------------------------+
                          |
                          v
               +------------------------+
               | One .yml per .xml file |
               +------------------------+
```

---

## 📚 Table of Contents

- 🎯 Objective  
- 🔧 Technologies Used  
- 🧠 Overview  
- 📁 Input Files  
- 🚀 Execution Flow  
- 📤 Output Files  
- 📄 Service Management via Systemd  
- 🧪 Testing Ideas  
- 📌 Future Scope  

---

## 🎯 Objective

To build a daemonized Java service that:

- Extracts all `{{keys}}` from `.xml` files.
- Matches with `.cfg` values.
- Uses **Freemarker** to generate `.yml` files in ConfigMap format.
- Maps `.xml` ↔ `.yml` 1:1.
- Supports external configuration.
- Logs activity to a defined system path.

---

## 🔧 Technologies Used

| Tool/Framework        | Purpose                          |
|-----------------------|----------------------------------|
| Java 17               | Core language                    |
| Quarkus               | Application framework            |
| Maven                 | Dependency management            |
| Simple XML Parser     | Key extraction                   |
| Freemarker            | Templating engine                |
| Systemd               | Daemon management                |
| Java IO               | File operations                  |

---

## 🧠 Overview

The tool processes `.xml` files to extract keys, matches them with `.cfg`, and renders ConfigMap YAML using Freemarker. Each `.xml` leads to a `.yml`. The tool runs continuously or via cron under `systemd`, and logs events for traceability.

---

## 📁 Input Files

### 1. blueprint.xml

```xml
<route>
  <to uri="http://{{api.host}}/call"/>
  <to uri="jms:queue:{{jms.queue.name}}"/>
</route>
```

### 2. dummy.cfg

```properties
api.host=localhost:8080
jms.queue.name=paymentQueue
```

---

## 🚀 Execution Flow

### Step 1: Read application.properties

- Located at `/home/usr/myapp/application.properties`
- Includes:
  - XML input directory
  - CFG path
  - Output directory
  - Template path
  - Log file path

### Step 2: Read XML files

- Regex extract `{{key}}` patterns.
- One `.xml` leads to one `.yml`.

### Step 3: Read CFG File

- Load key-value pairs into a `Map`.

### Step 4: Match Keys

- If key exists → assign value.
- Else → assign `"null"`.

### Step 5: Render YAML via Freemarker

- Use pre-defined `configmap.ftl` template.
- Bind the data and generate output.

### Step 6: Write Output

- Output path: `/home/usr/myapp/filename.configmap.yml`
- One `.yml` per `.xml`.

---

## 📤 Output Files

| File Name                   | Description                      |
|----------------------------|----------------------------------|
| `<filename>.configmap.yml` | Generated ConfigMap YML          |
| `systemd service log`      | Log output at `/var/log/...`     |

---

## 📄 Service Management via systemd

### Service File (`/etc/systemd/system/configmap-generator.service`)

```ini
[Unit]
Description=ConfigMap Generator Service
After=network.target

[Service]
ExecStart=/usr/bin/java -jar /home/usr/myapp/configmap-generator.jar
WorkingDirectory=/home/usr/myapp
Restart=always
StandardOutput=append:/var/log/configmap-generator.log
StandardError=append:/var/log/configmap-generator.log

[Install]
WantedBy=multi-user.target
```

### Commands

```bash
Re-executes the systemd process. It’s used after a systemd binary update 
sudo systemctl daemon-reexec

# Enable the service to start on boot
sudo systemctl enable configmap-generator

# Start the service now
sudo systemctl start configmap-generator

# Optional: View logs
sudo journalctl -u configmap-generator

# Optional: Stop the service manually when needed
sudo systemctl stop configmap-generator

```

---

## 🧪 Testing Ideas

| Test Case                       | Expected Result                                |
|--------------------------------|--------------------------------------------------|
| All keys match in `.cfg`       | Full YAML with values                           |
| Missing key in `.cfg`          | Output shows `"null"`                           |
| Extra keys in `.cfg`           | Ignored                                         |
| Multiple XML files             | Multiple `.yml` files generated                 |
| Invalid template path          | Log error, service continues                    |
| Log rotation test              | System log grows and rotates correctly          |

---

## 📌 Future Scope

- GUI for file selection & output preview
- Schema validation of `.cfg`
- Hot-reload of updated XML or CFG
- Unit tests for template logic
- Integration with CI/CD pipelines

---
