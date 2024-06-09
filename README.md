# avail-light-node

Min Req : 
CPU 	2+ vcpu  |
RAM 	4+ GB   |
Storage 	40+ GB SSD   |
UBUNTU 	22    |

# Update


````
sudo apt update && sudo apt upgrade -y
sudo apt-get install make curl clang pkg-config libssl-dev build-essential
````


````
cd
wget https://github.com/availproject/avail-light/releases/download/v1.9.0/avail-light-linux-amd64.tar.gz
tar -xvzf avail-light-linux-amd64.tar.gz
mv avail-light-linux-amd64 avail-light
chmod +x avail-light
rm -rf avail-light-linux-amd64.tar.gz
````


````
mkdir -p $HOME/.avail/turing/bin
mkdir -p $HOME/.avail/turing/data
mkdir -p $HOME/.avail/turing/config
mkdir -p $HOME/.avail/identity
````



````
curl -Ls https://raw.githubusercontent.com/Core-Node-Team/Testnet-TR/main/Avail-Turing/config.yml > $HOME/.avail/turing/config/config.yml
````

# Service

````
sudo tee /etc/systemd/system/availd.service > /dev/null <<EOF
[Unit]
Description=Avail Light Client
After=network.target
StartLimitIntervalSec=0

[Service]
User=root
ExecStart=/root/avail-light \
--network "turing" \
--config /root/.avail/turing/config/config.yml \
--app-id 0 \
--identity /root/.avail/identity/identity.toml
 
Restart=always
RestartSec=30
Environment="DAEMON_HOME=$HOME/.avail"

[Install]
WantedBy=multi-user.target
EOF
````

# Start

````
sudo systemctl daemon-reload
````

````
systemctl enable availd
````

````
sudo systemctl restart availd && journalctl -u availd -fo cat
````

# Logs

````
journalctl -u availd -fo cat
````
