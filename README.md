# Fuel

We suggest you use the [official documentation](https://docs.fuel.network/guides/running-a-node/running-a-testnet-node/). </br>
Below are the minimum system requirements for the project.</br>
CPU: 4 Core </br>
RAM: 16Gb </br>
SSD: 250Gb </br>
OS: Ubuntu 20.04 </br>


### Server preparation + install docker+docker-compose.
```
sudo apt update
sudo apt upgrade -y
sudo apt install -y curl git jq lz4 build-essential
sudo apt install -y unzip logrotate git jq sed wget curl coreutils systemd
sudo apt install screen -y
sudo apt install git -y
```

### Install node and run.
```
curl https://install.fuel.network | sh
export PATH="${HOME}/.fuelup/bin:${PATH}"
git clone https://github.com/FuelLabs/chain-configuration
screen -S fuel
```

### Generating P2P key:
```
fuel-core-keygen new --key-type peering
```

Example:
{
  "peer_id":"16Uiu2HAmEtVt2nZjzpXcAH7dkPcFDiL3z7haj6x78Tj659Ri8nrs",
  "secret":"b0ab3227974e06d236d265bd1077bb0522d38ead16c4326a5dff2f30edf88496",
  "type":"peering"
}
PLEASE SAVE AND BACKUP KEY!

### Running a Local node:
```
fuel-core run \
--service-name=fuel-sepolia-testnet-node \
--keypair YOURSECRET \
--relayer YOURRPCSEPOLIA \
--ip=0.0.0.0 --port=4000 --peering-port=30333 \
--db-path=~/.fuel-sepolia-testnet \
--snapshot /root/chain-configuration/ignition \
--utxo-validation --poa-instant false --enable-p2p \
--reserved-nodes /dns4/p2p-testnet.fuel.network/tcp/30333/p2p/16Uiu2HAmDxoChB7AheKNvCVpD4PHJwuDGn8rifMBEHmEynGHvHrf \
--sync-header-batch-size 100 \
--enable-relayer \
--relayer-v2-listening-contracts=0x01855B78C1f8868DE70e84507ec735983bf262dA \
--relayer-da-deploy-height=5827607 \
--relayer-log-page-size=500 \
--sync-block-stream-buffer-size 30
```

Collapse the screen:
```
CTRL +A +D
```

### Useful commands
```
screen -r fuel
```

Connecting to the local node from a browser wallet:
```
http://yourip:4000/v1/graphql
```
