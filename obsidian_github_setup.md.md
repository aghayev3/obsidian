
# Linking Your Computer to GitHub via SSH

**Date:** 2025-11-11  
**Tags:** #Git #SSH #Obsidian #PNPT

---

## Step 1 — Install Git
Check if Git is installed:
```bash
git --version
```
If not installed:
```bash
sudo pacman -S git   # for Arch Linux
```

---

## Step 2 — Configure Git
Set your name and email for commits:
```bash
git config --global user.name "yourusername"
git config --global user.email "12345678+yourusername@users.noreply.github.com"
```
> Using GitHub’s noreply email keeps your real identity private.

---

## Step 3 — Generate SSH Keys
Create a new SSH key pair:
```bash
ssh-keygen -t ed25519 -C "12345678+yourusername@users.noreply.github.com"
```
- `id_ed25519` = private key → **keep secret**  
- `id_ed25519.pub` = public key → **upload to GitHub**

Add the key to your SSH agent:
```bash
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
```

---

## Step 4 — Upload Public Key to GitHub
1. Go to GitHub → Settings → **SSH and GPG keys** → **New SSH key**  
2. Name the key (e.g., “ArchLaptop”)  
3. Paste the content of `id_ed25519.pub`  

---

## Step 5 — Test Connection
```bash
ssh -T git@github.com
```
Expected output:
```
Hi yourusername! You’ve successfully authenticated, but GitHub does not provide shell access.
```

---

## Step 6 — Link Obsidian Vault to GitHub
1. Initialize Git in your vault:
```bash
cd ~/path/to/ObsidianVault
git init
```
2. Add remote:
```bash
git remote add origin git@github.com:yourusername/YourVault.git
```
3. First commit:
```bash
git add .
git commit -m "Initial commit"
git push -u origin main
```
4. Optional: install **Obsidian Git** plugin for auto-commits.