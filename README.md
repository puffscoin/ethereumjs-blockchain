# SYNOPSIS

A module to store and interact with blocks on the PUFFScoin blockchain.

# INSTALL

`npm install puffscoinjs-blockchain`

# API

[./docs/](./docs/README.md)

# EXAMPLE

The following is an example to iterate through an existing gpuffs DB (needs `level` to be installed separately).

This module performs write operations. Making a backup of your data before trying it is recommended. Otherwise, you can end up with a compromised DB state.

```javascript
const level = require('level')
const Blockchain = require('puffscoinjs-blockchain').default
const utils = require('ethereumjs-util')

const gpuffsDbPath = './chaindata' // Add your own path here. It will get modified, see remarks.
const db = level(gpuffsDbPath)

new Blockchain({ db: db }).iterator(
  'i',
  (block, reorg, cb) => {
    const blockNumber = utils.bufferToInt(block.header.number)
    const blockHash = block.hash().toString('hex')
    console.log(`BLOCK ${blockNumber}: ${blockHash}`)
    cb()
  },
  err => console.log(err || 'Done.'),
)
```

**WARNING**: Since `puffscoinjs-blockchain` is also doing write operations
on the DB for safety reasons only run this on a copy of your database, otherwise this might lead
to a compromised DB state.

# puffscoinjs

See our organizational [documentation](http://puffscoin.leafycauldronapothecary.com/puffwiki/puffscoinjs-user-guide/) for an introduction to `PuffscoinJS` 
