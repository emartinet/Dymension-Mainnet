```
sudo apt install liblz4-tool
systemctl stop dymd
cp $HOME/.dymension/data/priv_validator_state.json $HOME/.dymension/priv_validator_state.json.backup
cp $HOME/.dymension/config/priv_validator_key.json $HOME/.dymension/priv_validator_key.json.backup
dymd tendermint unsafe-reset-all --home $HOME/.dymension --keep-addr-book
curl -L http://37.120.189.81/dymension_mainnet/dym_snap.tar.lz4 | tar -Ilz4 -xf - -C $HOME/.dymension
mv $HOME/.dymension/priv_validator_state.json.backup $HOME/.dymension/data/priv_validator_state.json
sudo systemctl daemon-reload
sudo systemctl restart dymd
sudo journalctl -u dymd.service -f --no-hostname -o cat
```
