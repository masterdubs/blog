---
title: "Web3 tips and tricks"
date: 2022-09-07T17:22:00+04:00
draft: false
---


# EVM:

## Generate an EVM address with python

### Step 1 install package
```
pip install web3
```


### Step 2 generate an EVM address
```
from eth_account import Account
import secrets
priv = secrets.token_hex(32)
private_key = "0x" + priv
print ("THIS IS YOUR PRIVATE KEY, SAVE IT BUT NEVER SHARE IT:", private_key)
acct = Account.from_key(private_key)
print("Your Public Address:", acct.address)
```
