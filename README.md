[![Documentation Status](https://readthedocs.org/projects/pyopenwatch/badge/?version=latest)](https://pyopenwatch.readthedocs.io/en/latest/?badge=latest)
![PyPI](https://img.shields.io/pypi/v/pyopenwatch)

# pyOpENWatch

```
pip install pyOpENWatch
```

Fetch the NFTs that has been minted on the blockchain, with current tools,
NFT data is hard to reach or depends on commercial third party
APIs.

This is not desirable for various reasons, PyOpENWatch offers an alternative.

## Usage

```python
from pyopenwatch import EthereumNFTWatcher
watcher = EthereumNFTWatcher(host, port, log_level)
watcher.fetch_nfts_until_block(terminal_block_hash, limit, callback)
```

Here, the `pyopenwatch.EthereumNFTWatcher` does the heavy lifting, you will have to point it
to an Ethereum node, using the `host` and `port`. The node _can_ be a light node.
`log_level` refers to [Python's logging levels](https://docs.python.org/3/library/logging.html#levels)
if passed, you can control what sort of information is being logged.

The watcher function traverses the blockchain and finds the NFTs being held inside,
the `terminal_block_hash` and `limit` can be provided to limit the number of blocks
the PyOpENWatch will fetch before terminating.

The `callback` function is the actual driving part of the package, it is a function
with the signature `(pyopenwatch.NFT) => None`. When the `EthereumNFTWatcher` finds a new NFT,
it initialises an `pyopenwatch.NFT` class and calls this `callback`.

Pass a function that takes found NFTs and process them as they are found.

### Logging

My understanding of the Ethereum nodes is that they can be extremely volatile,
and at numerous points significant errors may occur, thes errors are similar to
dropped packages in the TCP protocol, seem to occur when syncing issues occur,
in order to preserve functionality, instead of throwing errors, we log them instead,
the default behaviour of the `pyopenwatch.EthereumNFTWatcher` is to log these in the
`ERROR` level.

If you set the `logger_level` to `INFO`, newly found NFTs and mint transactions will
be logged. If the `logger_level` is set to `DEBUG` the newly fetched transactions and
blocks wil be logged.

## Use Case

This Python module was created as a part of a project to create a tool to find stolen
images minted as NFTs to help artists recover their stolen art. As you can probably
guess, I find NFTs and technology surrounding them less than ideal and I would
appereciate if dApp and Blockchain developers would refrain from using this library.

I would also like people who use this technology to limit illegal blockchain activity
to get in touch.

I understand that I cannot legally enforce this in any way, this is GPLv3 project,
so _legally_ you are free to do whatever as long as you follow the License, but
still, I hope my words hold some weight for people.
