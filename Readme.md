# 🧾 Approach Document for ConfigMap Generator Software (Quarkus Framework)

## Architecture Diagram
![architecture diagram](architecture.svg)

## 📚 Table of Contents
1. [🎯 Objective](#-objective)
2. [🔧 Technologies Used](#-technologies-used)
3. [🎯 Overview of the ConfigMap Generation Process](#-Overview-of-the-ConfigMap-Generation-Process)
4. [📁 Input Files](#-input-files)
5. [🚀 Step-by-Step Execution Flow](#-step-by-step-execution-flow)
6. [📤 Output Files](#-output-files)
7. [🧪 Testing Ideas](#-testing-ideas)
8. [📌 Future Scope](#-future-scope)

## 🎯 Objective
The main goal of this software is to:

> Extract all `{{keys}}` from a `.xml` files, match them with a `.cfg` file, and create a `ConfigMap.yml` file.

- If the key exists in the `.cfg` file ➡️ use the actual value.
- If the key is missing in `.cfg` but present in `.xml` files ➡️ use `null` as the value.

---

## 🔧 Technologies Used
- Java 17
- Quarkus Framework
- Maven
- Simple XML Parser
- Java File Reader / Writer

---

## 🧠 Overview of the ConfigMap Generation Process
1. User provides 2 types of input files:
   - `.xml` (contains keys like `{{some.key}}`)
   - `.cfg` (key-value pair config file)
2. The program extracts all used (keys) from the .XML files.
3. It checks each key in the `.cfg` files:
   - If match is found → fetch value and assign that value to the key
   - If not found → assign `null` value to the key
4. A new `ConfigMap.yml` file is created with all key-value pairs.

---

## 📁 Input Files

### 1. `.xml`
```xml
<route>
  <to uri="http://{{api.host}}/call"/>
  <to uri="jms:queue:{{jms.queue.name}}"/>
</route>
```

### 2. `.cfg`
```properties
api.host=localhost:8080
jms.queue.name=paymentQueue
```

---

## 🚀 Step-by-Step Execution Flow

### 🥇 Step 1: Read the XML File
- Open the `blueprint.xml` file.
- Search for all `{{...}}` patterns.
- Extract key names like `api.host`.

### 🥈 Step 2: Read the `.cfg` Files
- Load the `.cfg` files.
- Store all key-value pairs in a `Map`.

### 🥉 Step 3: Match Keys
- For each extracted key from XML:
  - If the key exists in `.cfg`, get its value.
  - Else, assign `null`.

### 🏁 Step 4: Write `configMap.yml`
- Format the matched values into this format:
```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: my-config
data:
  api.host: "localhost:8080"
  jms.queue.name: "paymentQueue"
  some.missing.key: "null"
```

---

## 📤 Output Files

| File Name             | Purpose                            |
|----------------------|-------------------------------------|
| `configMap.yml`       | Final output for ConfigMap         |

---

## 🧪 Testing Ideas

| Test Case                        | Expected Result                                    |
|----------------------------------|----------------------------------------------------|
| All keys match in `.cfg`         | All keys in `configMap.yml` have actual values     |
| Some keys missing                | Missing keys show `"null"` in `configMap.yml`      |
| Extra keys in `.cfg` file        | Only keys from XML are used, extras ignored        |
| Empty `dummy.cfg` file           | All values in `configMap.yml` will be `"null"`     |

---

## 📌 Future Scope
- Add UI for selecting files
