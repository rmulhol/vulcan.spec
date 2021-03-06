Assume nothing is shared.

One instance per deployment for similar contracts.

So local tables will need namespacing by address.

But be problematic with postgraphile

## Pip Medianizer

```
contract Med = {
  version: 1.0
  lib: makerdao/medianizer
  address: {
    mainnet: 0x729D19f657BD0614b4985Cf1D82531c67569197B
  }
  description: "Medianized price oracle used by tub.pip"
}

type Poke {
  guy: Address indexed
  val: Decimal
  pip: Decimal
  block: Int
  time: Datetime
  tx: String
}

event LogNote(sig: 'poke(bytes32)') {
  Poke.create {
    guy:   event.guy
    val:   event.foo
    pip:   Med.call read()
    block: event.blockNumber
    time:  event.timestamp
    tx:    event.transactionHash
  }
}

type Query {
  allPokes(args): [Poke]
}
```

## Pep Medianizer

```
contract Med = {
  version: 1.0,
  lib: makerdao/medianizer
  address: {
    mainnet: 0x99041F808D598B782D5a3e498681C2452A31da08
  },
  description: "Medianized price oracle used by tub.pep"
}

type Poke {
  guy: Address indexed
  val: Decimal
  pep: Decimal
  block: Int
  time: Datetime
  tx: String
}

event LogNote(sig: 'poke(bytes32)') {
  Poke.create {
    guy:   _.guy
    val:   _.foo
    pep:   Med.call read()
    block: _.blockNumber
    time:  _.timestamp
    tx:    _.transactionHash
  }
}

type Query {
  allPokes(...): [Poke]
}

```
