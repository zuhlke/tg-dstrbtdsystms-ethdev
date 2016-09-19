# tg-dstrbtdsystms-ethdev

## A Virtualbox Vagrant formula for an Ethereum development environment

To start, simply clone this repository (see "Clone or Download" button at the top of the [project's home page](https://github.com/zuhlke/tg-dstrbtdsystms-ethdev)), cd to the folder `tg-dstrbtdsystms-ethdev` and type `vagrant up`. The first time you do this, it will take a while because it has to download and install all the packages and tools.

To log into the VM by ssh, use `vagrant ssh`. To become root within the VM, use `sudo -i` or `sudo su -`.

### Release notes

At the current version, this does NOT install the mix-ide or mix packages. The MIX IDE has been [officially discontinued](https://github.com/ethereum/mix#mix-has-been-discontinued).

Instead, we install [Truffle](http://truffle.readthedocs.io/en/latest/) and [testrpc](https://github.com/ethereumjs/testrpc). Use a text editor (e.g. mousepad) or the [Solidity Browser](https://ethereum.github.io/browser-solidity/) to edit code.