# 🧭 Corda 5.2+ Kotlin CorDapp – Guide to Run Corda Nodes Locally (macOS)

This document walks you through **cloning, building, deploying, running, and testing** your CorDapp locally on **macOS** using **Corda 5.2+**.

---

## 1️⃣ Prerequisites

Before starting, ensure you have the following installed:

- **Java 17** – Required for Corda 5.2

```bash
java -version
```

- **Corda CLI (v5.2)** – Download from [Corda CLI](https://github.com/corda/corda-runtime-os/releases)
- **Docker Desktop** – Needed for Docker-based node deployment
- **IntelliJ IDEA (optional)** – For code completion, debugging, and Gradle tasks

---

## 2️⃣ Clone the CorDapp Template

Open a terminal and run:

```bash
git clone https://github.com/corda/corDapp-template-kotlin.git
cd cordapp-template-kotlin
git checkout release-V5.2
```

This template provides:

- Pre-configured Kotlin CorDapp project  
- Gradle build setup  
- Example flows (`com.template.flows`)  
- Example state (`TemplateState`)  
- Contract (`TemplateContract`)  

---

## 3️⃣ Build the Project

From the project root:

```bash
./gradlew clean build
```

- Compiles contracts and workflows  
- Generates `.jar` files for the nodes  

---

## 4️⃣ Deploy Nodes

Corda 5.2 uses the Gradle `deployNodes` task for node deployment:

```bash
./gradlew deployNodes
```

Creates node directories under:

```
build/nodes/
├── Notary/
├── PartyA/
└── PartyB/
```

Each node will contain:

- `corda.jar`  
- `node.conf`  
- `log/` folder  
- `persistence/` folder for vault database  

---

## 5️⃣ Start Nodes

```bash
cd build/nodes
./runnodes
```

- Opens terminal windows for each node: PartyA, PartyB, Notary  
- Each node logs its startup and RPC endpoints  

---

## 6️⃣ Interacting With the CorDapp

### 6.1 Using Corda CLI (RPC)

**List available flows:**

```bash
flow list
```

Example output:

```
com.template.flows.Initiator
net.corda.core.flows.ContractUpgradeFlow$Authorise
net.corda.core.flows.ContractUpgradeFlow$Deauthorise
net.corda.core.flows.ContractUpgradeFlow$Initiate
```

**Start a flow:**

```bash
flow start com.template.flows.Initiator receiver: "O=PartyB,L=New York,C=US"
```

- This triggers the Initiator flow from PartyA to PartyB  
- Returns a `SignedTransaction` ID  

**Query the vault (list stored states):**

```bash
flow start com.template.flows.QueryTemplateStates
```

- Returns all `TemplateState` objects stored in the vault  

---

## ✅ Summary

With this guide, you can now:

- Clone and explore a Kotlin CorDapp  
- Build and deploy virtual nodes  
- Run flows and interact via Corda CLI  
- Query vaults to validate transactions  

**Next Steps:**

- Implement multi-party flows  
- Add Token SDK or Accounts SDK  
- Test custom CorDapp flows with different scenarios  
- Explore automation via RPC or REST API  

---

Built for macOS • Corda 5.2+ • Kotlin CorDapp • Virtual Nodes • CLI & Gradle Driven Development
