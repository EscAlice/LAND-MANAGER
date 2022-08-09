### 以托管服务部署方式到 the graph
>原版本较低，无法使用the graph hosted-service 方式部署，故需要做如下修改

>0.
old -> package.json</font>
```
 "@graphprotocol/graph-cli": "^0.17.1",
 "@graphprotocol/graph-ts": "^0.17.0",
```

new -> package.json
```
 "@graphprotocol/graph-cli": "0.33.0",
 "@graphprotocol/graph-ts": "0.27.0",
```

>1.
```
npm install -g @graphprotocol/graph-cli
```
```
npm install -g @graphprotocol/graph-ts
```

>2.
old -> datasource.yaml
```
 mapping:
      kind: ethereum/events
      apiVersion: 0.0.1
```

new -> datasource.yaml
```
 mapping:
      kind: ethereum/events
      apiVersion: 0.0.6
```

old -> subgraph.yaml
```
specVersion: 0.0.2

apiVersion: 0.0.3
```

new -> subgraph.yaml
```
specVersion: 0.0.4

apiVersion: 0.0.6
```

>3.
```
npm install
```

>4.
```
npm run codegen
```

>5.
old -> authorization.ts
```
EthereumEvent
event: EthereumEvent
if (address == null)


Value.fromBytes(address!)
```

new -> authorization.ts
```
ethereum
event: ethereum.Event,

if (address === null)

Value.fromBytes(address)
```

old -> /utils/estate.ts
```
EthereumEvent
event: EthereumEvent
```

new -> /utils/estate.ts
```
ethereum
event: ethereum.Event,
```

old -> /mappings/estate.ts
```
  let estate = Estate.load(estateId)
 
  let parcels = estate.parcels
```


new -> /mappings/estate.ts
```
  let estate = Estate.load(estateId)
  if (!estate) {
    return
  }
  let parcels = estate.parcels
  if (!parcels) {
    return
  }
```

>6.
```graph auth --product hosted-service <ACCESS_TOKEN>```
```graph deploy --product hosted-service <GITHUB_USER>/<SUBGRAPH NAME>```

>7.
Build completed: QmWLD9BLH83Pjxa26RhCYSJo5nUwydFPpF2rp2CN8UToo2

Deployed to https://thegraph.com/explorer/subgraph/escalice/land-manager

Subgraph endpoints:
Queries (HTTP):     https://api.thegraph.com/subgraphs/name/escalice/land-manager