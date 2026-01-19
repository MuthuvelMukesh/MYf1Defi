# MYf1Defi

Small midnight-friendly blockchain playground in a single HTML file.

The goal is to learn the core building blocks (hashes → blocks → chaining → tamper detection → proof-of-work) with tiny, readable changes.

## What’s in here

- `index.html`: interactive demo (no build tools, no dependencies)

## Run it (Windows)

This demo uses the browser’s WebCrypto API (`crypto.subtle`), which works reliably from a local server.

1) Open a terminal in this folder

2) Start a tiny web server:

- If you have Python:
	- `py -m http.server 8000`
	- (or) `python -m http.server 8000`

3) Open:

- `http://localhost:8000`

## What you’ll learn (in the UI)

### Step 1: Hashes

A hash is a one-way fingerprint of data.

- Same input → same hash
- Tiny change → totally different hash

### Step 2: A Block

A “block” is just structured data that includes:

- `data`: the payload
- `prevHash`: the previous block’s hash (the link)
- `timestamp`, `nonce`: typical block fields

The block hash is the SHA-256 of the block’s JSON.

### Step 2 (continued): Tamper detection

Click **Store this hash**, then edit the block.

- If the stored hash doesn’t match the recomputed hash → the block is tampered.

### Step 2 (continued): Proof-of-Work (“mining”)

Mining = find a `nonce` so the hash starts with N zeros (difficulty).

- Higher difficulty → more attempts
- If anything in the block changes, the hash changes, and the proof no longer matches

### Step 3: Two Blocks = A Chain

Block 2 automatically uses Block 1’s hash as its `prevHash`.

- Change Block 1 → Block 2 must change too

### Step 3 (continued): Mine Block 2

Mine Block 2 separately. If Block 1 changes, Block 2’s proof-of-work becomes invalid until you re-mine.

### Step 4: Ledger View + Rules

The ledger summarizes the chain and checks validity under simple rules:

- require link (Block 2 `prevHash` must match Block 1 hash)
- require PoW (both blocks must satisfy the difficulty)

Try toggling rules to see how “valid chain” depends on the rule set.

## Next ideas (optional)

- Add a third block to show longer re-mining cascades
- Add transactions as an array and hash the Merkle root (later)
- Add a very small “consensus” simulation (longest chain / most work)
