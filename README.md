# 🪙 Corda 5 Installation Guide (macOS - 2025)

This guide explains how to install **R3 Corda 5** and all required dependencies on **macOS (Intel or Apple Silicon)** with the latest stable versions as of **October 2025**.

---

## 🧠 Overview

Corda 5 is a **modern, cloud-native blockchain platform** built with:
- Java 17+
- Docker / Kubernetes
- Corda CLI
- Gradle 8+
- Kotlin 1.9+
- PostgreSQL

---

## ⚙️ System Requirements

| Component | Recommended |
|------------|-------------|
| macOS | 12 (Monterey) or newer |
| CPU | Apple Silicon (M1/M2/M3) or Intel |
| RAM | 16 GB+ |
| Storage | 20 GB+ free space |
| Internet | Required for image pulls |

---

## 🧩 Step 1. Install Core Dependencies

### 🟡 1. Homebrew
If not installed:
```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

Update Homebrew:
```bash
brew update
```

---

### 🟢 2. Java (JDK 17)
Corda 5 requires **Java 17**.

```bash
brew install openjdk@17
```

Set environment variables:
```bash
echo 'export PATH="/usr/local/opt/openjdk@17/bin:$PATH"' >> ~/.zshrc
echo 'export JAVA_HOME=$(/usr/libexec/java_home -v17)' >> ~/.zshrc
source ~/.zshrc
```

Verify:
```bash
java -version
# Expected output: openjdk 17.x
```

---

### 🟢 3. Kotlin (1.9+)
```bash
brew install kotlin
kotlin -version
```

---

### 🟢 4. Gradle (8+)
```bash
brew install gradle
gradle -v
```

---

### 🟢 5. Git
```bash
brew install git
git --version
```

---

### 🟢 6. Docker Desktop
Corda 5 uses containerized services.

```bash
brew install --cask docker
```

After installation:
- Open **Docker Desktop** manually once.
- Ensure it’s running:
  ```bash
  docker version
  ```

---

### 🟢 7. Kubernetes
If using Docker Desktop, enable **Kubernetes** under:
> **Docker Desktop → Settings → Kubernetes → Enable Kubernetes**

Otherwise install Minikube:
```bash
brew install minikube
minikube start
```

---

### 🟢 8. Corda CLI (latest)
Corda 5 comes with a CLI for deployment and network control.

```bash
brew tap corda/corda-cli
brew install corda-cli
corda-cli version
```

---

### 🟢 9. PostgreSQL (Database)
Corda 5 nodes use PostgreSQL for persistence.

```bash
brew install postgresql
brew services start postgresql
```

---

### 🟢 10. IntelliJ IDEA (Optional)
Recommended IDE for CorDapp development:
```bash
brew install --cask intellij-idea
```

---

## 🧰 Step 2. Verify Setup

Run these commands:
```bash
java -version
kotlin -version
gradle -version
docker version
kubectl version --client
corda-cli version
```

All should return valid versions.

---

## 🚀 Step 3. Run a Local Corda 5 Network

Create and start a test network:
```bash
corda-cli network create --name test-network
corda-cli network start test-network
```

This spins up a local Corda 5 network using Docker.

---

## 🧱 Step 4. (Optional) Build a Sample CorDapp

Clone samples:
```bash
git clone https://github.com/corda/corda5-samples.git
cd corda5-samples/basic-cordapp
```

Build:
```bash
./gradlew build
```

Deploy via CLI or Kubernetes as per your setup.

---

## 📦 Summary of Dependencies (Latest 2025 Versions)

| Dependency | Recommended Version | Install Command |
|-------------|--------------------|-----------------|
| JDK | 17 | `brew install openjdk@17` |
| Kotlin | 1.9+ | `brew install kotlin` |
| Gradle | 8+ | `brew install gradle` |
| Git | latest | `brew install git` |
| Docker | latest | `brew install --cask docker` |
| Kubernetes | latest | `brew install minikube` *(optional)* |
| PostgreSQL | 15+ | `brew install postgresql` |
| Corda CLI | latest | `brew tap corda/corda-cli && brew install corda-cli` |
| IntelliJ IDEA | latest | `brew install --cask intellij-idea` |

---

## 🧾 Notes

- Ensure Docker is running before starting the network.
- Use Java 17 strictly for Corda 5.
- PostgreSQL must be running as a background service.

---

## 🧰 Optional: Automated Installer Script

You can automate all steps with one command:
```bash
curl -fsSL https://example.com/setup_corda5_mac.sh | bash
```
*(Replace with your script URL if hosting it yourself)*

---

## ✅ Done!

Your macOS is now **Corda 5 ready** 🎉  
You can start developing or deploying CorDapps immediately.

---
