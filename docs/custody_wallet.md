# Custody Wallet

## About

Custody smart transaction ensures that funds in custody wallet can be moved only with approval of
both the "custodian" and the "authorizer" until specified time has been exceeded.    
Once the lock period has passed, custodian can move funds without the approval.     

## Setup

To install this repository, and all requirements, clone this repository and then run:

```
$ python3 -m venv .venv
$ . .venv/bin/activate
$ pip install -r requirements.txt
$ pip install -e .
```
## Launch

Before launching custody wallet, make sure there is an instance of ledger-sim running.   
run:
```
$ ledger-sim
```

## Rate Limited Wallet Usage (step by step)
  1. **RUN**
     - Open three terminal windows and run  ```custody_wallet```
     - Open one terminal and run ```wallet```
     This tutorial assumes **Terminal 1 to 3** are custody wallets and **Terminal 4** is standard wallet
  2. **Get Chia**
     - **Terminal 1**
       - type "**4**" and press Enter (Get 1 Billion Chia)
  3. **Create Custody Wallet**
     - **Terminal 1** (Wallet 1 will be have to approve transaction during lockup period)
       - type "**5**" and press Enter
       - type "**a**" and press Enter
     - **Terminal 2**
       - type "**5**" and press Enter
       - type "**c**" and press Enter
       - from **Terminal 1** copy  "Authorizer pubkey" and paste it to **Terminal 2** (Press enter in terminal 2)
       - from **Terminal 2** copy "Custodian pubkey" and paste it to **Terminal 1** (Press enter in terminal 1)
       - type "**5000**" and press Enter (select the time when funds unlock)
     - **Terminal 1** 
       - type "**5000**" and press Enter (Same lock time)
       - type "**1000**" (we're sending 1000 Chia into custody wallet)
       - type "**4**" (farm a block that includes the last transaction)
     - **Terminal 2** 
       - type "**3**" and press Enter. (Get updates)
       - type "**2**" (view funds, there should be 1000 chia in custody balance)
  3. **Move to a different custody**
     - **Terminal 2** 
       - type "**6**" and press Enter
     - **Terminal 3**
       - type "**5**" and press Enter
       - type "**c**" and press Enter
       - from **Terminal 3** copy custodian pubkey and paste it to **Terminal 2**
     - **Terminal 1**
       - type "**7**" and press Enter
       - from **Terminal 3** copy custodian pubkey and paste it to **Terminal 1**
       - type **1000** and press Enter ("Value being moved from terminal 2")
       - From **Terminal 1** copy "**Approving Signature**" and paste it to **Terminal 2**
     - **Terminal 3**
       - From **Terminal 1** copy "**Authorizing pubkey**" and paste it to **Terminal 3**
       - Type "**5000**" (same lock time as previous custody)
     - **Terminal 1**
       - type "**4**" and press Enter
     - **Terminal 2**
       - type "**3**" and press Enter
       - ###### type "**2**" and press Enter (View funds to confirm they have moved)
     - **Terminal 3**
       - type "**3**" and press Enter
       - type "**2**" and press Enter (Confirm that funds are now in custody of this wallet)
  4. **Confirm that we can move funds after lock period has passed**
     - **Terminal 1** (Time increase by 1000 milliseconds every time we print wallet details)
       - type "**1**" and press Enter
       - type "**1**" and press Enter
       - type "**1**" and press Enter
       - type "**1**" and press Enter
       - type "**1**" and press Enter
       - type "**1**" and press Enter (time should be 6000 here)
     - **Terminal 3**
       - type "**3**" and press Enter
       - type "**6**" and press Enter
     - **Terminal 4**
       - type "**4**" and press Enter
     - **Terminal 3**
       - from **Terminal 4** copy "**New pubkey**" and paste it to **Terminal 3**
     - **Terminal 1**
       - type "**4**" and press Enter
     - **Terminal 3**
       - type "**3**" and press Enter
       - type "**2**" and press Enter (Confirm Custody balance is 0)
     - **Terminal 4**
       - type "**2**" and press Enter (Get update)
       - type "**4**" and press Enter (Confirm Current balance is 1000) )
