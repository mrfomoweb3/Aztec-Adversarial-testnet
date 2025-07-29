# Aztec-Adversarial-testnet

# Aztec Validator Setup Guide (Explorer Role)
<img width="1600" height="900" alt="image" src="https://github.com/user-attachments/assets/21ea8cb5-3dc1-4b54-ab12-91607da59911" />

This guide walks you through joining the **Aztec validator set** and earning the **Explorer** role during the testnet phase.

---

##  What You’ll Need

- [ZK Passport App](https://passport.aztec.network)
- Sepolia Testnet ETH  
  → [Claim from Faucet](https://sepoliafaucet.com)  
- Your Discord username
<img width="1600" height="900" alt="image" src="https://github.com/user-attachments/assets/ca55dc66-5a27-4186-a711-ef9bb7d7b1fb" />

---

## Step 1: Verify Identity with ZK Passport

1. Go to [testnet.aztec.network](https://testnet.aztec.network)
2. Click **“Join Validator Set”**

<img width="1600" height="900" alt="image" src="https://github.com/user-attachments/assets/f2c952d8-d9c1-48a5-aa0e-88964b22e9b4" />

3. Confirm your ID eligibility:
   - Issuing Country
   - Issuing Date
   - Expiry Date
<img width="1600" height="900" alt="image" src="https://github.com/user-attachments/assets/4f734042-9ceb-4920-9990-282e252162fc" />


4. **Connect your wallet**


<img width="1600" height="900" alt="image" src="https://github.com/user-attachments/assets/e3822f47-193b-49d8-a58a-5acac81abf25" />

> ⚠️ Note: Aztec allows only one passport per testnet.

---

##  Step 2: Verify Humanity

- Use the **ZK Passport app** to verify you're human.
- No personal data is stored — your proof remains private (ZK tech FTW).
<img width="1600" height="900" alt="image" src="https://github.com/user-attachments/assets/db3bbe89-9031-42ca-893c-8803ece4a931" />



---

## Step 3: Register as Validator

- Once verified, click **Register Validator**
- A transaction window will pop up
- Confirm the TX:  
  `0.0001 ETH @ 0.03 Gwei (Sepolia Testnet)`
  <img width="1600" height="900" alt="image" src="https://github.com/user-attachments/assets/bbeef40e-ba74-484f-a9d0-1426569c44c3" />


---

##  Step 4: Claim Your Discord Role

- Enter your **Discord username**
- Optionally, provide your **company name**
- You will receive the **Explorer** role in Aztec’s Discord
<img width="1600" height="900" alt="image" src="https://github.com/user-attachments/assets/f76b61aa-943e-471c-b510-3b360ef171ae" />

---

##  Final Steps

- View your validator dashboard:  
  https://dashtec.xyz

- Check your queue position:  
  https://dashtec.xyz/queue

---

## 🛠️ Troubleshooting

- You might encounter minor issues, just try again.
- Remember, **this is a testnet**: the goal is to test, break, and improve the system.
- More countries are now supported on ZK Passport, so check again if you weren’t eligible before.

---

Made it through? Welcome to the testnet validator set.
Now go decentralize with style.

---

# Aztec Node Update Guide (Version 1.2.0)

This guide explains how to **update your Aztec node** using either Docker Compose or CLI methods. It includes steps to stop the node, update CLI tools, remove old data, and restart the node correctly.

---

##  Docker Compose Method

### 1. Stop the Node

```bash
# Option A: Stop using image name
docker stop $(docker ps -q --filter "ancestor=aztecprotocol/aztec") \
  && docker rm $(docker ps -a -q --filter "ancestor=aztecprotocol/aztec")

# Option B: Stop using docker compose
cd aztec
docker compose down -v
```

### 2. Update CLI Tools

```bash
source ~/.bashrc
aztec-up 1.2.0
```

### 3. Delete Old Data

```bash
rm -rf ~/.aztec/alpha-testnet/data/
```

### 4. Rerun the Node

```bash
docker compose up -d
```

> ✅ **Note:** Ensure you're in the `aztec` directory where `docker-compose.yml` exists.  
> For full setup instructions, see the [Aztec Docker Guide](#).

---

##  CLI Method

### 1. Stop the Node

```bash
# Kill all aztec-related screen sessions
screen -ls | grep -i aztec | awk '{print $1}' | xargs -I {} screen -X -S {} quit
```

> Or manually terminate the screen session running your node.

### 2. Update CLI Tools

```bash
source ~/.bashrc
aztec-up 1.2.0
```

### 3. Delete Old Data

```bash
rm -rf ~/.aztec/alpha-testnet/data/
```

### 4. Rerun the Node

```bash
aztec start --node --archiver --sequencer \
  --network alpha-testnet \
  --l1-rpc-urls RPC_URL \
  --l1-consensus-host-urls BEACON_URL \
  --sequencer.validatorPrivateKey 0xYourPrivateKey \
  --sequencer.coinbase 0xYourAddress \
  --p2p.p2pIp IP
```

### Replace the placeholders:

- `RPC_URL`: Your Layer 1 RPC endpoint  
- `BEACON_URL`: Your consensus layer Beacon endpoint  
- `0xYourPrivateKey`: Your EVM private key (Don't share to anyone)
- `0xYourAddress`: Your EVM public address  
- `IP`: Your server’s public IP address

---


