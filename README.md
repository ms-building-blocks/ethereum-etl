# Extract transactions
## Build docker image
```sh
docker build -t ethereum-etl:latest .
docker image ls
```

## Export
```sh
docker run -v ${PWD}/output:/ethereum-etl/output \
            export_blocks_and_transactions  --start-block 0 --end-block 500000 \
            -b 100000 --provider-uri https://mainnet.infura.io \
            --blocks-output blocks.csv --transactions-output transactions.csv \
             ethereum-etl:latest 
```

