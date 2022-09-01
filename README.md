# CHIPS Snapshot procedure

### Step 1: Sync a CHIPS daemon to chain tip

Either clone and compile source code from https://github.com/chips-blockchain/chips, or use pre-compiled binaries on releases page.

Once synced to chain tip, shut your daemon off so that lock is not present on database.

### Step 2: Take snapshot using python tool

Clone repository located here: https://github.com/who-biz/chipsposbal2csv

Download prerequisite packages from `apt` and `pip`:

`sudo apt-get install python2.7-dev libleveldb-dev`

```
pip install plyvel==1.2.0
pip install base58
pip install pysqlite3
```

Then, take snapshot.  This will take a while.

```
cd chipsposbal2csv
python btcposbal2csv.py ~/.chips/chainstate ~/chips_addresses_w_bal.csv
```

Once this is complete, you should have a file in `home` directory titled `chips_addresses_w_bal.csv`.

### Step 3: Run script to distribute coins according to snapshot

You must have the required balance in your wallet to distribute to snapshot fully.  In the event that balance is insufficient, script will print a message indicating so.  It will also export JSON-formatted entries that have been excluded from snapshot to a file.

Clone repository located here: https://github.com/who-biz/blockchain_scripts

Run script:

```
cd ~/blockchain_scripts
./vrsc_sendmany_from_csv.sh ~/chips_addresses_w_bal.csv
```
