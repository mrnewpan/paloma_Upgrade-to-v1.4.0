## Upgrade-to-v1.4.0

```
sudo systemctl stop palomad
sudo systemctl stop pigeond
```

### upgrade paloma
```
cd || return
rm -rf paloma
git clone https://github.com/palomachain/paloma.git
cd paloma || return
git checkout v1.4.0
make install
sudo mv -f $HOME/go/bin/palomad /usr/local/bin/palomad
palomad version # v1.4.0
```
### upgrade pigeon
```
curl -L https://github.com/palomachain/pigeon/releases/download/v1.3.0/pigeon_Linux_x86_64.tar.gz > pigeon.tar.gz
tar -xvzf pigeon.tar.gz
rm pigeon.tar.gz
sudo mv -f pigeon /usr/local/bin/pigeon
pigeon version # v1.3.0
```

```
sudo systemctl start pigeond
sudo systemctl start palomad
sudo journalctl -u palomad -f --no-hostname -o cat
```
### Check logs
```
sudo journalctl -u palomad -f --no-hostname -o cat
```
```
sudo journalctl -u pigeond -f --no-hostname -o cat
```
### Check synchronization
```
palomad status 2>&1 | jq .SyncInfo.catching_up
```
