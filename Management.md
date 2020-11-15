# Common Commands
The following are some common commands you may want to use while running this setup.

### Login to User
``` console
sudo su - username
```

### Geth Syncing Progress
``` console
sudo su - geth
geth attach
eth.syncing
```

Alternatively, you can paste the following instead of *eth.syncing*

	var lastPercentage = 0;var lastBlocksToGo = 0;var timeInterval = 10000;
	setInterval(function(){
   	var percentage = eth.syncing.currentBlock/eth.syncing.highestBlock*100;
   	var percentagePerTime = percentage - lastPercentage;
   	var blocksToGo = eth.syncing.highestBlock - eth.syncing.currentBlock;
   	var bps = (lastBlocksToGo - blocksToGo) / (timeInterval / 1000)
   	var etas = 100 / percentagePerTime * (timeInterval / 1000)

	var etaM = parseInt(etas/60,10);
   	console.log(parseInt(percentage,10)+'% ETA: '+etaM+' minutes @ '+bps+'bps');
    
   	lastPercentage = percentage;lastBlocksToGo = blocksToGo;
	},timeInterval);

Be aware that the syncing progress will only be report correctly for the first part of the syncing process, the bandwidth intensive *block downloading* part. 

After the blocks are downloaded then comes the disk IO and CPU limited *state trie syncing* part, which is currently impossible to monitor due to Ethereum limitations. The above commands won't report meaningful data during that part.

### Service Statuses
To see the status of system services:

```console
sudo systemctl status beacon-chain
sudo systemctl status validator
sudo systemctl status geth
sudo systemctl status geth-goerli
sudo systemctl status prometheus
sudo systemctl status grafana-server
sudo systemctl status eth2stats
sudo systemctl status node_exporter
sudo systemctl status blackbox_exporter
```

Or, to see the status of all at once:
```console
sudo systemctl status beacon-chain validator geth geth-goerli prometheus grafana-server eth2stats node_exporter blackbox_exporter
```
### Service Logs
To watch the logs in real time:

```console
sudo journalctl -u beacon-chain -f
sudo journalctl -u validator -f
sudo journalctl -u geth -f
sudo journalctl -u geth-goerli -f
sudo journalctl -u prometheus -f
sudo journalctl -u grafana-server -f
sudo journalctl -u eth2stats -f
sudo journalctl -u node_exporter -f
sudo journalctl -u blackbox_exporter -f
```
### Restarting Services
To restart a service:

```console
sudo systemctl restart beacon-chain
sudo systemctl restart validator
sudo systemctl restart geth
sudo systemctl restart geth-goerli
sudo systemctl restart prometheus
sudo systemctl restart grafana-server
sudo systemctl restart eth2stats
sudo systemctl restart node_exporter
sudo systemctl restart blackbox_exporter
```

### Stopping Services
Stopping a service is separate from disabling a service. Stopping a service stops the current execution of the server, but does not prohibit the service from starting again after a system reboot. If you intend for the service to stop running and to not restart after a reboot, you will want to stop and disable a service.

To stop a service:

```console
sudo systemctl stop beacon-chain
sudo systemctl stop validator
sudo systemctl stop geth
sudo systemctl stop geth-goerli
sudo systemctl stop prometheus
sudo systemctl stop grafana-server
sudo systemctl stop eth2stats
sudo systemctl stop node_exporter
sudo systemctl stop blackbox_exporter
```

**Important:** If you intend to stop the beacon chain and validator in order to run these services on a different system, stop the services using the instructions in this section, and disable these services following the instructions in the next section. You will be at risk of losing funds through slashing if you accidentally validate the same keys on two different systems, and failing to disable the services may result in your beacon chain and validator running again after a system reboot.

### Disabling Services
To disable a service so that it no longer starts automatically after a reboot:

```console
sudo systemctl disable beacon-chain
sudo systemctl disable validator
sudo systemctl disable geth-goerli
sudo systemctl disable prometheus
sudo systemctl disable grafana-server
sudo systemctl disable eth2stats
sudo systemctl disable node_exporter
sudo systemctl disable blackbox_exporter
```

### Enabling Services
To re-enable a service that has been disabled:

```console
sudo systemctl enable beacon-chain
sudo systemctl enable validator
sudo systemctl enable geth
sudo systemctl enable geth-goerli
sudo systemctl enable prometheus
sudo systemctl enable grafana-server
sudo systemctl enable eth2stats
sudo systemctl enable node_exporter
sudo systemctl enable blackbox_exporter
```
### Starting Services
Re-enabling a service will not necessarily start the service as well. To start a service that is stopped:

```console
sudo systemctl start beacon-chain
sudo systemctl start validator
sudo systemctl start geth
sudo systemctl start geth-goerli
sudo systemctl start prometheus
sudo systemctl start grafana-server
sudo systemctl start eth2stats
sudo systemctl start node_exporter
sudo systemctl start blackbox_exporter
```

### Upgrading Prysm
Upgrading the Prysm beacon chain and validator clients is as easy as restarting the service when running the prysm.sh script as we are in these instructions. To upgrade to the latest release, simply restart the services.

```console
sudo systemctl restart beacon-chain
sudo systemctl restart validator
```

### Changing systemd Service Files
If you edit any of the systemd service files in `/etc/systemd/system` or another location, run the following command prior to restarting the affected service:

```console
sudo systemctl daemon-reload
```
Then restart the affected service:
```console
sudo systemctl restart SERVICE_NAME
```

- Replace SERVICE_NAME with the name of the service for which the service file was updated. For example, `sudo systemctl restart beacon-chain`.

### Updating Prysm Options
To update the configuration options of the beacon chain or validator, edit the Prysm configuration file located in the home directories for the services.

```console
sudo nano /home/validator/prysm-validator.yaml
sudo nano /home/beacon/prysm-beacon.yaml
```

Then restart the services:

```console
sudo systemctl restart validator
sudo systemctl restart beacon-chain
```
