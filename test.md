# 🧭 Corda 5.2+ CorDapp Template – Clone, Build, Deploy & Run (macOS)

This guide walks you through **cloning a CorDapp template**, building it, deploying virtual nodes, installing the CorDapp, running flows, and validating results on **macOS** using **Corda 5.2+**.

---

## 1. Clone a CorDapp Template

```bash
git clone https://github.com/corda/some-cordapp-template.git
cd some-cordapp-template
```

The template usually contains:

- `states/` – example states  
- `contracts/` – rules for state validity  
- `workflows/` – flows to automate actions  

> **Important:** Ensure the template is compatible with Corda 5.2.x.

---

## 2. Build & Package the CorDapp

```bash
./gradlew clean build
```

After a successful build, you should see a `.cpi` file:

```bash
build/libs/my-cordapp-1.0.cpi
```

### Troubleshooting Build Errors

- Open `build.gradle.kts`  
- Confirm `corda-api` version is set to 5.2.x  

Example:

```kotlin
cordaVersion = "5.2.0"
```

---

## 3. Deploy Virtual Nodes & Install the CorDapp

### Prepare the Environment

```bash
corda-cli preinstall
```

### Create Virtual Nodes

```bash
corda-cli vnode create --name PartyA
corda-cli vnode create --name PartyB
```

### Install the CorDapp CPI on Each Node

```bash
corda-cli bundle install --cpi build/libs/my-cordapp-1.0.cpi --vnode PartyA
corda-cli bundle install --cpi build/libs/my-cordapp-1.0.cpi --vnode PartyB
```

### Start the Nodes

```bash
corda-cli vnode run --name PartyA
corda-cli vnode run --name PartyB
```

Logs will appear in:

```
~/.corda/cli/logs
```

---

## 4. Run a Simple Flow

Invoke a sample flow to test the CorDapp:

```bash
corda-cli flow start --vnode PartyA --flow MyExampleFlow --args "PartyB,100"
```

> Replace `MyExampleFlow` and arguments based on your template.

---

## 5. Verify the State is Recorded

Check both nodes' vaults:

```bash
corda-cli vault query --vnode PartyA --state MyExampleState
corda-cli vault query --vnode PartyB --state MyExampleState
```

Both nodes should show the shared state if the flow succeeded.

---

## 6. Inspect & Validate

- **Check Vaults** – Ensure states are visible only to correct parties  
- **Logs** – Check `~/.corda/cli/logs/*.log` for errors  
- **Network** – Confirm nodes can see each other; flows complete

---

## 7. Optional Advanced Steps

- Upgrade CorDapp CPI versions  
- Explore Token SDK or Accounts SDK  
- Deploy multiple parties, observer nodes, or notary pools  
- Run custom vault queries  
- Automate flows via RPC/REST API  

> Official Docs: [Corda 5.2 Developer Documentation](https://docs.corda.net/docs/corda-os/5.2/index.html)

---

## 8. Summary of Commands

| Step | Command / Action |
|------|-----------------|
| Clone template | `git clone https://github.com/corda/some-cordapp-template.git` |
| Build CorDapp | `./gradlew clean build` |
| Preinstall nodes | `corda-cli preinstall` |
| Create virtual nodes | `corda-cli vnode create --name PartyX` |
| Install CorDapp | `corda-cli bundle install --cpi ... --vnode PartyX` |
| Run nodes | `corda-cli vnode run --name PartyX` |
| Run flow | `corda-cli flow start ...` |
| Query vault | `corda-cli vault query --vnode PartyX --state ...` |

---

## 🎉 You're Ready!

Your macOS environment is now fully set up to:

- Develop  
- Deploy  
- Test  

**CorDapps on Corda 5.2 using virtual nodes.**

### Next Steps

- Explore multi-party flows  
- Implement tokenization  
- Simulate production-like network setups

---

Built for macOS • Corda 5.2+ • Virtual Nodes • CLI-Driven Development
