# WIS2

Deployment of a WIS2 stack and multiple WIS2NODEs on a K8S cluster

## WIS2 Stack
### Components
- a 6-node Redis cluster (3 masters and 3 slaves) accessible via ClusterIP at addresses redis-{0..2}.redis:6379
- a 2-node EMQX cluster accessible via ClusterIP at the address ws://emqx-headless:8083
- a 2-node wis2node cluster accessible via Ingress at the address http://wis2node.< your_hostname >

### Deployment

- Install cert-manager and emqx-operator following [this procedure](https://docs.emqx.com/en/emqx-operator/latest/getting-started/hello-emqx-operator.html)


- Install wis2node using the following commands:
```
helm repo add wis2node https://moz411.github.io/wis2node
helm -n wis2node --create-namespace upgrade --install wis2node wis2node/wis2node
```

## Administration

- The logs of the wis2node can be viewed with the command `kubectl -n <namespace> logs service/<wis2node>`

Example:
```
# kubectl -n dsi-isi-wis2 logs service/fr-meteofrance 
Found 2 pods, using pod/fr-meteofrance-9cf9fc6d9-ksqwd
Defaulted container "wis2gb" out of: wis2gb, leader-elector

> node-red-docker@4.0.2 start
> node $NODE_OPTIONS node_modules/node-red/red.js $FLOWS --userDir /data

16 Aug 12:58:09 - [info] 

Welcome to Node-RED
===================

16 Aug 12:58:09 - [info] Node-RED version: v4.0.2
16 Aug 12:58:09 - [info] Node.js  version: v20.13.1
16 Aug 12:58:09 - [info] Linux 5.14.0-362.8.1.el9_3.x86_64 x64 LE
16 Aug 12:58:09 - [info] Loading palette nodes
node-red-contrib-createrandom backend started.
16 Aug 12:58:10 - [info] Settings file  : /data/settings.js
16 Aug 12:58:10 - [info] HTTP Static    : / > /
16 Aug 12:58:10 - [info] Context store  : 'default' [module=memory]
16 Aug 12:58:10 - [info] User directory : /data
16 Aug 12:58:10 - [warn] Projects disabled : editorTheme.projects.enabled=false
16 Aug 12:58:10 - [info] Flows file     : /data/flows.json
16 Aug 12:58:10 - [warn] Using unencrypted credentials
16 Aug 12:58:10 - [info] Server now running at http://127.0.0.1:1880/admin/
...
```

