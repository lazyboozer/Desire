<p align="center">
  <img src="https://i.imgur.com/s7rXj0A.png" width="100"/>

[WEBSITE](https://www.desire-crypto.com/ "desire-crypto.com") [COINMARKETCAP](https://coinmarketcap.com/currencies/desire/ "CoinmarketCap") [BITCOINTALK](https://bitcointalk.org/index.php?topic=2272607.0 "Bitcoitalk Forum") [DISCORD](https://coinmarketcap.com/currencies/desire/ "Discord Live Chat")

</p>

Desire Core staging tree 0.12.2.2
=========================================

What is Desire?
--------

Desire is an experimental new digital currency that enables anonymous, instant payments to anyone, anywhere in the world. Desire uses peer-to-peer technology to operate with no central authority: managing transactions and issuing money are carried out collectively by the network. Desire Core is the name of the open source software which enables the use of this currency.

For more information, as well as an immediately useable, binary version of the Desire Core software, see https://bitcointalk.org/index.php?topic=2272607.0.

Desire Specifications
--------

- Release date: 15/10/2017 / Premine ~ 4%
- ASIC resistance
- NeoScrypt hashing algorithm
- Difficulty retargets using Dark Gravity Wave
- CPU/GPU/ mining
- Block reward is controlled by: 2222222/(((Difficulty+2600)/9)^2)
- Mastenode reward: 

<p align="left">

| Block         | Award MN           | 
| ------------- |:------------------:| 
| 0             | 20.0%              | 
| 158000        | 25.0%              | 
| 175280        | 30.0%              |  
| 192560        | 35.0%              |
| 209840        | 37.5%              |
| 227120        | 40.0%              |
| 244400        | 42.5%              |
| 261680        | 45.0%              |
| 278960        | 47.5%              |
| 313520        | 50.0%              |

</p>

- Block generation: 2.5 minutes
- InstantSend confirmation: ~5 seconds
- Est. ~22M Max Coins
- Decentralized Masternode Network
- Superior Transaction Anonymity using PrivateSend

License
--------

Desire Core is released under the terms of the MIT license. See COPYING for more information or see https://opensource.org/licenses/MIT.

Development Process
--------

The master branch is meant to be stable. Development is normally done in separate branches. Tags are created to indicate new official, stable release versions of Desire Core.

The contribution workflow is described in CONTRIBUTING.md.

Testing
--------

Testing and code review is the bottleneck for development; we get more pull requests than we can review and test on short notice. Please be patient and help out by testing other people's pull requests, and remember this is a security-critical project where any mistake might cost people lots of money.

Automated Testing
--------

Developers are strongly encouraged to write unit tests for new code, and to submit new unit tests for old code. Unit tests can be compiled and run (assuming they weren't disabled in configure) with: make check

There are also regression and integration tests of the RPC interface, written in Python, that are run automatically on the build server. These tests can be run (if the test dependencies are installed) with: qa/pull-tester/rpc-tests.py

The Travis CI system makes sure that every pull request is built for Windows and Linux, OS X, and that unit and sanity tests are automatically run.

Manual Quality Assurance (QA) Testing
--------

Changes should be tested by somebody other than the developer who wrote the code. This is especially important for large or high-risk changes. It is useful to add a test plan to the pull request description if testing the changes is not straightforward.