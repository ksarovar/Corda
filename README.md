# 🪙 R3 Corda 5.2+ Installation Guide (macOS)

This guide sets up **R3 Corda 5.2+** on macOS with all required dependencies.  
It includes a **manual method to install the Corda CLI**, which works even when the official installer script fails.

---

## ⚙️ 1. Install Homebrew

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
brew update
brew --version
```

---

## ☕ 2. Install OpenJDK 17

```bash
brew install openjdk@17
```

---

## 🧩 3. Configure Java Environment Variables (Apple Silicon)

```bash
echo 'export PATH="/opt/homebrew/opt/openjdk@17/bin:$PATH"' >> ~/.zshrc
echo 'export CPPFLAGS="-I/opt/homebrew/opt/openjdk@17/include"' >> ~/.zshrc
echo 'export JAVA_HOME="/opt/homebrew/opt/openjdk@17"' >> ~/.zshrc
source ~/.zshrc
```

**For Intel Macs:**

```bash
echo 'export PATH="/usr/local/opt/openjdk@17/bin:$PATH"' >> ~/.zshrc
echo 'export CPPFLAGS="-I/usr/local/opt/openjdk@17/include"' >> ~/.zshrc
echo 'export JAVA_HOME="/usr/local/opt/openjdk@17"' >> ~/.zshrc
source ~/.zshrc
```

---

## 🔗 4. Link JDK for macOS System Recognition

```bash
sudo ln -sfn $(brew --prefix openjdk@17)/libexec/openjdk.jdk /Library/Java/JavaVirtualMachines/openjdk-17.jdk
```

Verify Java:
```bash
java -version
```

✅ Expected:
```
openjdk version "17.0.17" ...
OpenJDK Runtime Environment (Homebrew)
OpenJDK 64-Bit Server VM
```

---

## 🐳 5. Install Docker Desktop

```bash
brew install --cask docker
open /Applications/Docker.app
```

Verify:
```bash
docker --version
docker-compose --version
```

---

## 🧱 6. Install Gradle

```bash
brew install gradle
gradle -v
```

---

## 🧰 7. Install Git

```bash
brew install git
git --version
```

---

## 🛠️ 8. Install Corda CLI (Manual Method)

> ⚠️ The Homebrew tap for Corda CLI is deprecated.  
> This method manually sets up the CLI for macOS.

### Step 1: Create CLI folder

```bash
mkdir -p ~/.corda/cli/bin
```

### Step 2: Copy the CLI JAR

Assuming `corda-cli.jar` is in your current folder:

```bash
cp corda-cli.jar ~/.corda/cli/bin/corda-cli.jar
```

### Step 3: Create a launcher script

```bash
nano ~/.corda/cli/bin/corda-cli
```

Paste the following:

```bash
#!/bin/bash
java -jar "$HOME/.corda/cli/bin/corda-cli.jar" "$@"
```

Save and exit (`Ctrl+O`, `Enter`, `Ctrl+X`).

### Step 4: Make it executable

```bash
chmod +x ~/.corda/cli/bin/corda-cli
```

### Step 5: Add CLI to PATH

```bash
echo 'export PATH="$HOME/.corda/cli/bin:$PATH"' >> ~/.zshrc
source ~/.zshrc
```

### Step 6: Verify CLI

```bash
corda-cli --version
```

✅ Expected:
```
Corda CLI version 5.2.0.0
```

---

## 🐘 9. Optional: Kotlin (for CorDapp development)

```bash
brew install kotlin
kotlin -version
```

---

## 🐘 10. Optional: PostgreSQL (for node database)

```bash
brew install postgresql
brew services start postgresql
```

---

## 🧾 11. Verify Full Setup

```bash
brew --version
java -version
docker --version
docker-compose --version
gradle -v
git --version
corda-cli --version
```

All should print valid versions.

---

## ⚡ Notes & Troubleshooting

- **Log folder errors**: If you see `Could not create directory /Users/krushna/.corda/cli/logs`, run:

```bash
mkdir -p ~/.corda/cli/logs
chmod -R 755 ~/.corda/cli
```

- **Do NOT use `sudo` with install.sh** — it may install CLI under `/var/root/` instead of your home folder.  

- **Always check PATH**: `echo $PATH` should include `$HOME/.corda/cli/bin`.

---

## ✅ Summary of Dependencies

| Tool | Version | Installation |
|------|---------|--------------|
| Homebrew | Latest | Official script |
| OpenJDK | 17 | Homebrew |
| Docker | Latest | Homebrew Cask |
| Docker Compose | Latest | Included in Docker Desktop |
| Gradle | Latest | Homebrew |
| Git | Latest | Homebrew |
| Corda CLI | 5.2.0 | Manual installer (`corda-cli.jar`) |
| Kotlin | 1.9+ | Homebrew |
| PostgreSQL | 15+ | Homebrew |

---

## 🚀 Ready to Use

Your macOS is now fully set up for **Corda 5.2+ development** and testing.  
You can start creating and managing virtual nodes with:

```bash
corda-cli preinstall
corda-cli vnode
corda-cli mgm
```

