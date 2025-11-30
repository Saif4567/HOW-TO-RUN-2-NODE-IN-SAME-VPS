🚀 How to Run 2 Gensyn Nodes on the Same VPS (Port Change Method)

This guide explains how to run a second Gensyn node on the same VPS by cloning a new instance of rl-swarm and changing all necessary ports from 3000 → 3001.

⚠️ Warning:
Running 2 nodes requires high RAM (64GB or more).
Do NOT try this on low RAM VPS.

✅ Step 1 — Create a New Directory for Node 2
mkdir node1

✅ Step 2 — Open the Directory
cd node1 && ls

✅ Step 3 — Clone the RL-Swarm Repository
git clone https://github.com/gensyn-ai/rl-swarm/

✅ Step 4 — Enter the RL-Swarm Folder
cd rl-swarm

✅ Step 5 — Change All 3000 Ports to 3001 in modal-login/package.json

Open file in nano:

nano modal-login/package.json

🔧 Inside nano editor:

Find every 3000

Change all to 3001

Total around 5 entries, but check fully

Save nano:

CTRL + X → Y → ENTER

✅ Step 6 — Change Ports in code-gen-swarm.yaml

Open config:

nano code_gen_exp/config/code-gen-swarm.yaml

🔧 Inside file:

Replace ALL 3000 → 3001

Save:

CTRL + X → Y → ENTER

✅ Step 7 — Update Startup Commands in modal-login/package.json

Open again:

nano modal-login/package.json


Now modify two lines:

Before	After
next dev	next dev -p 3001
next start	next start -p 3001

Save:

CTRL + X → Y → ENTER

✅ Step 8 — Create New Screen Session

If your original node uses screen gensyn,
create a different screen name for node 2:

screen -S gensyn2

✅ Step 9 — Create Virtual Environment & Start Node
python3 -m venv .venv && source .venv/bin/activate && bash run_rl_swarm.sh


Your second Gensyn node is now running on port 3001 in a screen session.

Detach screen:

CTRL + A + D

✅ Step 10 — Create Cloudflare Tunnel for Login

Open a new terminal tab of same VPS and run:

1. Download Cloudflared
wget -q https://github.com/cloudflare/cloudflared/releases/latest/download/cloudflared-linux-amd64.deb

2. Install it
sudo dpkg -i cloudflared-linux-amd64.deb

3. Create tunnel for port 3001
cloudflared tunnel --url http://localhost:3001


A public URL will appear →
Open it → Login & access your second Gensyn node UI.

🎉 Finished!

Now you have:

✔️ Two Gensyn nodes running on the same VPS
✔️ First node on port 3000
✔️ Second node on port 3001
✔️ Both nodes running in separate screens
✔️ Cloudflare tunnel for separate login access
