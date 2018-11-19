# Extract transactions
## Build docker image
```sh
docker build -t ethereum-etl:latest .
docker image ls
```

## Export
```sh
mkdir -p output
chmod -R 777 output
docker rm -f exporter
# First 1M blocks
docker run -v ${PWD}/output:/ethereum-etl/output \
            --name=exporter ethereum-etl:latest  \
            export_blocks_and_transactions  --start-block 0 --end-block 1000000 \
            -b 100000 --provider-uri http://172.17.0.1:8545 \
            --blocks-output /ethereum-etl/output/blocks.csv --transactions-output /ethereum-etl/output/transactions.csv 
             
```

## Note - Run Etherem node instance
```sh
ETH_DATA=/home/ethereum
geth --datadir=$ETH_DATA \
        --rpc  --rpccorsdomain "*" \
        --rpcaddr "172.17.0.1" --rpcport "8545" \
        --wsapi "admin,db,eth,debug,miner,net,shh,txpool,personal,web3" --rpcapi "admin,db,eth,debug,miner,net,shh,txpool,personal,web3" --ipcpath "$ETH_DATA/geth.ipc"  --cache=8196

```
