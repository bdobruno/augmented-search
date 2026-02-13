## Hetzner Server Setup

- Spin up cheap Hetzner Ubuntu server with IPv4
- Add SSH key during setup
- Create firewall allowing ports 22/TCP and 41641/UDP
- SSH into server

## Get SSH Key from Mac

**Check if you have an existing key:**
```bash
cat ~/.ssh/id_ed25519.pub
```

**Or for RSA key:**
```bash
cat ~/.ssh/id_rsa.pub
```

**If no key exists, generate one:**
```bash
ssh-keygen -t ed25519 -C "your_email@example.com"
```

**Copy the entire output** (starts with `ssh-ed25519` or `ssh-rsa`) and paste into Hetzner SSH key field during server setup.

**Never share the private key** (`~/.ssh/id_ed25519` without `.pub`) - only share the public key (`.pub` file).

## SSH Into Server

**Get server IPv6 address from Hetzner console** (looks like `2a01:4f8:xxxx:xxxx::1/64`)

**Remove the `/64` suffix and connect:**
```bash
ssh root@2a01:4f8:xxxx:xxxx::1
```

**On first connection, type `yes` when prompted about authenticity**

**Alternative - if using IPv4:**
```bash
ssh root@95.217.xxx.xxx
```

## Server Configuration

- Run: `apt update && apt upgrade -y`
- Install Tailscale: `curl -fsSL https://tailscale.com/install.sh | sh`

## Enable IP Forwarding
```bash
echo 'net.ipv4.ip_forward = 1' | sudo tee -a /etc/sysctl.d/99-tailscale.conf
echo 'net.ipv6.conf.all.forwarding = 1' | sudo tee -a /etc/sysctl.d/99-tailscale.conf
sudo sysctl -p /etc/sysctl.d/99-tailscale.conf
```

## Advertise Exit Node

- Run: `tailscale up --advertise-exit-node`
- Approve exit node in Tailscale admin console (https://login.tailscale.com/admin/machines)

## Mac Setup

- Install Tailscale on Mac
- Connect to exit node: `tailscale up --exit-node=<server-name> --accept-routes`
- Verify: `curl ifconfig.me` (should show Hetzner IPv4)

## Client Access

- Give Hetzner IPv4 to clients for database whitelist
- Toggle exit node on/off as needed:
- Enable: `tailscale up --exit-node=<server-name> --accept-routes`
- Disable: `tailscale up --exit-node= --accept-routes`
