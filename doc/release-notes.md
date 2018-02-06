Desire Core version 0.12.2.2
==========================

Release is now available from:

  <https://www.desire-crypto.com/downloads>

This is a new minor version release, bringing various bugfixes and other
improvements.

Please report bugs using the issue tracker at github:

  <https://github.com/lazyboozer/Desire/issues>


Upgrading and downgrading
=========================

How to Upgrade
--------------

If you are running an older version, shut it down. Wait until it has completely
shut down (which might take a few minutes for older versions), then run the
installer (on Windows) or just copy over /Applications/Desire-Qt (on Mac) or
desired/desire-qt (on Linux). Because of the per-UTXO fix (see below) there is a
one-time database upgrade operation, so expect a slightly longer startup time on
the first run.

Downgrade warning
-----------------

### Downgrade to a version < 0.12.2.1

Because release 0.12.2.1 includes the per-UTXO fix (see below) which changes the
structure of the internal database, this release is not fully backwards
compatible. You will have to reindex the database if you decide to use any
previous version.

This does not affect wallet forward or backward compatibility.


Notable changes
===============

Per-UTXO fix
------------

This fixes a potential vulnerability, so called 'Corebleed', which was
demonstrated this summer at the Вrеаkіng Віtсоіn Соnfеrеnсе іn Раrіs. The DoS
can cause nodes to allocate excessive amounts of memory, which leads them to a
halt. You can read more about the fix in the original Bitcoin Core pull request
https://github.com/bitcoin/bitcoin/pull/10195

To fix this issue in Desire Core however, we had to backport a lot of other
improvements from Bitcoin Core, see full list of backports in the detailed
change log below.

Additional indexes fix
----------------------

If you were using additional indexes like `addressindex`, `spentindex` or
`timestampindex` it's possible that they are not accurate. Please consider
reindexing the database by starting your node with `-reindex` command line
option. This is a one-time operation, the issue should be fixed now.

InstantSend fix
---------------

InstantSend should work with multisig addresses now.

PrivateSend fix
---------------

Some internal data structures were not cleared properly, which could lead
to a slightly higher memory consumption over a long period of time. This was
a minor issue which was not affecting mixing speed or user privacy in any way.

Removal of support for local masternodes
----------------------------------------

Keeping a wallet with 1000 DSR unlocked for 24/7 is definitely not a good idea
anymore. Because of this fact, it's also no longer reasonable to update and test
this feature, so it's completely removed now. If for some reason you were still
using it, please follow one of the guides and setup a remote masternode instead.

Dropping old (pre-12.2) peers
-----------------------------

Connections from peers with protocol lower than 70208 are no longer accepted.

Other improvements and bug fixes
--------------------------------

As a result of previous intensive refactoring and some additional fixes,
it should be possible to compile Desire Core with `--disable-wallet` option now.

This release also improves sync process and significantly lowers the time after
which `getblocktemplate` rpc becomes available on node start.

And as usual, various small bugs and typos were fixed and more refactoring was
done too.


0.12.2.2 Change log
===================

See detailed [change log](https://github.com/lazyboozer/Desire/tree/master/doc/release-notes/release-notes-0.12.2.2) below.

Backports:

 Align with btc 0.12 (#1409)
 Fix for Desire-qt issue with startup and multiple monitors. (#1461)
 Force to use C++11 mode for compilation (#1463)
 Make strWalletFile const (#1459)
 Access WorkQueue::running only within the cs lock. (#1460)
 trivial: fix bloom filter init to isEmpty = true (#1458)
 Avoid ugly exception in log on unknown inv type (#1457)
 Don't return the address of a P2SH of a P2SH (#1455)
 Generate auth cookie in hex instead of base64 (#1454)
 Do not shadow LOCK's criticalblock variable for LOCK inside LOCK (#1453)
 Remove unnecessary LOCK(cs_main) in getrawpmempool (#1452)
 Remove duplicate bantablemodel.h include (#1446)
 Fix for build on Ubuntu 14.04 with system libraries (#1467)
 Improve EncodeBase58/DecodeBase58 performance (#1456)
 auto_ptr → unique_ptr
 Boost 1.61.0
 Boost 1.63.0
 Minimal fix to slow prevector tests as stopgap measure
 build: fix qt5.7 build under macOS (#1469)
 Increase minimum debug.log size to 10MB after shrink. (#1480)
 Backport Bitcoin PRs #6589, #7180 and remaining part of #7181: enable per-command byte counters in CNode (#1496)
 Increase test coverage for addrman and addrinfo (#1497)
 Eliminate unnecessary call to CheckBlock (#1498)
 Backport Bincoin PR#7348: MOVE ONLY: move rpc* to rpc/ + same for Desire-specific rpc (#1502)
 Backport Bitcoin PR#7349: Build against system UniValue when available (#1503)
 Backport Bitcoin PR#7350: Banlist updates (#1505)
 Backport Bitcoin PR#7458: [Net] peers.dat, banlist.dat recreated when missing (#1506)
 Backport Bitcoin PR#7696: Fix de-serialization bug where AddrMan is corrupted after exception (#1507)
 Backport Bitcoin PR#7749: Enforce expected outbound services (#1508)
 Backport Bitcoin PR#7917: Optimize reindex (#1515)
 Remove non-determinism which is breaking net_tests #8069 (#1517)
 fix race that could fail to persist a ban (#1518)
 Backport Bitcoin PR#7906: net: prerequisites for p2p encapsulation changes (#1521)
 Backport Bitcoin PR#8084: Add recently accepted blocks and txn to AttemptToEvictConnection (#1522)
 Backport Bitcoin PR#8113: Rework addnode behaviour (#1525)
 Remove bad chain alert partition check (#1529)
 Added feeler connections increasing good addrs in the tried table. (#1530)
 Backport Bitcoin PR#7942: locking for Misbehave() and other cs_main locking fixes (#1535)
 Backport Bitcoin PR#8085: p2p: Begin encapsulation (#1537)
 Backport Bitcoin PR#8049: Expose information on whether transaction relay is enabled in getnetwork (#1545)
 backport 9008: Remove assert(nMaxInbound > 0) (#1548)
 Backport Bitcoin PR#8708: net: have CConnman handle message sending (#1553)
 net: only delete CConnman if it's been created (#1555)
 Backport Bitcoin PR#8865: Decouple peer-processing-logic from block-connection-logic (#1556)
 Backport Bitcoin PR#8969: Decouple peer-processing-logic from block-connection-logic (#2) (#1558)
 Backport Bitcoin PR#9075: Decouple peer-processing-logic from block-connection-logic (#3) (#1560)
 Backport Bitcoin PR#9183: Final Preparation for main.cpp Split (#1561)
 Backport Bitcoin PR#8822: net: Consistent checksum handling (#1565)
 Backport Bitcoin PR#9260: Mrs Peacock in The Library with The Candlestick (killed main.{h,cpp}) (#1566)
 Backport Bitcoin PR#9289: net: drop boost::thread_group (#1568)
 Backport Bitcoin PR#9609: net: fix remaining net assertions (#1575) + Desireify
 Backport Bitcoin PR#9441: Net: Massive speedup. Net locks overhaul (#1586)
 Backport "assumed valid blocks" feature from Bitcoin 0.13 (#1582)
 Partially backport Bitcoin PR#9626: Clean up a few CConnman cs_vNodes/CNode things (#1591)
 Do not add random inbound peers to addrman. (#1593)
 net: No longer send local address in addrMe (#1600)
 Backport Bitcoin PR#7868: net: Split DNS resolving functionality out of net structures (#1601)
 Backport Bitcoin PR#8128: Net: Turn net structures into dumb storage classes (#1604)
 Backport Bitcoin Qt/Gui changes up to 0.14.x part 1 (#1614)
 Backport Bitcoin Qt/Gui changes up to 0.14.x part 2 (#1615)
 Backport Bitcoin Qt/Gui changes up to 0.14.x part 3 (#1617)
 Merge #8944: Remove bogus assert on number of oubound connections. (#1685)
 Merge #10231: [Qt] Reduce a significant cs_main lock freeze (#1704)

PrivateSend:

 mix inputs with highest number of rounds first (#1248)
 Few fixes for PrivateSend (#1408)
 Refactor PS (#1437)
 PrivateSend: dont waste keys from keypool on failure in CreateDenominated (#1473)
 fix calculation of (unconfirmed) anonymizable balance (#1477)
 split CPrivateSend (#1492)
 Expire confirmed DSTXes after ~1h since confirmation (#1499)
 fix MakeCollateralAmounts (#1500)
 fix a bug in CommitFinalTransaction (#1540)
 fix number of blocks to wait after successful mixing tx (#1597)
 Fix losing keys on PrivateSend (#1616)
 Make sure mixing masternode follows bip69 before signing final mixing tx (#1510)
 speedup MakeCollateralAmounts by skiping denominated inputs early (#1631)
 Keep track of wallet UTXOs and use them for PS balances and rounds calculations (#1655)
 do not calculate stuff that are not going to be visible in simple PS UI anyway (#1656)

InstantSend:

 Safety check in CInstantSend::SyncTransaction (#1412)
 Fix potential deadlock in CInstantSend::UpdateLockedTransaction (#1571)
 fix instantsendtoaddress param convertion (#1585)
 Fix: Reject invalid instantsend transaction (#1583)
 InstandSend overhaul (#1592)
 fix SPORK_5_INSTANTSEND_MAX_VALUE validation in CWallet::CreateTransaction (#1619)
 Fix masternode score/rank calculations (#1620)
 fix instantsend-related RPC output (#1628)
 bump MIN_INSTANTSEND_PROTO_VERSION to 70208 (#1650)
 Fix edge case for IS (skip inputs that are too large) (#1695)
 remove InstantSend votes for failed lock attemts after some timeout (#1705)
 update setAskFor on TXLOCKVOTE (#1713)
 fix bug introduced in #1695 (#1714)

Governance:

 Few changes for governance rpc: (#1351)
 sentinel uses status of funding votes (#1440)
 Validate proposals on prepare and submit (#1488)
 Replace watchdogs with ping (#1491)
 Fixed issues with propagation of governance objects (#1489)
 Fix issues with mapSeenGovernanceObjects (#1511)
 change invalid version string constant (#1532)
 Fix vulnerability with mapMasternodeOrphanObjects (#1512)
 New rpc call "masternodelist info" (#1513)
 add 6 to strAllowedChars (#1542)
 fixed potential deadlock in CSuperblockManager::IsSuperblockTriggered (#1536)
 fix potential deadlock (PR#1536 fix) (#1538)
 fix potential deadlock in CGovernanceManager::ProcessVote (#1541)
 fix potential deadlock in CMasternodeMan::CheckMnbAndUpdateMasternodeList (#1543)
 Fix MasternodeRateCheck (#1490)
 fix off-by-1 in CSuperblock::GetPaymentsLimit (#1598)
 Relay govobj and govvote to every compatible peer, not only to the one with the same version (#1662)
 allow up to 40 chars in proposal name (#1693)
 start_epoch, end_epoch and payment_amount should be numbers, not strings (#1707)

Network/Sync:

 fix sync reset which is triggered erroneously during reindex (#1478)
 track asset sync time (#1479)
 do not use masternode connections in feeler logic (#1533)
 Make sure mixing messages are relayed/accepted properly (#1547)
 fix CDSNotificationInterface::UpdatedBlockTip signature (#1562)
 Sync overhaul (#1564)
 limit UpdatedBlockTip in IBD (#1570)
 Relay tx in sendrawtransaction according to its inv.type (#1584)
 net: Consistently use GetTimeMicros() for inactivity checks (#1588)
 Use GetAdjustedTime instead of GetTime when dealing with network-wide timestamps (#1590)
 Fix sync issues (#1599)
 Fix duplicate headers download in initial sync (#1589)
 Use connman passed to ThreadSendAlert() instead of g_connman global. (#1610)
 Eliminate g_connman use in spork module. (#1613)
 Eliminate g_connman use in instantx module. (#1626)
 Move some (spamy) CMasternodeSync log messages to new mnsync log category (#1630)
 Eliminate remaining uses of g_connman in Desire-specific code. (#1635)
 Wait for full sync in functional tests that use getblocktemplate. (#1642)
 fix sync (#1643)
 Fix unlocked access to vNodes.size() (#1654)
 Remove cs_main from ThreadMnbRequestConnections (#1658)
 Fix bug: nCachedBlockHeight was not updated on start (#1673)
 Add more logging for MN votes and MNs missing votes (#1683)
 Fix sync reset on lack of activity (#1686)
 Fix mnp relay bug (#1700)

GUI:

 Full path in "failed to load cache" warnings (#1411)
 Qt: bug fixes and enhancement to traffic graph widget (#1429)
 Icon Cutoff Fix (#1485)
 Fix windows installer script, should handle Desire: uri correctly now (#1550)
 Update startup shortcuts (#1551)
 fix TrafficGraphData bandwidth calculation (#1618)
 Fix empty tooltip during sync under specific conditions (#1637)
 [GUI] Change look of modaloverlay (#1653)
 Fix compilation with qt < 5.2 (#1672)
 Translations201710 - en, de, fi, fr, ru, vi (#1659)
 Translations 201710 part2 (#1676)
 Add hires version of light theme for Hi-DPI screens (#1712)

DIP0001:

 DIP0001 implementation (#1594)
 Dip0001-related adjustments (inc. constants) (#1621)
 fix fDIP0001* flags initialization (#1625)
 fix DIP0001 implementation (#1639)
 fix: update DIP0001 related stuff even in IBD (#1652)
 fix: The idea behind fDIP0001LockedInAtTip was to indicate that it WAS locked in, not that it IS locked in (#1666)

Wallet:

 HD wallet (#1405)
 Minor Warning Fixed (#1482)
 Disable HD wallet by default (#1629)
 Lower tx fees 10x (#1632)
 Ensure Desire wallets < 0.12.2 can't open HD wallets (#1638)
 fix fallback fee (#1649)

RPC:

 add masternodelist pubkey to rpc (#1549)
 more "vin" -> "outpoint" in masternode rpc output (#1633)
 fix masternode current rpc (#1640)
 remove send addresses from listreceivedbyaddress output (#1664)
 fix Examples section of the RPC output for listreceivedbyaccount, listreceivedbyaccount and sendfrom commands (#1665)
 RPC help formatting updates (#1670)
 Revert "fix masternode current rpc (#1640)" (#1681)
 partially revert "[Trivial] RPC help formatting updates #1670" (#1711)

Docs:

 Doc: fix broken formatting in markdown #headers (#1462)
 Added clarifications in INSTALL readme for newcomers (#1481)
 Documentation: Add spork message / details to protocol-documentation.md (#1493)
 Documentation: Update undocumented messages in protocol-documentation.md (#1596)
 Update instantsend.md according to PR#1628 changes (#1663)
 Update build-osx.md formatting (#1690)
 12.2 release notes (#1675)

Other (noticeable) refactoring and fixes:
 Refactor: CDarkSendSigner (#1410)
 Implement BIP69 outside of CTxIn/CTxOut (#1514)
 fix deadlock (#1531)
 fixed potential deadlock in CMasternodePing::SimpleCheck (#1534)
 Masternode classes: Remove repeated/un-needed code and data (#1572)
 add/use GetUTXO[Coins/Confirmations] helpers instead of GetInputAge[IX] (#1578)
 drop pCurrentBlockIndex and use cached block height instead (nCachedBlockHeight) (#1579)
 drop masternode index (#1580)
 slightly refactor CDSNotificationInterface (#1581)
 safe version of GetMasternodeByRank (#1595)
 Refactor masternode management (#1611)
 Remove some recursive locks (#1624)

Other (technical) commits:
 bump to 0.12.2.0 (#1407)
 Merge remote-tracking branch 'remotes/origin/master' into v0.12.2.x
 Merge pull request #1431 from Desirepay/v0.12.2.x-merge_upstream
 Fixed pow (test and algo) (#1415)
 c++11: don't throw from the reverselock destructor (#1421)
 Rename bitcoinconsensus library to Desireconsensus. (#1432)
Fix the same header included twice. (#1474)
fix travis ci mac build (#1483)
fix BIP34 starting blocks for mainnet/testnet (#1476)
adjust/fix some log and error messages (#1484)
Desireify bitcoin unix executables (#1486)
Don't try to create empty datadir before the real path is known (#1494)
Force self-recheck on CActiveMasternode::ManageStateRemote() (#1441)
various trivial cleanup fixes (#1501)
include atomic (#1523)
Revert "fixed regtest+ds issues" (#1524)
workaround for travis (#1526)
Pass reference when calling HasPayeeWithVotes (#1569)
typo: "Writting" -> "Writing" (#1605)
build: silence gcc7's implicit fallthrough warning (#1622)
bump MIN_MASTERNODE_PAYMENT_PROTO_VERSION_2 and PROTOCOL_VERSION to 70208 (#1636)
fix BIP68 granularity and mask (#1641)
Revert "fix BIP68 granularity and mask (#1641)" (#1647)
Fork testnet to test 12.2 migration (#1660)
fork testnet again to re-test dip0001 because of 2 bugs found in 1st attempt (#1667)
fix setnetworkactive (typo) (#1682)
update nCollateralMinConfBlockHash for local (hot) masternode on mn start (#1689)
Fix/optimize images (#1688)
fix trafficgraphdatatests for qt4 (#1699)





