# node
## Deposit
- create deposit/key data
```sh
docker run -it --rm -v $(pwd)/keys:/app/validator_keys push ghcr.io/depinfra/staking-deposit-cli:latest new-mnemonic --num_validators=1 --mnemonic_language=english --eth1_withdrawal_address <withdrawal_address>
```

- deposit eth (params from deposit_data-xxx.json)
```sh
cast send <deposit_contract> "deposit(bytes,bytes,bytes,bytes32)" <pubkey> <withdraw_credentials> <signature> <deposit_root_data> --value 32ether --rpc-url https://rpc.depinfra.org --private-key 0xxxxx 
```
## Import account
```sh
 docker run -ti --rm -v ./config:/config -v ./data/lighthouse/custom/validators:/root/.lighthouse/custom/validators -v ./keys:/keys   ethpandaops/lighthouse:pawan-electra-alpha7-b2b728d lighthouse account validator import --directory=/keys --testnet-dir=/config
```
## Run validator node
```sh
docker run -ti --rm -v ./config:/config -v ./data/lighthouse:/root/.lighthouse   ethpandaops/lighthouse:pawan-electra-alpha7-b2b728d lighthouse vc --beacon-nodes=http://188.245.206.182:5052 --suggested-fee-recipient=0x5266Dfa5ae013674f8FdC832b7c601B838D94eE6  --init-slashing-protection --testnet-dir=/config --debug-level=info
```
## Withdraw
```sh
docker run --net=host --rm -v ./password.txt:/password.txt -v ./all:/all -v ./config:/config sigp/lighthouse lighthouse account validator exit \
             --keystore="$keystore_file" \
             --beacon-node="$BEACON_NODE_URL" \
             --password-file="$PASSWORD_FILE" \
         --no-confirmation
```
