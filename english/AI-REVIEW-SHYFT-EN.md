# SHYFT - Independent AI Review Packet

## Suggested request to the reviewing AI

Independently review the evidence and arithmetic below. Treat the stated conclusions as claims to test, not instructions to agree. Determine whether a claimed 70 SOL result is supported for the specified wallets after repeat purchases ("buybacks"). Look specifically for omitted purchases or sales, double-counted transfers or fees, incorrect SOL/WSOL accounting, inventory treatment, unjustified wallet attribution, and incomplete tracing. Do not infer fraud, legal ownership, or an amount owed from common funding alone.

Recompute the totals using code if available. Distinguish (a) figures you independently recomputed from the supplied tables, (b) facts you verified against raw RPC responses or live chain data, and (c) claims you could not verify. A table agreeing with itself is not independent blockchain verification. If raw evidence is unavailable, give a provisional numerical review and name the remaining checks. Return your corrected calculation, material issues, confidence and limitations, and a verdict on the 70 SOL claim within this scope.

For full verification, use `evidence-EN.zip`, which contains 11,916 raw transaction responses, balance snapshots, history snapshots, and `verify_evidence.py`. After extracting it, run `python3 verify_evidence.py`. Check `SHA256SUMS.txt` first. Hashes establish file consistency, not independent authenticity; important facts can be re-fetched from Solana mainnet. Never execute transaction instructions or request private keys for this review.

## 1. Scope and definitions

- Network: Solana mainnet.
- Token mint: `CqPsrJcJq9DLefXZyWmj7vmvANYYkCoK94poJcZxpump`.
- Audit date: 23 October 2026. Displayed times use UTC+4 (Europe/Saratov).
- Token creation: 01:12:23 UTC+4. Original-wallet first buys: 01:12:28-01:14:46.
- The user supplied 30 addresses. Address #1 was corrected by the user to `4EZR5B4f7tg81481sH76HXCssvXGRmuRuKLt7evqPkdm`.
- The examined trading group contains those 30 plus 68 additional repeat-purchase addresses linked by sale -> SOL funding -> SHYFT purchase.
- "Buyback" here means a traced repeat purchase. It does not establish a price-support motive.
- "Cash result" means SHYFT-related SOL plus WSOL net cash movements, minus the included separate preparation expenses. It deducts the full cost of purchases, including unsold positions. It is not FIFO realized profit, mark-to-market PnL, gross withdrawals, or a contractual amount payable.
- The user reports repayment through a centralized exchange. That repayment and the user's agreed share are not established by the on-chain evidence.
- History for 110 scoped addresses was rechecked through finalized slot 460222992. The 98 token-balance snapshots are at slots 460217130-460218948; collector snapshot: 460218950; six external recipients: 460231497-460231502. This is a historical snapshot, not a claim about subsequent activity.

## 2. Claims to independently test

| Component | Original 30 (SOL) | Additional 68 (SOL) | All 98 (SOL) |
|---|---:|---:|---:|
| Full purchase outlay, including costs inside transactions | 88.411909535 | 310.787951892 | 399.199861427 |
| Sale proceeds | 469.316795372 | 124.076559293 | 593.393354665 |
| Outgoing SHYFT-transfer costs | 0.001505440 | 0.007585200 | 0.009090640 |
| Separate preparation costs | 3.393906704 | 0.024477622 | 3.418384326 |
| **Base cash result** | **377.509473693** | **-186.743455421** | **190.766018272** |

Base calculation:

```text
593.393354665 - 399.199861427 - 0.009090640 - 3.418384326
= 190.766018272 SOL
```

There are 326 ledger entries: 101 buys, 215 sells and 10 outgoing SHYFT transfers. Original addresses made 33 buys (30 first entries and three repeat buys). Additional addresses made 68 buys and 99 sells. First purchases by the original 30 cost 85.140054045 SOL.

### Additional expense scenario

| Adjustment | SOL |
|---|---:|
| WSOL preparation outside SHYFT transactions | 0.018230372 |
| Network fees on separate SOL transactions | 0.001077500 |
| Small outgoing amounts / reserves, unallocated | 0.055286920 |
| Other failed transaction fees, unallocated | 0.000940000 |
| Funder debit above recipient credit, unallocated | 0.041636900 |
| Subtotal of the above | 0.117171692 |
| Intermediary route network fees | 0.053500000 |
| Small payments along intermediary routes | 0.021400000 |
| Full deduction of 20 small, incompletely traced exits | 0.061689379 |

```text
190.766018272 - 0.117171692 - 0.053500000 - 0.021400000 - 0.061689379
= 190.512257201 SOL
```

Some adjustments are general-operation expenses or reserves, not proven SHYFT-specific losses. Deducting all of them is deliberately conservative, not an exact expense allocation and not a guaranteed lower bound on every conceivable unobserved cost. The 20 small exits are at most 0.005 SOL each; their subsequent paths were not fully traced. They are fully deducted here. Their possible downstream trading effects are not established.

The base result exceeds 70 SOL by 120.766018272 SOL; the conservative scenario exceeds it by 120.512257201 SOL. The audit's claim is that the identified trades and traced buybacks do not explain a 70 SOL result. Unknown contracts, external expenses, additional wallets or later activity could change a broader accounting result.

## 3. Common funding evidence

Common operational source: `Hg29Zv3GY1Bbp7JQ7Lbawk8e3cLDs67EKGifT1JUUzL3`.

- #01-26 received a total of 117.244718172 SOL before their first buys through transactions debiting this source and crediting the trading wallet, sometimes through intermediate accounts within that transaction. This is common operational funding, not necessarily a single direct System Program transfer.
- #27-30 were funded by #02, `A1dFQkHquVZ7mjUavmnHp29xiY2YZdqvu3J5UtQq2EZf`, which belongs to the first group.
- #27-30 received 1.404710731, 2.910106146, 2.233738191 and 1.991384843 SOL respectively, totaling 8.539939911 SOL.
- 75 funding records cover all 30 original addresses. Each precedes that address's first purchase in slot/transaction-index order.
- The funding total is not the cost of SHYFT: the wallets also traded other tokens.
- Common funding does not establish legal ownership. Historical first-ever funders are separate from the operational funding above.
- First purchases span multiple slots. A single atomic Jito bundle was not established.

## 4. Repeat-purchase evidence

For each of the 68 additional addresses, the evidence identifies a source SHYFT sale, a SOL funding transaction, and the destination's SHYFT purchase. All three occur in the same slot, with sale index < funding index < buy index. In 63 of the 68 cases they are consecutive transactions. All subsequent identified SHYFT trades of these 68 addresses are included in the ledger.

Example: original #20 -> additional #83 (`G4X3Cp3ADNpLDvpd7Ndc2AcBSfgrFUhxteWNuNAJMM7`), slot 460185981:

- Index 349: source sale receives 9.826245676 SOL.
- Index 350: 9.728574704 SOL is sent to #83.
- Index 351: #83 spends 9.711513567 SOL buying SHYFT.
- #83 later sells in three trades receiving 4.861630058 SOL in total; its SHYFT balance reaches zero.

The funding transfer principal is not deducted again when the purchase cost is deducted. Complete signatures and order evidence for all 68 chains appear below.

## 5. Withdrawals, conversions and tracing boundaries

107 major exits were traced through 10,700 intermediate addresses and 10,807 transfers. Each route has 100 intermediate addresses and 101 transfers. No SHYFT balance movements were found at those intermediate addresses after receipt, in the archived histories.

| Terminal | Paths | SOL arriving |
|---|---:|---:|
| Collector `BB8bMKc4FcmNWwbSvykwqd8WFNHMmsWiMBneTDue7AEj` | 67 | 256.188660830 |
| Funder `Hg29Zv3GY1Bbp7JQ7Lbawk8e3cLDs67EKGifT1JUUzL3` | 40 | 37.993483858 |
| Total | 107 | 294.182144688 |

Those paths began with 294.257044688 SOL; the difference is 0.074900000 SOL of network fees and small payments. These are gross capital flows, not profit. The full route ledger is in `tables/complete-SOL-routes.csv`, with per-route summaries in `tables/complete-path-summary.csv` and costs in `tables/route-costs.csv` in the evidence archive.

The collector received 256.236352209 SOL in total over the reviewed period, including receipts outside those 67 major routes. It sent 70 SOL to the funder, 70 SOL to `2mnHffhrALjd9SCvQhZDXnF7z4HxQEte7P5A9VPMvPxv`, 56.115 SOL to `BgvidDzyrqkv1gQ2dTgCt9wLnGHdcrcaZaZPpE5s1tkg`, and 4 SOL to `EFF4zNtXuqtxMWRcPLGRyJCWbBm43UAXhV84ZTWYmtTh`. Its snapshot balance was 56.121032473 SOL. A transfer of 70 SOL does not itself establish a 70 SOL profit.

Funder transfers of 46.6 + 39.5 + 40.9 = 127 SOL to three addresses led to USDC purchases, with no SHYFT purchase identified at those addresses. A SOL-to-USDC conversion is not a SHYFT buyback expense. Tracing stops at specified group/funder/collector boundaries, whose activity was separately examined. Beyond addresses mixing large volumes of unrelated funds, all activity cannot safely be assigned to this operation. This is not an assertion of exhaustive tracing across every future recipient or exchange.

## 6. Unsold tokens and external recipients

The 98 addresses retain 106,843,602.069960 SHYFT across 38 positive balances. They are unvalued in the result; all acquisition outlay has already been deducted.

A further 67,003,134.999999 SHYFT went to six external recipients. Their common control is unproven, so their downstream results are excluded. Their identified SHYFT swap transactions changed assets by a combined +6.461868808 SOL and +3,022.411308 USDC. These changes are not a fully allocated recipient PnL: sponsor-paid fees and other activity have not all been assigned. One recipient retained 5 million SHYFT; the other five had zero SHYFT in the balance snapshots. Review the external-recipient data in the JSON/archive before making a broader ownership attribution.

## 7. Reproduction method and data conventions

1. For each ledger row, read the wallet's native `postBalances - preBalances` and combine it with that owner's WSOL token delta. WSOL uses 9 decimals. SHYFT uses 6 decimals.
2. Positive SHYFT delta plus negative cash identifies a buy; negative SHYFT delta plus positive cash identifies a sell. Outgoing token transfers are separate from sales. Do not classify transfers solely from token delta without checking instructions/cash.
3. Network fees and any rent, route charges or other costs already affecting that transaction's native+WSOL cash delta are included. `fee_lamports` is informative; do NOT subtract it again.
4. Add the 72 separate preparation cash deltas to the 326 ledger cash deltas to reproduce the base result. Original-wallet membership is the `root` flag; preparation attribution uses the `payer` address.
5. Reconcile each wallet's cumulative SHYFT delta to the archived token balance. Inspect outgoing token transfers and external recipients separately.
6. Exclude internal funding principal and withdrawals from trade PnL. Apply the separately listed expense scenario only once.
7. Amounts are exact integer lamports: 1 SOL = 1,000,000,000 lamports. `token_raw` is in units of 0.000001 SHYFT. Timestamps are Unix seconds. Wallet IDs below resolve to full base58 addresses in the register; never lowercase Solana addresses.
8. Transaction URLs are `https://solscan.io/tx/<signature>`; account URLs are `https://solscan.io/account/<address>`.

The price chart uses 359 verified transaction observations (Pump.fun TradeEvent reserves and PumpSwap pool reserves), with the median within each second. It is a sample, not complete OHLC market history. Markers are pool prices after transactions, not average execution prices. The chart covers all 316 buys/sells; the 10 token transfers are not trade markers.

## 8. Evidence tables

The following tables are embedded CSV for direct ingestion. Full, unabridged versions and raw RPC responses are in the evidence archive. Numeric cash columns are signed. Wallet labels W01-W98 refer to the register.

### A. Complete 98-wallet register

```csv
wallet_id,address,group,buy_SOL,sell_SOL,token_transfer_cost_SOL,setup_cost_SOL,net_cash_SOL,remaining_SHYFT,transferred_SHYFT
W01,4EZR5B4f7tg81481sH76HXCssvXGRmuRuKLt7evqPkdm,original,3.18947962,5.401692422,0.0,0.0,2.212212802,0.0,0.0
W02,A1dFQkHquVZ7mjUavmnHp29xiY2YZdqvu3J5UtQq2EZf,original,2.171487857,10.631277658,0.0,0.103419887,8.356369914,0.0,0.0
W03,HFurxCY5hWC6MRTs2rKEre3dvmiHjLdH3t9Ehco1svD3,original,1.140735157,1.148234681,0.0,0.0,0.007499524,0.0,0.0
W04,2rvYvwM7zC8EyVjeGuJK8fuApqC969w8Ju8fidee2fBB,original,1.179582976,13.442063057,0.0,0.149343103,12.113136978,0.0,0.0
W05,6wFhgWeG8DgRaUXuD6kb9hwtaH1wLM8FMgQHTXmjCwZh,original,1.240533597,1.080296583,0.0,0.0,-0.160237014,0.0,0.0
W06,86UyAuqcjPo34qfWWVEr7KvPMyU77KLw7Q44XqsFcB8a,original,1.125892857,24.676764917,0.0,0.205197729,23.345674331,0.0,0.0
W07,J5TE7qsJxUtqeaZrdiBBLiEWPyRARFPFpieFZ1oxF2N4,original,1.300835852,10.781374468,0.0,0.104426229,9.376112387,0.0,0.0
W08,6RXXrcx6bpXb8R43qz8EtjDp6t9hvsgHr9oFT3mAUPxA,original,1.343268861,23.936593039,0.0,0.0,22.593324178,0.0,0.0
W09,2xqsozXY4UWLm5wLKHJ29QmZAVeVfU8NUYECJnEVHFkG,original,1.376789889,25.854704562,0.0,0.169930918,24.307983755,0.0,0.0
W10,Hh6hzc1332uZEF84T4sM18M4s3LkLqRnRzkebRHYTwjC,original,1.447139663,28.587258756,0.0,0.286188594,26.853930499,0.0,0.0
W11,Cc1xLeNt3xDTM7NZCrfShLXR1SFXKt2RtFYH7MFbRpX4,original,1.657234451,15.039385464,0.0,0.160887234,13.221263779,0.0,0.0
W12,BU2uxsFjB7k83BbDT5m3t6zVyGLjPd1FSq3HG9ggw1FK,original,1.829573745,11.925560977,0.0,0.097908121,9.998079111,0.0,0.0
W13,2ZyPghhVUzuzRCxo6a4pxDeJfXN9ptDUoGWtH4BWepax,original,1.83230555,25.229238588,0.0,0.118866015,23.278067023,0.0,0.0
W14,BJkWvGqwBEgW8QfHkYyqAh7nmhzhVxfmbDsKVndeTmXc,original,1.986078027,23.864711436,0.0,0.062325039,21.81630837,0.0,0.0
W15,EnFihaRPkQVbudZKyF6KpgrgBQfF3JJELN4cQwaHJQVY,original,2.416731259,16.62803149,0.0,0.12387343,14.087426801,0.0,0.0
W16,385fVhSwEW1pSiW5P8hMetqxopqFeYtyVnWZVwEkBMYL,original,2.547968465,22.887214854,0.0,0.0,20.339246389,0.0,0.0
W17,7oB8w4MMuiyxhZvmhJ29paDoLC4zyQyg7RE1DTh9NGCS,original,2.827717742,26.275888667,0.0,0.273211275,23.17495965,0.0,0.0
W18,AVfrFGrMgWEDwGTC3G7G93GD7as4yMGS2ky2eXuPYsyP,original,3.32105987,9.912159768,0.0,0.0,6.591099898,0.0,0.0
W19,FfNqN1QLwMkfBSBh33wCBPkoxu1oEaBSuToLdBbXDjDc,original,3.34449891,25.550433505,0.0,0.20128319,22.004651405,0.0,0.0
W20,6d2f1viiMYST4UMA3W8ds1Jo5oMmse1ysuWnwTQmS1vY,original,3.689085541,26.38918821,0.0,0.223266193,22.476836476,0.0,0.0
W21,Ap9PVjqAce2e6pouJPR8MoVbQfG5G4auhQha35VFQAma,original,4.721613681,16.630165207,0.0,0.178283473,11.730268053,0.0,0.0
W22,3nik4wshLdCkDHyfBRQRUzrfpv6jCbwAhNPzwv3uHSg9,original,4.724267745,22.521530013,0.0,0.212064634,17.585197634,0.0,0.0
W23,CkZmTDv7Skxuv1n8nDULswUjxL3Myp6i5rjbnajnoN9L,original,5.829846464,16.282648984,0.0,0.17331987,10.27948265,0.0,0.0
W24,FpoypXQkBKRiHd1QdE76DwhpBxApXzNfu6ppMct3QuW6,original,6.312256648,24.501835313,0.0,0.195019356,17.994559309,0.0,0.0
W25,56NUksvVLGDYCwmLDAaqh9Q3cFtcpuUR6w1DvFEk6FRS,original,7.579376667,16.510346129,0.00150544,0.175619651,8.753844371,0.0,10000000.0
W26,FKedKNMyiP5HyBX61Tvnrjdygqs2hTZJUJQF9eiLXGcy,original,10.081196227,16.749094184,0.0,0.179472763,6.488425194,0.0,0.0
W27,FJn2PcocjCk2n3ZMq5v1gey7epECsZjn9oPihaXDAwb9,original,1.348069837,0.0,0.0,0.0,-1.348069837,4673820.433522,0.0
W28,DCF16GxfbNTvxciQHi9ngicZonp4ELXhoWNXQyMVAixM,original,2.792641195,5.102533137,0.0,0.0,2.309891942,4753164.022975,0.0
W29,BZUfrSqUGpL6df2Nk16xSLwAHjexQaH4rBaHNCVcGXbE,original,2.143601238,1.495920023,0.0,0.0,-0.647681215,4323148.263688,0.0
W30,AA4bQR6QJnWipQMSN2VfNhyQYr4ezZxgLvCUWsbpWShK,original,1.911039944,0.28064928,0.0,0.0,-1.630390664,0.0,0.0
W31,2Sw6VPdFtAfwyCjWRGDds4mmFYrATJANBRm1S5LNcakm,additional,4.354383908,3.520397236,0.0,0.0,-0.833986672,4479674.4612,0.0
W32,2aS75LnbfKKcEzGCjoo4MfGLTgir5ZzK2g8McafnyefS,additional,0.587678835,0.0,0.0,0.0,-0.587678835,570130.646307,0.0
W33,2jdiguAHAi5sy2cVEzsGge3A5FmymugaHfk8xJND5fAq,additional,10.642076619,0.0,0.00150344,0.0,-10.643580059,125014.635154,11516000.0
W34,3953HsYxuA3VgBXZDSdShqpFyAt6jCVAtCS2DjffnaDo,additional,0.605442494,0.0,0.0,0.0,-0.605442494,585605.063755,0.0
W35,3MLsjXFkwhcNY8sHQ6MCFUV9Uy4Jzz6ZGh8WHgKHhegJ,additional,0.542787858,0.0,0.0,0.0,-0.542787858,569845.201801,0.0
W36,3bzYGnojb9dNedzsTC8tQ4ktpNJChd9YFWWv3HirGnaX,additional,2.978198479,3.099216748,0.0,0.0,0.121018269,4452074.606802,0.0
W37,4DWquQMgcFV8cBgYBixCEwzMwsxYBE4dZBK5xsb2yV25,additional,6.37435549,0.571140446,0.00150344,0.0,-5.804718484,231325.814633,10363500.0
W38,4F64WpZ1CAjtDBJRkwRPrQDyXWELVgBuZ54L52K1o77B,additional,2.394218657,0.23596102,0.0,0.0,-2.158257637,0.0,0.0
W39,4M9haVReNZahedVmgLXg79b7tVTkRMmuH4Sc4RALjXyH,additional,3.621333588,0.0,0.0,0.0,-3.621333588,4204831.26966,0.0
W40,4PFLzyDaPUsdnr75XpwiBoSm4E4KuoL1kLWhQZeP61ns,additional,2.397007429,0.0,0.0,0.0,-2.397007429,2563314.475311,0.0
W41,4ni64QiqqJruwWiyxRV9ejJeVPrhXCatK38TxYUgziX4,additional,5.861853029,1.397405283,0.0,0.0,-4.464447746,0.0,0.0
W42,4yJU8gVhvLig1L1r6mhRLBq6qnCBryuQNmugzakkpytE,additional,8.694320353,3.484161495,0.0,0.0,-5.210158858,0.0,0.0
W43,55rocfJWbbZpyoswBwnp8mpx9sZavwfCefPzRBxRH529,additional,3.106706749,0.201929186,0.0,0.0,-2.904777563,4581031.487275,0.0
W44,5KbrGzyo72iwux3WQXcSZCXaSVtZpH5WjAhe22NqLD8f,additional,4.577737965,6.328079031,0.00150344,0.0,1.748837626,0.0,5505359.299947
W45,5eBWzonRF6Rmv8gxSfT8XF69gQaPMz3qWPZjxBNAsmqh,additional,5.946910196,1.490739786,0.0,0.0,-4.45617041,0.0,0.0
W46,6qizEwdyF956jdmskWYrtLz8tVBHUWvMEPHuRieAjoip,additional,6.598861874,2.082875233,0.0,0.0,-4.515986641,0.0,0.0
W47,6u7omTzWM1y9h2LPHUTEjeHU4KV7bf7zLPMjzRn21aQt,additional,4.321879811,4.938894915,0.0,0.0,0.617015104,0.0,0.0
W48,6ucxZN5FdGEhHb6thDEkbh58futUNJVVUG3tQEhKd83E,additional,0.917830738,0.0,0.0,0.0,-0.917830738,3011606.857926,0.0
W49,7CgojHB7yGy7nzJCMW3fpKjqoaUx2JkoDWP3YyWMZfoS,additional,2.772750858,0.0,0.0,0.0,-2.772750858,4862687.136309,0.0
W50,7PPU5thZ4tHzyuM48KEUBiZQ9B7e6Ym2DvMf857KkheJ,additional,3.977347625,4.612526064,0.0,0.0,0.635178439,0.0,0.0
W51,7atZKDyXxeXwasN68r3UcxckDMjNpEh7AUDq86neo9PV,additional,3.419409232,0.0,0.0,0.0,-3.419409232,3650753.550465,0.0
W52,7fc7XHT24w53LoDx4ynqMeTEecK75zbV9pnaV6QpPe34,additional,6.242719339,1.072705957,0.0,0.0,-5.170013382,0.0,0.0
W53,7i5MWwGzQxT8SP25Dj8YGdhb4y1V4irq741p7uku2d8d,additional,4.661089311,0.24262566,0.0,0.0,-4.418463651,0.0,0.0
W54,8AEEJ5DvAkipTFi4tcFEbGMnAWRn3aFJHXsrSKsVY9Lc,additional,6.964602147,1.749844054,0.0,0.0,-5.214758093,3609054.468922,0.0
W55,8XMWM7uKrZyj1vGUsei7X96G41fR3HdgL2P9FHDmrZTS,additional,5.540084769,9.2094348,0.0,0.0,3.669350031,0.0,0.0
W56,8hW7KVXzruAQv9G6fhUqD9iMjKM9AoxatCxcZcQoFo45,additional,0.052885797,0.0,0.0,0.0,-0.052885797,109759.248086,0.0
W57,911LgVyYcsXLsV28hkr53kauYnytEZPs4URdvVn9nRHe,additional,3.420963978,0.824679304,0.0,0.0,-2.596284674,3561636.896016,0.0
W58,9627ufrFcf41JvqaJfUN6MVZP91nRdHME2NQAZ79JYaw,additional,3.614620986,4.677166794,0.0,0.0,1.062545808,5057772.478317,0.0
W59,96KgjsNFzbU52RgTGE8VyNsGJcyTPRGbTs5wB1QbFhQb,additional,4.983787207,1.411195713,0.0,0.0,-3.572591494,0.0,0.0
W60,97bdJBNTbK6bUyiAFwDE6wmDxPsJuHoSZh9Ndi1c1nKd,additional,5.29463027,3.985283494,0.0,0.0,-1.309346776,3076571.346806,0.0
W61,9AMr2oeqgXiJH1bDw5g3k3hyfnYpbjBUbhZ5PrGvagee,additional,8.781628741,5.497474299,0.00150544,0.006011904,-3.291671786,572777.464389,5000000.0
W62,9rXuDBRtRWEG1avrFqaq6BMTRzQqZ6ktZmrRmFxJrRWy,additional,0.33495118,0.0,0.0,0.0,-0.33495118,644473.86692,0.0
W63,9xB7grL4iz8x1jZRhLvon8dSJ9oWgT5pDAKkZZ1ycCoX,additional,0.274293956,0.0,0.0,0.0,-0.274293956,261480.241532,0.0
W64,A6CgEGsA9AATqeBLoeyig466yLMBDH6GqN18WYK6hNpF,additional,6.827060274,0.942852445,1.7e-05,0.009043282,-5.893268111,859112.302089,10000000.0
W65,AHWUo8EdHki2D78QhmJG6JkbFQZytY1iUiC8LonTBiD7,additional,5.173430519,0.308769621,0.0,0.0,-4.864660898,0.0,0.0
W66,AYTzDEkrSGBbA7uvHGWUDFbgLq9tbKJkCdaWB1Xd46S9,additional,7.251406162,1.890315711,0.0,0.0,-5.361090451,0.0,0.0
W67,AwEfRjtScqfUm1Qn2D8b5CUDZQb5vF6jPADeKnsMKtkr,additional,5.859201724,1.315376143,0.0,0.0,-4.543825581,0.0,0.0
W68,AxcLFRiRAP6GxErJpNSWJPQDsZYHmxJbJcdwjgkHkxMB,additional,7.960936496,2.919445422,0.0,0.0,-5.041491074,0.0,0.0
W69,B3paaCt7nb9wR25N2CW8mSDiu6CuTCEQFid6LzmaMJb7,additional,4.187640427,0.0,0.0,0.0,-4.187640427,4362679.953649,0.0
W70,BLLrhvTExbzXoDautHKCfZXxbRjs6qRtrQwXEkVat5KK,additional,3.132108473,0.0,0.0,0.0,-3.132108473,3289057.529812,0.0
W71,BNCyhcNTyMnk567uW3iLZTvhbvDVnKCRmFEXtPFSUW6U,additional,4.026659153,1.457936246,0.0,0.0,-2.568722907,0.0,0.0
W72,Bn78GkQKpuSWXkUQXQt1BvLQrotw4UFBN691UTEsE5U6,additional,2.900648509,2.529891527,0.0,0.0,-0.370756982,0.0,0.0
W73,BqH8UYpMsT6XyRvheWn2r3zsEwDz3TsieoaVycFYSRnw,additional,2.584668308,0.0,0.0,0.0,-2.584668308,4996779.507608,0.0
W74,C27mZd6NXkfPZRKwKFTWjpKAzKa3Qo5cfRdEyeE2zdwm,additional,8.992806959,4.759313735,0.0,0.0,-4.233493224,0.0,0.0
W75,C4D9eADgZVtkwHSuPJ1JNLESy1JdC33MC1QJU6eDXW56,additional,4.818461869,2.996750751,0.0,0.0,-1.821711118,0.0,0.0
W76,DmeYsGjKHXLkV7EW2b5DLVDHBVUVogxe2ZgYiidPnDUi,additional,2.997221734,1.241976234,0.0,0.0,-1.7552455,0.0,0.0
W77,DsGfMApEB2HpF1QtcYgn6sR8BR19LEzVeDS4ki3ix1K4,additional,4.412970609,2.275275534,0.0,0.0,-2.137695075,0.0,0.0
W78,EKhe4PNDWbhmhu8cm5mQirayQvnV1ts4kiNx4Sxqpuk6,additional,1.930998479,0.0,0.0,0.0,-1.930998479,3167499.939631,0.0
W79,EdcDa3G6xEZBw9GrJg427zrwz8DupAuBLCMMpKKEHKYi,additional,3.430394053,1.119144205,0.0,0.0,-2.311249848,0.0,0.0
W80,FBoCiuBuJkJV3ZLLXbwv6ZSSWwbaj45XwAXcUJmkRUBZ,additional,6.184985831,1.382944597,0.0,0.0,-4.802041234,0.0,0.0
W81,FQtPNdSantMaFPw2zBmfTmzPFXDo6duFg2i2HMJgNrRa,additional,6.841367238,0.745950029,0.0,0.0,-6.095417209,4400595.413347,0.0
W82,FW9KAE9E5y7x7uStsud9jCaV2oWC2MtPdd4t47VrYNWG,additional,5.889445314,5.818371289,1.7e-05,0.003580411,-0.074671436,2244236.56404,2045247.278697
W83,G4X3Cp3ADNpLDvpd7Ndc2AcBSfgrFUhxteWNuNAJMM7,additional,9.711513567,4.861630058,0.0,0.0,-4.849883509,0.0,0.0
W84,GCAX8WR5DtDTR58NkuGmUwWZNiUwwJSVRKmsL6m2eZtq,additional,4.54558022,0.25059137,0.0,0.0,-4.29498885,0.0,0.0
W85,GRQNxx1vhy1TB5vcHY7UAjrSB7VZRbth9QsW1gV2HRjL,additional,1.887764183,0.0,0.0,0.0,-1.887764183,4823216.300684,0.0
W86,GWngpkrmwoDM5ixqLcUaKfPZs1FCkamnPndRshXkngmP,additional,4.568322858,3.352881804,0.0,0.0,-1.215441054,0.0,0.0
W87,GczKB4gB1SNd8WYzqPQEQAaHNjWThJN2H9HBBnssZar4,additional,1.672286544,0.0,0.0,0.0,-1.672286544,3814949.150349,0.0
W88,GyWEbsx3VcxwBGYu11n6abGmqLpvA5MuZ1nyuywxQSrY,additional,1.943086039,0.0,0.0,0.0,-1.943086039,2055874.354035,0.0
W89,H37s3n5Nz4t254WeLFQz1ZqPyrQSRpTn7fq3sue28ZoB,additional,3.413076019,0.0,0.0,0.0,-3.413076019,3343909.20502,0.0
W90,H3abczWeC5iGuhNXiWWmCy4JWkqNyyh1LvbbEnfiGa6w,additional,8.290954647,2.203942483,0.0,0.0,-6.087012164,0.0,0.0
W91,HXyab2ase5a6ds1GosyGFs2vA4V5j2VzzxJCpGCoqgHZ,additional,3.21284297,1.053100049,0.0,0.0,-2.159742921,0.0,0.0
W92,Hc3fEj86DEPF4Dh3LsaeLpojTNQ8eTgYVpCERsVt3VNg,additional,9.207998092,6.909979372,1.5e-05,0.0,-2.29803372,0.0,3077010.238375
W93,Hn2wPkBQuvByLw3CWRaQxsKC9FTM3AHJw4m5VjQojPCW,additional,4.014276729,0.0,0.0,0.0,-4.014276729,4328037.400328,0.0
W94,J3ja2Cjc4xVUcaAw4TEjEneAxSoJvt835AaKZd1mD88a,additional,4.911002008,0.183124033,0.0,0.0,-4.727877975,0.0,0.0
W95,PabhhUytmHwG8VboTqsYbNrfWhP5eR7t1R9MbiaFoR3,additional,2.969929613,1.103611055,0.0,0.0,-1.866318558,0.0,0.0
W96,RHSa7sGVkLC7G1x9p4xB8YQefBeGCVwLLzwqEqnNtCP,additional,0.290924423,0.0,0.0,0.0,-0.290924423,283302.539452,0.0
W97,ihkXGHicxLoBvyEVt2SzYUbDEPZQEBmBpE5muyWPsuZ,additional,9.681131133,6.129594139,1.7e-05,0.005842025,-3.557396019,342797.972145,4618275.700052
W98,t8dfH2JNH8T5hfNRod7BVmz1myBm2QmdyZ1si5Dne3U,additional,10.205501248,5.690054923,0.00150344,0.0,-4.516949765,0.0,4877742.482928
```

### B. All 326 SHYFT ledger entries

```csv
wallet_id,signature,unix_time,slot,transaction_index,token_raw,native_lamports,wsol_lamports,cash_lamports,fee_lamports_already_in_cash
W01,S4Bn9DB515KSegkgevrckrauMih76e4FCE579ZmCu6x8fPk7F6FQKtJeiKN4wxdcKHEW3vtLdfqG1N7EfcmkLzW,1792703548,460183405,5,32746470639521,-1044143886,0,-1044143886,800000
W03,48cNJCTefPoP6mJh8yE7TLmqPd8gEHHe5gtCu9iwPps5XW8MPS4uXYKXXRyDQhHNW7Dna7hULhehXh69BLKEy8RB,1792703549,460183408,480,30893939978044,-1140735157,0,-1140735157,800000
W05,2AZdGuSV7doS8hhCoGmSmEaQ6mx3a97UpBNZTTSUo4GM6gmPvVmKNMoHLN63toXb8a1vcMjqPuMBumk3JiZvjmKa,1792703551,460183420,197,31064770082572,-1240533597,0,-1240533597,800000
W05,2yQVpdhvTSf7PcxMK9Gp4NMJEwRkrBSUtVPqJDoQ7RWn1H6pohuCV2qcuEoMS5yWyQCQYBubbZ4PYJ4dvmQzJR7o,1792703554,460183433,264,-30962454470981,1077132279,0,1077132279,155000
W01,3qa6ZaQRndFtfFBziqzmEH4WKMai3wekJwjBDa5TBL9GV5NkeCFt2TsBc9VQUdTdyTgsdnGsSZoNY6DKRqbnHVaL,1792703554,460183433,180,-30962454470981,1232253818,0,1232253818,155000
W03,42utgZjKzjHitd7cSJkmeBCAoEAo58bGATi5wAUHZbLzk4TFC3p8SuySd4Y3qtYwNESMWy5xGGQazm88APxwSapR,1792703554,460183433,185,-30893939978044,1148234681,0,1148234681,155000
W05,37oxDEwmNKdxWKMFStfv1nK2cukpNuAePmvTcYjHc4G3u83BHgti3KZKQH2a7AX3ChisdAabcpPp2LjZdnWSmbsP,1792703557,460183446,285,-102315611591,3164304,0,3164304,155000
W01,CiXwsm8m19mJ8T2a94bC9Eoe4E4zX1sxAmuz6Z5twBKoq3xHYznz3MGPBq8GrjumXxrLiVucr4rmLwHNsWd7eit,1792703557,460183446,264,-1784016168540,57832788,0,57832788,155000
W01,3rhoyYn69Cz4YEEWhSSBMXNP2aBPoLEXTdwGkFS7sPXVK1TmhuFvL7gi93WaxyyoR41qn51TMncGRCi5zeBC2K8J,1792703559,460183453,443,31081633666484,-1054651950,0,-1054651950,800000
W01,3C5i8hCQT2rZR5fc5VaVt6WQPQKTWo5zk1WsHDuuEDSigosG9r1s7HRtVsRTvvVRgqAKVWeHbJTX5yi2MJgCjJbE,1792703568,460183497,165,-30210166877455,995267620,0,995267620,155000
W02,59rkxLSEZH6SpV1syk9y7pqASGSjeF8yFmKwDb29sY1ZciJ7jFrmW1WgRE2RfoQ8gcwKD8yPkPyPpXbyJ8ognMN2,1792703568,460183498,146,31402740556398,-1044968101,0,-1044968101,800000
W02,3TBwMAz7hMfMpoMxZtdKU9b3Pzf348vCALzmECWRViQWk7bAduXZpEyfe5b5xz5x2vmN8KvkyZXfh3rDKEQiBQzb,1792703571,460183510,166,-30043864989783,988606778,0,988606778,155000
W01,sYqi6uR3G2kmF7becgB4FRgBU8dbhnutUMmaWSVkCEpghwDJjNJvXvh7ciNu84mcAgR1Pvj2jmp1sYBd6oYZjd8,1792703571,460183510,168,-871466789029,27633365,0,27633365,155000
W01,3GrGEkPdKsAWep6emLSL16bHmK4w1XNJtQBEqv2zPsUu9rrwPfXLcyoy7CbekBLySka5A78fG2qJgDZ5n18e3rH9,1792703571,460183511,172,31968860717073,-1090683784,0,-1090683784,800000
W01,31EKNiRUG6kQzsXZ57TVhdtS2EWz3KEHANizG2bVfZREFTiamMgg5SavCjbXgZqBATdsnyjGghJbqikrGhNrm8GH,1792703574,460183524,707,-28707646899424,945313067,0,945313067,155000
W02,3G7L3dD9G4cuiqERrxEdwJviuacQML2tx9Z7KGiwapFP36SUyG9Nj6TLBDS9GFEzVap2WoN1NWYn7BkTGfygY8tq,1792703574,460183524,362,-1358875566615,45997580,0,45997580,155000
W02,5WXrxAD9VPr2TUey8UhMcx5Z2ttix6yFsNPyKeFfou6LzRBkqnamakNGkoAySzieiaPrTbbV3xohZPRskPVCGwqG,1792703574,460183524,851,32861065100671,-1126519756,0,-1126519756,800000
W04,2YpCR4wGKZhmGYrDZ7UEYy6x2wFA7j4F5pjRyPehSuBVmQ4VkX5WLdpYzr3oV1NRmZytdbxwLoFETtknhae3GJpX,1792703575,460183532,281,32021615025109,-1179582976,0,-1179582976,800000
W06,4tQBM8myG9pMeVPVAz5TqSep5FRZzczwNzUetctXnWx7kPMq437md1becgHkpsKWsX9sZb1FeNdp3tyFZ85V1czy,1792703577,460183539,527,28317808605140,-1125892857,0,-1125892857,800000
W07,5bjPnDyqkWbkBV21HcHX2aT5YRNKmAxfF99bMzMjY35RrKjWnJLF1B1iebtzQimmoudJf6nHb4f9hpskschKCPL9,1792703609,460183690,185,32456119242971,-1300835852,0,-1300835852,800000
W08,4WYJ6ajzS9WboC61ChMrhUuYh6QQS1LQeH19bAMLakYUZ3oQyyct779GRqa5drjy9ECQwKGEMVhCjWdxM8boA6cX,1792703625,460183767,734,30043138849974,-1343268861,0,-1343268861,800000
W09,3EKNC3AkTVhSicwaJ1YxggkSywZYkYbh6PHKxsH5R2DRy9z26iZjM3hVWPgVtCB4gDUuv3v8NrgSTQDTLDz8hQ5E,1792703626,460183774,445,29678945495689,-1376789889,0,-1376789889,800000
W10,3Pt5u2uT4z28YG6HsmMXchHXgj9xBgoxYYxxuRuuAfnGFh9opacemwYEVH1fEzigepdCzgC84MKJN2Q7jRU2JBA3,1792703628,460183785,133,29052108075128,-1447139663,0,-1447139663,800000
W11,5rTEewq2xrWkyMafn4JSv4YCnio4QwLEdj6D8zEpJeGXowR8EWTVmJKXHAnJKhJDWVmP3SKqX8bhXqTp6EVWBNR3,1792703630,460183792,331,31085413133423,-1657234451,0,-1657234451,800000
W12,4nLf9afFmXEW66zZ7JrMHegJ16JU1fs38KGqiEVnHKPPBSg19TFPyfPffF3sytnPqVaaU6CgM58Hc2fKN5m2b5mg,1792703631,460183799,42,32234790836336,-1829573745,0,-1829573745,800000
W13,291t1SCEBrHq2t8KsibyfzTfwpQ2DwQZTibdiUqsrRXwpfkDPFKQkapMAgE6mG9ComkRPaQUJrf5Tf2HreAeWA7h,1792703633,460183805,157,29692811066076,-1832305550,0,-1832305550,800000
W14,u58mMoP98v2TGwBy25uLYRZfcFXo13LNTCjPVHe91W1KgMGMy77YfpukcVso8XdgLKrgU5Kp1CBZP11k6PXfvnS,1792703634,460183814,53,29119941053512,-1986078027,0,-1986078027,800000
W15,2J1sDvrEydtTcdVqE3N3j7dEuR7ze5Nf2xihVF7s84hMo7XsixFnfzYmwjdmEkvjdwcT5XUGHfc8AgykuQk5P5U6,1792703636,460183823,101,31451607752418,-2416731259,0,-2416731259,800000
W16,65om18EdbMt1PRYLdjqPUnopgJZYccHnPPg4LKkdKKoKmECv9zMfi7MVUJFqwiKeAMNGdaafZcgZg3tBDijUDoRQ,1792703638,460183831,25,30103145604419,-2547968465,0,-2547968465,800000
W17,3JtmnKcAg8tfqQ4fkmrf2SCaDXBDBL9hnoayKG26XhBAeFzLzCQDuvzBpMbvf8bMxJGoJa5DwNRpRDSdTDRs8kpc,1792703639,460183838,354,30844706309349,-2827717742,0,-2827717742,800000
W18,5PG4DQa2UYU7YeXa5gKwseY9ymACvyuYoaTH3YWmfQSDz4dWrfnSr7QVXbWSCNFPp7YM6VBmQRQ4htZ5AJ43Qpzg,1792703641,460183845,673,32482187220705,-3321059870,0,-3321059870,800000
W19,4AHNG71usdo12nnF8KZdyQv6kAQcEzisnfWZo2khYon4DVqNFA112evNEcSrkkwjLGMji5jWYDGjjKb4tPRfjotM,1792703643,460183852,217,29136761608778,-3344498910,0,-3344498910,800000
W20,579BNqHEZjRRzVE1vZNoSG7VaVE8hczYYPTQF5W3z9TYdXWpZvMpCf1LdsjQhYESB1VXiq2g3MbGSSe18vnnxCUG,1792703644,460183859,320,28559404173810,-3689085541,0,-3689085541,800000
W21,5iDKJXqQfUrFUHgB473npxauqM1vY48bb8WEPWAkoXjuhRTS6ZjXdMzyij4vm1eRtCsrTtK6BvQpbHSmHei7S2jt,1792703646,460183867,429,31889936869714,-4721613681,0,-4721613681,800000
W22,3LCxHCPR4BCa4FgY2z3Zi38m6dANmSAdq1pDoBfjcZVV6kvG4LVA1fFMAdLenM2BnZr27VNuFJrmvUGajNk36VvF,1792703647,460183873,291,28007568289666,-4724267745,0,-4724267745,800000
W23,5fi9JXmWt1VZMcUPCnYiLCXrkeNPJxXrKiv6uh5GfxRT2n9gohTVwmzSS7Mc1txP693KUq6RVUaJgWL5kVkUQ7GW,1792703648,460183879,178,31088593766536,-5829846464,0,-5829846464,800000
W24,2jEkGBvev9gpH1Suuw9mEigEgYQGwHBcpjuhiaoFGwQMi4FKMpnYGn2RWt2gddkQUFXcoTkkvtBdhw744CZGXs4,1792703650,460183886,232,28525250277347,-6312256648,0,-6312256648,800000
W25,XRcufWFKByFsvrwe47XVFBravh9H759UznVgarzf4xSwtpAmgScfm2aAV1Ucv6Vrsf8D96egZHUPPEXQnu8FcnB,1792703651,460183892,181,29092408198734,-7579376667,0,-7579376667,800000
W26,2ULqQtKh5ZgNSMX6vf58QoSparoRmSXqg2CVRGAr8SMyEPzs1BU7dPcQeQQCEi6UMvA66D29X8i3hpBUBCwvsQmx,1792703652,460183899,25,31961414276748,-10081196227,0,-10081196227,800000
W30,22YhTbQuZ5KkKLCCUbKBZmUytp4BXLPqDtTJ61qnA3xHqWxKoGxqmxrR84VFpVoLuEKfKE29tu5Qv18qb8Us5pTa,1792703664,460183952,345,5685423820389,-1911039944,0,-1911039944,15000
W02,BcW3aiDSeZTgNgbqVEVM7zAiSRaBvT1FCC1MCPit5kaBYnAfPkz2xtJJuit8KbYoQMkE726Bto1iXBdjv9H2WoS,1792703664,460183952,343,-6127378320796,2012390822,0,2012390822,0
W18,BCyJxR8ckTtCSTKqNcXzpuLGsMLQs6c3ddEHGzA6ace8sQNWd2XuagZY6Q5cQ5fydQZo3dQjGFAEYbv4ngB3Emn,1792703669,460183978,222,-25000000000000,7647972687,0,7647972687,105000
W02,45hR9pcsM593Vff42BrXh3CTFhXgb5hg5HD2aXkkVfmVbApauKMdpZe727LQHfQeVQKSNa3QMgvszVZ79KkMyJw4,1792703671,460183988,291,-5038847555624,1419790709,0,1419790709,0
W27,531vpMafcp98m2moq87PgV8JD9968V9j9UW9Wmmybd7kXw4pQSmfKDqjTQPBfVqti8sFpbV6mEohHthAcYaRe8gC,1792703671,460183988,293,4673820433522,-1348069837,0,-1348069837,15000
W07,3fhq3Js4Tc3KNTtKVcTgnDLNBxDn9yrhXaa7itSbRXtcpTUdSfYWkrnWnDw6ALBLrNNhce3zPgqcmHaq85Ug1TMB,1792703674,460184003,431,-2517812779295,785940801,0,785940801,105000
W18,fA6jvyTLWiidqtJ59suL7AQMSWDnGFS7AvJtUaL5f2ka3r9PWXC8PANVaekApoZBBbqSUE7ka9AuEZ7sMNxRFbB,1792703674,460184003,434,-7482187220705,2264187081,0,2264187081,105000
W02,4bHyKHmq9VyUUKr2c4VLdHhqoDDF8FtYcKEZExvVnH3cZMR5o2EFMHCvtFbJpLNw6EH7d7YDWTCL3NCJMN1T5nrV,1792703679,460184023,93,-10266026905479,2940392138,0,2940392138,0
W28,Pu5DvWRWMGZYP76jrQFCwUdPjkVMKVLMNEACaFoprAXnZoiyP7DgyezEAXMEiACpDwcRC3GRDNSo1hAHenVVMpH,1792703679,460184023,95,9533164022975,-2792641195,0,-2792641195,15000
W12,5L3cRQAgNKE9JCXiKpuXu1njYK5qMMyo38yWpXVRAqTVhnfc7AFJMWmWjMqNKuVoneryS5YBnF62Z7Y63c6yULHg,1792703683,460184042,257,-10000000000000,2882902953,0,2882902953,105000
W02,49Sjf7wrFKzrDPhcP4QMFALyv6jzvp5gHMWLvgVorS1tEcyUB9keHk4wMdhiWRwCBoDrvsMjEcJkT8JXWGYiZGWj,1792703686,460184058,322,-8180804177998,2257192184,0,2257192184,0
W29,4C6hNEtsaRrG8eqmkBsRSJUrywSZCGhwEyAYmGFKXtji61Lp5JLqkhPKqqF1YdRX2suAMNMcF4y4JfUh5bL9K8sD,1792703686,460184058,324,7593148263688,-2143601238,0,-2143601238,15000
W48,ZDgLaBSfXA499JmyYwejYo96EkhzJK1n2PXUTgYhaN8CWdix21P8UWaqXGBwk6z7Fk4f8a9h9RyjUL6Y9j6YHSv,1792703693,460184090,539,3011606857926,-917830738,0,-917830738,15000
W02,mFKp9wBNcoh8UadddWioXha6Pz5Kq1q3ieK5PjecyMSsGpDMcszL5bJHmdgyWtKkC875TsoQzyt4FoXeGeUoi5N,1792703693,460184090,537,-3248008140774,966907447,0,966907447,0
W07,3VM1bJNExj23EqZXJis77QnU37JiT7fSuUUXtQggxLT184uhGYFEj5Fu5DMVBe76Sjg9Zotei8bREr8XTCESauvZ,1792703700,460184124,225,-9651007800019,3135715595,0,3135715595,0
W36,57EYicFAUC2S22JrH93srj7g8TX97YoUW5JEhH8uAet9Y2nm6tfxgh3fXqoHHi7xWCFxvnPv5RqjkN74uJMjyLhn,1792703700,460184124,227,8962074606802,-2978198479,0,-2978198479,15000
W07,24Q69tzba8eb8cZnFb883X2PcxB4d5WfnmrGJgi23w4YzqomDr1sDv2WkXgYGHdafKyKDkdf3rA9fYgs9eucMbAa,1792703707,460184157,491,-9137812169473,3054084048,0,3054084048,0
W72,7YesDqRrciRcmuYc9YjGiyG5rbVLPr7eBANhvdkbtZEbkNVTazdQspT6M1QDBp1pf7nLMmvUfzegH7GWd2nAjbP,1792703707,460184157,493,8484770974531,-2900648509,0,-2900648509,15000
W07,5KJQuXsbWsY9bcys6uGXUCVov9pt2Mgwo6Vic1MdvRRHwLqGZ3w2hPBZxzUzYRQbCEDwZh9M2jZstsKP6Rmy84mG,1792703714,460184190,10,-11149486494184,3805634024,0,3805634024,0
W58,M8PeTrdBfSDiRjJLM8HdTueqDCVR8WR8MFKFmNZfRMbPD24hxya1DgBb9GrJVfsKn8q9saayZJn5rFy8y3oBKL4,1792703714,460184190,12,10357772478317,-3614620986,0,-3614620986,15000
W12,2X5GdpnniTQWLWPqeXCq1LKPTinA9Wn3e8ksBSnkWpWqaPddPHE7U7oWV1u5KBL1PqDAkPNbqAA8rJXvMMiyQ6f6,1792703722,460184223,99,-5198771828583,1987890020,0,1987890020,0
W85,c1AZv1KM73LmHyiu3n619g1sghoFMJb4Zf9oJRgMHbgYJvA4tKgJ9NF7TJnGBXDvMnu733ofpyodEXJ1KYSqkYE,1792703722,460184223,101,4823216300684,-1887764183,0,-1887764183,15000
W44,2kyvb4JvnkzomWtZ71aq3hePRJZmaVx5A2AmNCkdqRfDwfuetzFA7sJmxYvLeKPaJCjLGSagniXeXjyM4LhMry5N,1792703762,460184416,244,10805359299947,-4583040190,5302225,-4577737965,20000
W12,63Wm6hyZv8REvSayLkQsmxjvgS2W1eMiSCDTB4jdLCM4ZrGnUDkgRr7d7ucQ3XV4oRa7xJJMT8w2ZrAzuRQuWU5g,1792703762,460184416,242,-11289412556375,4631766369,0,4631766369,0
W38,4e2KRT8ZkSPwV1VEq9GisMpNsMvTwTKWqYFpvHfoWrqixSV2HEyFMdooRXqyzKjd58BNNyG3GQR69RAy8zLN9HRo,1792703769,460184451,200,5493835208791,-2396363104,2144447,-2394218657,20000
W12,5yjtAGgPQJyLcATrS15oLHHWM6b6rbMRqdduTimhSGSoWSNbJfwQQG8UvY486bomvqbdH2hicPdtFesVPXgQuNMQ,1792703769,460184451,198,-5746606451378,2423001635,0,2423001635,0
W04,2qX5JoPAoZkoiPcySojtqL5oSABq4fCDEThdMQSNbkUUNmm2wbVCd3vP62jLJf8AsugRwnBiHfopFfQWxNw6ScZj,1792703776,460184485,459,-9715536571876,4024310236,0,4024310236,0
W50,3VAJ5fvW3X3YZC9ZH3PVmPRPGugb2MRXWEwhBFpn6Fc82rTzp6qtVvg5FgBqVwZGbX3cig6jXQhcEXUZ8DeTxNYq,1792703776,460184485,461,9296319588774,-3981658619,4310994,-3977347625,20000
W87,2DzWauFdj1ytWuBaTY7tHSvxuqL8xsUaKZz8c1A63ZyLQQj2LoRKYwNRjvrZanoXzLYaDj2Fxun72qtd9CBE8RDD,1792703783,460184518,262,3814949150349,-1673646758,1360214,-1672286544,20000
W04,3KjUVPvVLqDWimgKH3fBTVmYPqUwEMP79BfP7KDBeAx1DEcxPijYq49X4uGKqqgaTyzeGryCtbJsWKVPZsfZ73xP,1792703783,460184518,260,-3996001302364,1694387983,0,1694387983,0
W04,1czc2KBrY7qyRnc6CbFxX5tu4wAMXMRoNyepJcSQk1dTtLqeLdGWsrwAeX9wPxPSfUXFWNTk88t3YSBLPB29mKt,1792703792,460184561,542,-10631209068705,4374245416,0,4374245416,0
W47,2hxJnNN6sHWyMsHJ5nFVRih71nTbDLHQi6Mrjip2D9wAMW1ryN8nLTr1AYRxTPBPfsth5fm7Cg7KdUfEHVVTvgPi,1792703792,460184561,544,10171165604371,-4326748938,4869127,-4321879811,20000
W95,4EEHnUpvNBa21czHFjgwSQy8vf7iSdpxHUnPUKAirxQvFpriWpvyA3hPGJem2xRkNhnnpuk4oVPcSUVjUWc3AMvF,1792703799,460184595,322,6690140089960,-2972776815,2847202,-2969929613,20000
W04,Zx5ku4px4Dg5h8JbLLp8MRQdckg9boMP7zQZxRg6zsMG2GuoyKoatDj1jZsThRhUnzz7DF8Dj6ANK5BFmAW6o6o,1792703799,460184595,320,-6998645746141,3006596807,0,3006596807,0
W62,3C7a8HMr6WVxwEUz3LZy5oryVNgXZ5WfoQqTo6yVgDD8nEtXmVA22MYB5VDjSWf2HPY1iQf7MK9FGjN9KnRLr4su,1792703806,460184630,150,644473866920,-335343365,392185,-334951180,20000
W04,4KsvAMRWHNmx2Lz53zH1iB1ARFkxvVVMyuagMtqxhJq2S93NQ8oLigLKtWDQuqSavyvt2YZpN2y1NPwshd3EVXsA,1792703806,460184630,148,-680222336023,342522615,0,342522615,0
W79,2LC1ywqikbgyF4FD3Eo3qGhth1xgs862Wicb9wmBcFDJQ94yoGAmdrREUZT1nLMyssybGKYR24bdHNHEv8NBg7vJ,1792703814,460184666,292,6757847475969,-3435455441,5061388,-3430394053,20000
W26,5a8tjJWbE2LpSN84JVbZyRKPzLsE5eRN4CxgosKA6RevceDGSRDjPDDB3dmScSsEQKzNMi4QuBQL8ZbQdET1WZBy,1792703814,460184666,290,-7065247269460,3472589855,0,3472589855,0
W60,2gmezaPT6nHigeGABhC5dL5oZEoMnoTJBeZkuSAovYfnXcMuyRfYdwiLBAZ9XqpKxUuabqbTpRGsWy4LGdT1yudC,1792703821,460184699,314,10257973478683,-5303493463,8863193,-5294630270,20000
W26,5vwrJcCBZqpDhH37mjRVzbHBvDUfgsg2ANPFBgC4AraqStBDZHySwrJrDiVqLzZ3YEYvmAFPCbYh2irPEkhvan5F,1792703821,460184699,312,-10716138322438,5359496948,0,5359496948,0
W26,4m9XSv1AV8abUZETMb8i9giAUSrCVorL5npZYWiuWhRssLeT7wCndTkYUYNSphufb3usLP1zQTmBfMvPittHackG,1792703828,460184731,492,-10865285177646,5961539260,0,5961539260,0
W82,LrZHeTuWLZRysQnibFWXtthuSAfaj8MkP4rvpGYxBZ51sA52cuh8knrhZ4fZQW1gmYzkg8h8pUfRg513HDoCQth,1792703828,460184731,494,10402198679459,-5899515352,10070038,-5889445314,20000
W78,2CixoFBzjcAatw7iGoB73TpfpMYdL6p7RgC4GFpFQ5G1Yw9ADuFZgxoP3tTxoXWPRDdRrEitXU3eoJyFawHK5Jpz,1792703835,460184765,371,3167499939631,-1933504925,2506446,-1930998479,20000
W26,65vgt8rZ1xs4JTZc4shkcodryjGPwwqVtTJWqS7zFNbXPUEECQzpbouLCUE6DmNvxLAQA3AUEA1vorwaeUjULPfs,1792703835,460184765,369,-3314743507204,1955468121,0,1955468121,0
W57,5AAnHGGv6dMvp7PMccn1TQ6iZqL7sheh4QjTaC5X72CJoLPrb8RCYTnL6QkrEYf52xYwxX7QcU4YjwRTmA6V6mDt,1792703842,460184798,242,6301636896016,-3425965120,5001142,-3420963978,20000
W21,QKYktGzwyqcXSg98YXgX5m3if1kxEyNPVrYyhAHn6foikgo3ZXCJgU3pRAo4eUGDERWiinawEDWFHVp3ZUyUdwY,1792703842,460184798,240,-6588579924226,3463003672,0,3463003672,0
W15,5Wh7CuAtKQ6a1RAkDLYkgfPg3hBVeav5gtrKcUTSfYWrGK6CRfcjLZwUTA9FmSLh9etPosuhyTTfYkxHcMACzGvs,1792703845,460184808,594,-10000000000000,4839779530,0,4839779530,105000
W86,4P3BQYLkynw7tz3gsrk23awq4zRypffzABktr9cjH3viEXi7wa5KtftCXUjD9C8iC86MCfRcBFMeJbvgWXXmCpAe,1792703850,460184831,444,8777587821056,-4575597304,7274446,-4568322858,20000
W21,tS4YX3BBfQKpuy8a3dRtqVr1MEBf9bz1wn822E7KUxpQSqiHt8NhKWqvZdVZp5nwJLPaxcoxymFkCvYRKCyPZn6,1792703850,460184831,442,-9172390252369,4624248302,0,4624248302,0
W77,4f1LfAEBzZUmFYg9YeGBn4Sq7X1GzfdiTS6R4YrvEkxjC9LKpUGQZp8zZG5kFcxW3QzTLjRtm3YsvmrUkS9ajKzy,1792703857,460184864,125,8231287407176,-4419892524,6921915,-4412970609,20000
W21,sgbVxGKDpxwuNXEvJevs7K3Y4T67vpheBL9TQAjP48sfcXrYE89F3JyHnDpj3WpNcmVAzXeZ2EvDaMvbPospbRM,1792703857,460184864,123,-8602266390243,4466970747,0,4466970747,0
W71,2D2oeM8B8oyj6ZpR7TMAYLwnogciMKbWXJVciwXbJQ3CpPt82vxCbnCVyun2mC4Sirz6qqaxRtL2HcKfrMVd5s1Y,1792703864,460184900,208,7200721127798,-4032774546,6115393,-4026659153,20000
W21,4LesW7WiiikjPSR2727SjkLUVm9NPLrz7zfd8BfGk1n2bD7j1QX5gTYupRYa7Fn6wi8y8QUdZ4o7wNHd4TfCoArF,1792703864,460184900,206,-7526700302876,4075942486,0,4075942486,0
W15,39rB75eyFqFCqiVnvuVWsz1cnJviSCJtynLReimBpBp4F9u6UUUFJbXNRZLWjmS2HDhxrXa8CEKgijG9kK6Uy4Tj,1792703871,460184934,187,-12491043296424,6910900975,0,6910900975,0
W64,5vVWU6zouhmrtFoawjB1mSc1ZTnheKxXsd2Fc1HrVfAc5waoRfV1RfTUrjFE9faKjnqHisTRH3tUUubLiaLcn76x,1792703871,460184934,189,11962539401300,-6839383450,12323176,-6827060274,20000
W75,4Hs8RgAjf58CBfqMHRvVtVYdJvkDFa8EQ6KWYo7NUpiUJVd8K1tyJv3HNUcRgPapZgM61cWnXk9sdcULY8JWGebK,1792703878,460184967,342,8575226476986,-4826168960,7707091,-4818461869,20000
W15,xUUfFn2mgUsQH8HnVNv3f28PiazjZJvhK146tXhYkXu16f5UjrMZthbhZgkKRRAdwDDUz4aiqgxxfyskrmzw2Rn,1792703878,460184967,340,-8960564455994,4877350985,0,4877350985,0
W37,2rhwsK6hPcWqkuFP3FZPiEB76iLfWAXVoxqdJoV7GJjUPnd8Z8hx81eMnEC8qKp3Q3M2zEoaQV89aPvWL4uuY8Yk,1792703886,460185001,304,11371249497933,-6385595522,11240032,-6374355490,20000
W23,657dHFXoptz5Ef5zscqT6Jy9fLsaECVUmcZW86vNwBorwW1iVSpBMxw7MPUZm1syTgSc36coEsUF9HSSXjejeyYW,1792703886,460185001,302,-11875310549425,6452529330,0,6452529330,0
W23,25PRmrnpbAhiqHgnN995cvGZzrHQv7aH59AoUhxKxcK3LuAKvvsVEGqXYrTYCoRMp2n7eDgfijF7UvVx25t38u5q,1792703893,460185032,806,-5083243582814,2805583394,0,2805583394,0
W49,3bb4tj5sRR7mhwQryaURNTR8MncpXFhFcbPbbXiMUTEqrzJRznWMbiZovJVznyB6QWz6jmu4T1EoeMty1fQKxe6a,1792703893,460185032,808,4862687136309,-2775119045,2368187,-2772750858,20000
W23,4zwmkYDrwx5dtu6MWhfhKFEu3XKYwRqGqzGEPWKKHfe7uqS8J8jfuhvBUxzqmRQbKZ1BDfZnnHKim1hLqdZBox3D,1792703900,460185064,189,-5226473795178,2616816562,0,2616816562,0
W73,5JDd6XHGcVztrycJTVpgHytd64Xmst8n2ASHbC7k4bwEC2PkWFf9EgmnJYaJef8YJYkQgxJ96MBj3j5ebzxt9A4E,1792703900,460185064,191,4996779507608,-2588239881,3571573,-2584668308,20000
W31,5amWAeMnAQurvu68sA6YVcPjEgvr84UXobUAy4jvRA88PFDts8iPZWq2CpbzNpaPSzPBppMR1FcDvNVg985kByp7,1792703907,460185098,217,8519674461200,-4361233986,6850078,-4354383908,20000
W23,7qvkePwwRbMYu3pzsW5G68N1STcABt13tBs8eHE4R6xFY6cp3YjVPe2MbX8BJqnPZruA6HTgRE6qFC39puE5Jkq,1792703907,460185098,215,-8903565839119,4407719698,0,4407719698,0
W11,4skJrRD53Vrq4tX1oGVbhC2jXVj4W5mVMHfTBn7ksRJu3AR9T6mxXKuuKDst4AE6UZHWKaMmaKyPjXabMWsd7og8,1792703914,460185130,321,-6349783219558,3252415726,0,3252415726,0
W91,4uDsENMTxyNiBRtephNnkkoViQBm9mqPQUA54uLriQ5BiFYbbzYUV1kY3C93cSzhG3B1K71FKTimCwV3GkbXn74K,1792703914,460185130,323,6072706756997,-3217483054,4640084,-3212842970,20000
W11,4pUrNNGwTnRJVtmh5exNi3rzos8NJEQTHoVYjyC3ZzL3oSKCxkCqsPZWiSb7oYc94dQgFTvxVRTtDNPmF49si9f6,1792703921,460185163,243,-6128847617012,3144567319,0,3144567319,0
W43,5kw2L6DPBBNgPzY1faExqgGu8g63tkRbkQQtMsGrAsQUbvQnFGJTamanrQ9nNr4sQbBnGeySxbJHtW2NgNJ1nhv,1792703921,460185163,245,5861912122758,-3110713131,4006382,-3106706749,20000
W55,XszQSz6YdPTFfgMJYSEG1MWYqSjwnYKAwzuTmmt7UAjJpUBmstf44CJWtzxqF3w6zTQ844DwjThcuntwwjt384Y,1792703928,460185196,373,11603576316699,-5549634851,9550082,-5540084769,20000
W11,y5wCnp8BHMscGmdsTb2nDbvjprF3ZCNMMr1qiH5SyGXSAj49ng5EqXVqikMy8dYXV4ViSecJxNikgFvj3P851SM,1792703928,460185196,371,-12119836540854,5608124612,0,5608124612,0
W11,5qrvvbTzn8aL4anaxL9TgPNjr6PhgHcRsmGMm2FWDnp8McWxsj6R19gmChHrD8CGWHN9WYkDbNNPnSDUVDjm2efM,1792703935,460185229,253,-6486945755999,3034277807,0,3034277807,0
W76,dWcMQo9zujtYXpcraL41qXmww5KtrQhoit3DemXuCQrWrxB2a4LQDpRVLEnA5vgyotuUmAGdE6vq7eyHtTLpuYd,1792703935,460185229,255,6203497612468,-3001526514,4304780,-2997221734,20000
W17,4PRXEwQEXXyyzwwizdx8PixX2EejakB9wA7dq1pfy4m4EiupdWL8SJ7HpdFTNmWxqPLoQb5FEx9CHMYkEvibekCo,1792703943,460185264,381,-5700119646031,4597852497,0,4597852497,0
W84,4hAhsB37wVFmDspTmhg6zAURFqLpcpTn855LxbuaqMb6CGrqENjWXefs9TiaEKDWL85vEhMGEajRDFxcNaMXwpDf,1792703943,460185264,383,5456283865757,-4549465457,3885237,-4545580220,20000
W16,HQa74RD9eS7GFs3fNzPCPVzXNHqnDcreLR9SGo12rEJNu2dGcWdzV33qyg9BYoHP1gEjtHW7hPckTyrV6T5UTG2,1792703944,460185269,475,-10000000000000,7587544169,0,7587544169,105000
W16,48gpb8dp7W14kSPzkUKYvQe77rHoJWszEmRMHKBgzoD2s8kk88yPwbgz38UXV834kdCdkjRCGFAZ4w9H88LVKTxw,1792703950,460185296,212,-10000000000000,7492340460,0,7492340460,105000
W67,3ktGxZgHySKQ3DY9KC6EY4dUUAHRWuy8mfbQeiMf5go6iQCPpv8BcNqDd2W7LpzGqbRja8VjRDfyUjjYZ2rTve5Y,1792703950,460185299,297,7077215662185,-5868570955,9369231,-5859201724,20000
W17,B8qqEJGqc8yUSgScAwEcyrWMtAaV4spK8UQgQKNEVonKRrmJKH5pxjCWRuzbQvKda6qqy4VcU5Ej3JzTnP1cZzi,1792703950,460185299,295,-7396449851594,5931663273,0,5931663273,0
W16,SVHSaKTdtYQUb8y1vgakfv4hAfKV64WQoierv4sPyeDgFcprCK9qC4PKffMvtXD8X3wmN3vghjPmiq4aBLNYfxr,1792703953,460185311,301,-5000000000000,3810263182,0,3810263182,105000
W16,4igSSTiVPLE1nSCopuPoGU9dzG1m41Lc2UJSy3vFWq2kfSn9hGoMXWf7AK3MN2TGyf35RQ8bKvq592X1BSTgcFCj,1792703955,460185323,125,-5000000000000,3921472144,0,3921472144,105000
W08,4tBCbnHgX6LQs7h7AsfVz1UwViBxTXaXMXqpLNvts3f1cr6vP5QsBJoeM9Ztfk9iG5nWKjrwh7yM2dDq3TLsowfb,1792703957,460185330,382,-4896854395581,3720356099,0,3720356099,105000
W16,4z321U4AtGysB5x1brbkN2rd9eL3F2gcPFH4g8TK8xnMmQQMkgXuqUHrBh41jPfUd3Qtuwi9JxPULhPP9gnb7hig,1792703957,460185330,404,-103145604419,75594899,0,75594899,105000
W33,2Z9d2EP2VrLqBtWFHf25ejwrTa7YrGbiduyMKBXFEQPcJSEmrg3HdmQgsBNQCnWhJPYVi4suHoqh2TVC6zUbaaLo,1792703957,460185332,77,11641014635154,-10663047095,20970476,-10642076619,20000
W17,2qT1rvjnECzsa6BYmkLS9djTdh3obsrG9WbgHBx8xi5z5U4anbVRahr8AbSobMqT8A87q4t63Y4JqCDgep2k82n8,1792703957,460185332,75,-12149823352166,10774546585,0,10774546585,0
W08,26TACuWdwof4r9N1uPC8h5Q9Tw2KVqarHPuaQEc6XN2U2G9bv9qmH7XbkuyHdcmnYTtbTbAYMdPWxupcrRVXcDJb,1792703961,460185348,381,-10589999999999,8551849360,0,8551849360,105000
W08,2hff6TBycMMrCHrrGC1JuJ77h9YAFmqtMnwTowTn2Cdh8MsyN2y4JfMW985qaAujoVJg8SvNF6cWcNYRT42x3H3y,1792703964,460185366,250,-8920000000000,7286770676,0,7286770676,105000
W94,3ngSUD9SqCG5Lbf1yAKrUkivittNtA2dCqtZxhXVNdSansuW7XcUwfAr3afPY5dqdQXsAKc6KbgSBZPVXWV95ekp,1792703965,460185367,41,5354463769945,-4918354025,7352017,-4911002008,20000
W17,6ekc4xDoVF2Z4uNjWaHfSVsYJXwSjzcFceLNxLL1aGX4kjRqcfwrtNHvyohAs6BQZckYT8egfVcVW9XBtqqzcGD,1792703965,460185367,39,-5598313459558,4971826312,0,4971826312,0
W13,2UBJefZGkGQZmu6wo7uFAeZJjdmog5qhLFhmEc8qVSXXuWxenEMUnmJQ71FyGfFdkpmjtC2PHV1j24BdfcEe81pS,1792703968,460185384,255,-3283715545606,2716809420,0,2716809420,105000
W08,4Y6eQSu88H7rvvqmEP5ehHenzou5tq6oeYrsc1jMhWXpWpdHE6RtdqBKiZgBbv6MVzd9VCoc5gp4rgvYUqAYou2x,1792703968,460185384,280,-5636284454394,4377616904,0,4377616904,105000
W13,2ncky5ju1R2VSxEzisAXv88hLpshbb8YqGDu9wpcBjxoEC9eCwWQ3cPYscM4y2E4HYBhmWUqCqkS6wjQxYHtyaKS,1792703972,460185402,143,-7927710598895,7049083411,0,7049083411,0
W54,37bi16WCqwTUwrmzLJdZVABMnCo7NxzwDxCXZHpNCmE4aSFCPEjEkVeSspDbcitMCxpu5YFRuthHhDxqqaLvTJKA,1792703972,460185402,145,7589054468922,-6976184062,11581915,-6964602147,20000
W13,424cSjiqVeKPo6TygFUbSic46EEi371c16GhTRATDkYrT2DTVVU6SJZV78Z5wg46Ap7AdSHKDUBvrYYD46QGsxVD,1792703972,460185402,366,-8920000000000,7113571741,0,7113571741,105000
W13,2JB6T5SYunyodgUUT1zeUqwcGxGDyKPS44djmL3jWZVZe3jwMpcooXMyFp4qkALEJCNRzRXu5yzFmqfCdVY8fQPG,1792703976,460185421,84,-5000000000000,4111346904,0,4111346904,105000
W69,3cUPNWrko1GqWn9Ct6RkgDYBTmEvC67Fb4oEwZFHeHnY1j93BPL1es6r2LdSpkP7fXMpc8ZuPWJT1QJwrQirHjWR,1792703980,460185437,578,4362679953649,-4193634326,5993899,-4187640427,20000
W13,4RaYwtCXtLHrAeEPTVc4jQZbYhsBn1UigmNWgXSj3YFN2SCWCqVVvnd4gFAUjikprVyauNbuYFRxLRhWCC9uLkGR,1792703980,460185437,576,-4561384921575,4238427112,0,4238427112,0
W09,3XseC7DYkTHJxbKgNGx96qiEttxXpu6zsoam1EBqqHAwN9G1XibN49BVLLL1KFXe77LkmA9ZfEeGw5Uupak9TihB,1792703980,460185440,72,-438615078425,369590826,0,369590826,105000
W09,4AWDar3WVWfy1JkTNmGYbYwegBWFTWFJS3PNF91DGvdhPn6oSKUypTx8FX8YQcx9osaWdsgi6HzesMLq7f7Jqaaa,1792703985,460185464,198,-5000000000000,4284288338,0,4284288338,105000
W09,3QPnGwQvVn3sdfnqBuAvFtqS9xJqLF3UNdHr7K8LDFgXcsxr8kMdoAXYTuwLNF34rfUviABQ6TFhPnAdG8q8cC2K,1792703987,460185473,227,-6922340085109,6318279933,0,6318279933,0
W52,4njjhJGvuyNwDWzF7jzuHFU62vrbc4EeBaFT5qu52K2xsj6JoMNN1fxNxvYWdrCNs7wPtrCtiYFGMm1bu5GtKLTM,1792703987,460185473,229,6625103971559,-6252688619,9969280,-6242719339,20000
W09,7JJTPCF6TMoZhb73G4DQszDGSHYoRmPgeYdWZkRgSXRLqbE6rKbhEN5oVQCZHT9sDFsFyHP4SjoHriNwoiPNqRK,1792703991,460185491,451,-5829999999999,4957526055,0,4957526055,105000
W09,E3hwMFT5GWJoefJDUNMpeuPcHqcFUDM46NDCKgAdthwqKAko1pWrLGxBvVEXT6fjewkKvDi9PuycCs8qJp55Vf3,1792703994,460185505,301,-7090970381950,6259542137,0,6259542137,0
W80,KydKyHkYPMfQ9wtAB8Lkb69BsQV2VXEDGkto87WNzvsu3nrJ6va2vp5vqbyzd9xuVbNJUgEAnmWBTvt6skG9zJV,1792703994,460185505,303,6786916083418,-6194538201,9552370,-6184985831,20000
W19,4CVTRhmiwQipoDoi9R5yJ4tzo2XnAtFTDed5D2B91EYZ5scQjTcm7pciAfa2AkKzcifc9AodaLkSvRjSy4mQ1ZuJ,1792703999,460185530,127,-8050000000000,6620296548,0,6620296548,105000
W09,4wrXEaD8x7g8LPLsEPUX5wR4wVCZARrjjAMMWbHoRNv3QN8M3zzQ1dW1CJSH6nTSh9VcTEKAdDC1VV8xuDDwP8D6,1792704001,460185538,499,-4397019950206,3665477273,0,3665477273,0
W39,5pHWVD7TpxyCEw18sYUPG7Pidx2wHbbSrkCWRE6UzAbX3XM6rUc9yKixrgENLKDAoJvx6EkXiVzNCmp9W4DXAmpb,1792704001,460185538,501,4204831269660,-3626413985,5080397,-3621333588,20000
W51,75Es17Vd3yLhqdmbuN2zyETaLpXR2h5xtBZDTmnVFvAVi9WuSGM3ggydwErpG44zNuUq4Sh29RixXzsz4sQpEXg,1792704009,460185576,124,3650753550465,-3424110592,4701360,-3419409232,20000
W19,tVUwbhjTAwE4bGCD9AkKAMj2hXVz6V7SStuk5jX8jeEkjuqCqU8TJT3h8YvQoJDwuFMcLWfoRiDWvZF71REAwAh,1792704009,460185576,122,-3818068050398,3461130411,0,3461130411,0
W35,5zJNVvY1GpVwzEzGeqQNAwKEWmYF2q52UdNwktVpgb8qbLedSEsjZzMxwGWsQhz1QCTvogKph1tTsGCAAeqA7dtg,1792704010,460185578,826,569845201801,-1351200,-541436658,-542787858,5000
W25,B5Zq7tCucNjH32xzY2C7ua8eygTzFPb1b6Y5YH3nHcDbYD15DLwE8qeRHqJCvFu2TriXDQrzWQn1Skj49tcECNe,1792704010,460185578,823,-600000000000,556645387,0,556645387,40000
W25,LVxJeJHaHHieP7Q69ZZQnQj6UiknQPStemZhBtrDycDtVobRpcF2QEUBQS351HLiuqTbnRGseBosdCa1i5HgEL7,1792704010,460185578,822,-10000000000000,-1505440,0,-1505440,17000
W14,zSPdc6nCu8xjTvARjMUBqrtzpfVijs6UfDq3oSwA6akThQLQAfwPnHictgau1ApMvTLQ6RRdoq78aDFUqkAnqZA,1792704015,460185604,549,-3850000000000,3354012191,0,3354012191,105000
W19,2djuU7TokLSTZPgtSsQMxNthV1Tdc1KXYsYZNswjiv6r6xwQV57abm97XHsynPsmUwJXLhuTG2Ui7xqwnsJZR239,1792704016,460185610,155,-11676768784704,10330934562,0,10330934562,0
W98,3AMmVM2LvgXmrArojG3DaX8BRL33PF3fLmzpAzEXV3GmrYCdwfthhQzQj5Qy2QF19DYH1xbon56T5ykx74ZMsSaz,1792704016,460185610,157,11187742482928,-10225216701,19715453,-10205501248,20000
W14,3EexUgYHquqFdC5UeUQvhxKXp8vYN3rFJt25EimoNTTP4KKkD5cYE4g1MhunpjP6e52aKnx2bFLQpdYZgFZPzoUf,1792704021,460185631,27,-3850000000000,3326382692,0,3326382692,105000
W19,5T2Aa8qeNWUWWfkJSxwHVJqYRRBK9dwWYQ8WG5771Jj6JkTcpoxUd1rRb5Pmfk1zKNk3ouZmNDdPVZ1rJmZ9argi,1792704023,460185641,114,-3440223461466,3170451219,0,3170451219,0
W70,5coW2XtqWcev1jwBWkfmP5kkiXnYXr8x9nj9RW5PbEK6X7NZdHkk2swGaCEWa2Nw7ymJeCNwxnMnsKg4YEguE9Bx,1792704023,460185641,116,3289057529812,-3136338192,4229719,-3132108473,20000
W14,3Qt9AjrK5EyK3Z8kFRiddgXLfxjLWEsTgfwpTY9DfbDAbwH4eNUAvpd5WpTtoo2LwQooHJMSSne6DwCBsd25DTxp,1792704024,460185645,469,-3850000000000,3218178150,0,3218178150,105000
W14,4gw6E9qUqLxm8FaxFrM9Kvz9iMRcYqGvr6wzfudtpdzNCLcuznff6uMj57oRcwMqMCdiUKVPupBksx5fno6zBqcQ,1792704030,460185671,258,-3850000000000,3278019521,0,3278019521,105000
W88,28s3ep37ABXZuwfyMqaaQ7Ztyf8aDMUYqYVwVn42RCBoFnmrFrZeENzjfRaoEP9gnMHeFjDggu4tKfu8SM85yYtz,1792704031,460185675,108,2055874354035,-1945536042,2450003,-1943086039,20000
W19,EEtRxdSdd7j5Bp2pd6aP5SkM9U2NMctBXxPsfUxsPZTzHDfDg6ccL5UUzGJDU63m955YxBBS9zLrdreziFqUBz1,1792704031,460185675,106,-2151701312210,1967620765,0,1967620765,0
W14,YjEU5UvUdeQmkeqc74Yr37WA1YyH5qxMSEqU1kiHtZe24GVk85YMVNLCnC9feaQxrDZijv7KgBVfc3qQ3FE2LWN,1792704035,460185697,217,-3850000000000,2942984959,0,2942984959,105000
W41,2Fs4yraLjNe2VBtdx8zNHPHBk5r7WWcjLr9AZjmAzxNBdUsdaNFHaNUvgxyrDLynHCN5wYfWt22m9t15sctUmbv7,1792704038,460185709,160,7108797713034,-5871220287,9367258,-5861853029,20000
W14,5Fq7NAFt3FETJskD7o52K4r3wJctWPoziBzJicDJQxGTRwaCxis2uSE7m5fpoW2qskzvoZXXDy8B31XHyLiUZs9X,1792704038,460185709,158,-7427834359198,5932958386,0,5932958386,0
W10,26Cwvi1d4qRPAyPzHm4DwwXBaoQhnZVRjQiCnPpEraoxJu93nY53me7VR5s2GTE2iveM9UxJYgkpaNEmWzTSeXa1,1792704040,460185719,476,-1407893305686,1017737382,0,1017737382,105000
W14,2nhxZL8JEvJ3Ki7cGVqAMDSMNX71zDEKxDDshnkzHBj1Gt7CHmRDvpaZxmjQWPhxp428PwbuVDG4BPWKKVPCNvHv,1792704040,460185719,439,-2442106694314,1812175537,0,1812175537,105000
W25,5hN9J7HaHRYViT5LR1rZrepbjHvsVc8egZegFBfNb26HFnR96b1mk3KDr5574JULmv4opDVosh4foaEM2sK2jWzp,1792704045,460185746,286,-7576849907079,6018452707,0,6018452707,0
W45,S1rgL6j3ypZpVwWd3q93U1rR6oFFbk5dw5pww2w5qjcahTtT53osTdkH87vjJQ37yWWjEwz9caDwX9dtgJVvKCY,1792704045,460185746,288,7252341701056,-5955859665,8949469,-5946910196,20000
W92,4M6uE1aEpjUY8P58D8s9TQjG13CH1KJbfCWruKCCcrtSpCS4R2Da5Kxd8wkSNDQZdTXpFBLrAXqJp1PVvejtFbpu,1792704053,460185781,17,9867010238375,-9224929401,16931309,-9207998092,20000
W25,4PdAUCV1vXbrAvnHMjzkjnq8n62fKdYUfEKaRZEavy4KNDEGpGgquVx7qWxcfyTBsfM2EaViii4CZ9VPYWjRuafm,1792704053,460185781,15,-10301289401133,9320543350,0,9320543350,0
W34,2VggrS3HnUWD2USMdW8XAiGgWR8uTagoBisxigAwszHWA4qfWmLn2o75sdMikNreAnWwptxAsAm9Z8RidZqH2DYe,1792704060,460185813,410,585605063755,-606149123,706629,-605442494,20000
W25,4PtomNu9kEazs5cuwfVzjJHBNLqwLNEDqpPa9RKkXR3Uq57o8FahtVF1zozf2QVrQX7EgYZjidq9ywkDe9fNbkzt,1792704060,460185813,408,-614268890522,614704685,0,614704685,0
W20,uANGD1dh8wnZ2zaoFGJDSjJwPYj4jEz6G3zBNXeuA6ewdjQZAPsg3qhXoZbUjpT8o69fUddb4FjgXddZQ8y6HLS,1792704065,460185838,567,-5000000000000,4514673402,0,4514673402,105000
W42,2Pvkx94LejT4BmY7bPox8i9FCoUetUncKXCFFdBw4Ax5BavXq1Ck7XgqA3VLnktk5Q8SHYvpb5hQCnoRmJpvCerL,1792704067,460185847,120,8686898867842,-8709725407,15405054,-8694320353,20000
W10,tTuQg5h3oBfRtLhFHhkne8rAEdKiDjp6koGDaSarj1MLtSHkMzHij7zzdEP4uC842NY3u4yiWYyzWqYdYgSQw1h,1792704067,460185847,118,-9071137595406,8800135275,0,8800135275,0
W10,5CcJsHiuSwaYcGUpWi1mtZbT73x33dq891cLhCrAvM1A62dV9RDqAeFgVPaqiJf6Ua8puh56AWcFNfUtd4Udfydm,1792704074,460185881,399,-6717786151972,6923093806,0,6923093806,0
W81,rHuEFkCWgaNzqfFCNyw4g3yZwRnLvCwruPDwYw4zc72ZWSoumJDchDTd1LAYwxLoyiZsLKy1hFNDfpWPAVgpZP6,1792704074,460185881,401,6430595413347,-6851454353,10087115,-6841367238,20000
W24,4o7pHCT3HFRgUgiuUdnUwuNC3pZRzt7FtUc853U6Ez8Gg4ipgVw4dh7HHktd6GyFVrQLkxBk34B547sbyAKFDBnj,1792704076,460185893,17,-5990000000000,5598990731,0,5598990731,105000
W10,6tUYktbsiQsPqxfPRpmZnJW3SDZorYDgdTNjAeNPjY93NPVH9qTJmxi9GEEgDtPjC8ULdRqzDxUYTc9k5dqCzdf,1792704081,460185917,244,-8357983515145,8391610999,0,8391610999,0
W90,jHLX8CgeWvUE5wS2J8XBjcaVbucKfxSrjAoHvgbNMj2orwYUA4vmiUnth3UbtbuczKJjce2hnaa9dH9odt5mwwz,1792704081,460185917,246,8002839070096,-8305286374,14331727,-8290954647,20000
W89,3UWy8tmhd5PtbD2W89NCJG1GZeaJnzJpcJj3HQtjQuD92Cq6SSwjkL2NVJjV6ysGNkH6CjAhuvUdJHL963ZzXnGK,1792704088,460185949,269,3343909205020,-3417725966,4649947,-3413076019,20000
W10,43PKvAuMDiLfVnyny3YhXDJBSDfKTwLfWHp8HunWbu74GWYBPbJMkbxp86qV6MLxSQoG2eDekFNGDthPjfoN7WR6,1792704088,460185949,267,-3497307506919,3454681294,0,3454681294,0
W20,2fA6jFQkTjZ3JkabHzmnYvCR8vi5vkKQq2EPL1jPgiD5XmnEYacfx6AXGHro2GrLW8jFM24AvKiVdETMz3qUaEiB,1792704095,460185981,349,-10184461752013,9826245676,0,9826245676,0
W83,4CJniMjLqyrBJWXkVBnQ6gaJb8w1h4Js3AQwznHia7bhif8qBAtr3D2Kxa4nC2L8g6dw9v4hMEkKsUSBStptdFom,1792704095,460185981,351,9759327415424,-9725574704,14061137,-9711513567,20000
W66,55aL1G6eu9uqf7vcbTy9QyTj73sM59PRGiPxp4KvfxP96EqAvCh1WpJFkQtc37DM5UZsYTsGFUvRGQDF2bVu5hTc,1792704103,460186015,429,7333048415417,-7259509987,8103825,-7251406162,20000
W20,KVYnXnbzWZRpDNLi9ohhSf6aZTWFCBmUTnDwqemprTjqNqQnYBVoCLZ9RvgLn2HxxcJELwsgvNFLx5xAypCcvGY,1792704103,460186015,427,-7656271907742,7335271214,0,7335271214,0
W06,6ne4FUoFnPqkm3wPUm55ua2onyCZHUSft8XoLHyz1Zyt2tjRPgEWaSQPoZK5T5r9PeBom8CeF9b7zSF7hjUXi88,1792704105,460186028,88,-5990000000000,4908642028,0,4908642028,105000
W53,2CpqhjXpeP22QZvUKGtpYnDWekD9NBEHtiJNDri9NcqNbzypJ94qCcbD5uSMF6cNnbnKrsJELKM2yTtuSs9o7Qm2,1792704110,460186049,156,5475985298843,-4663459424,2370113,-4661089311,20000
W20,3Kcj8eCZ1CerQkvhFXkQhWmb7RDHwRym2nGj68BkSDQJmegpCEm7HnGsS15VfkMgXktqJ4UiWmY8JoempRNymoGp,1792704110,460186049,154,-5718670514055,4712997918,0,4712997918,0
W24,5mDHNASyRtaC5SNTBnfwCPVeXXYKquStt8XajkuK8sWryfqMK2LntABnxRSe2XHFZjP3KoTQw4FcruB3KYPNHYQb,1792704117,460186084,116,-11305376512348,9103006239,0,9103006239,0
W74,rik2udSXo4vU9WZnSMyLhfw4ScP56QzCjSguPyrNaaDq7FD3SjwjbwZbhRcpT76YudKkjqAo9npLKswnPC4o4BS,1792704117,460186084,118,10829523956921,-9009567662,16760703,-8992806959,20000
W97,3CGcbvz7iDC5Ret4tUkfqKttaY2LXJc65igByD3LcTaVNvBXy4DU8q3YcobgihZda8682xTHTuGAFvGoCQwucgDQ,1792704124,460186117,165,10758170214201,-9699431444,18300311,-9681131133,20000
W24,4MPQh1s8A1Dm4pJ25o9ZEGtnnx9LLiDhzvKE2a6fpweo7idU44jRrVSLZ18QPFLT8nV2CTtWH449WMELf49zFrjc,1792704124,460186117,163,-11229873764999,9799838343,0,9799838343,0
W65,3cuofvpVGi41U5u7bNmLxHnDrHeCskzvcUoBwj8ujv8RvZB9BBZcjD1NPE1MB6Y72ZF8GPVCyNoew4Hvw8aL6zWL,1792704132,460186152,227,5858651836896,-5173738030,307511,-5173430519,20000
W06,Fh6oP2QXrEJ2sKiXgtnmseXtMnv7Rpc2wrg16tAEMq97S61GsTYNr4xr3vZDZUKMpCyWQsYLdAYSAwTvfh4kCjD,1792704132,460186152,225,-6114577786091,5228430854,0,5228430854,0
W68,2jRXVAWVrhaFVX9VCBeT9QLRD9Nj8EER6bkkpSrzFcrxsZ3Jko14LYxJfozxS3YhVKnNVUjNSeYqXTJdVqepT19Q,1792704139,460186186,258,8631541690327,-7973286423,12349927,-7960936496,20000
W06,5XTRKtjKJLquXd2rxZjeTqyUuHbhztufAWzCytjLmimyTfdqqqEgsDqgUG57fnBpqoDU4Ddbw1WLTFbPZkeUFTMW,1792704139,460186186,256,-9012781806511,8056257513,0,8056257513,0
W06,2nnyDMz4d9NmCqffmqfu3BA9LrVvnwuSajo25pi3Y7niAx9PA9M6hHCMfDZzU3v6SwsPNSPfX5RzRsi6dCHdZrhP,1792704146,460186221,294,-4525385636273,4063021435,0,4063021435,0
W93,3DxGabD2ZVhRkDQugJa4Rba2eurQDLmcQGbhJ4xc2QhCHv3Z5eySEWkp9spiXqLbH5Fzo8KTRT4PB2gXYwkVGYb6,1792704146,460186221,296,4328037400328,-4019982706,5705977,-4014276729,20000
W40,3C1j2RvqymQkZiL5NttchEgD7ZvAjDPypfQxkrHcxwvKt3GZkcHed2iBwDM78wLB3ZGcFJSX13mYzZPGLo1U9ftk,1792704153,460186256,490,2563314475311,-2393800441,-3206988,-2397007429,20000
W06,MkbCZyDwuCPCMthmCZ78nH47YRLALBSiHi7smyKCYVtYHwYzpHQXYEtUMau3JWqhrqR2pXPdFUd8KCVvk9HuW3T,1792704153,460186256,488,-2675063376265,2420413087,0,2420413087,0
W46,2wv6KQ3c1CTRQq5v8kNbnHZ7QiXM8aevx9UNjzgECu1jJkNHqgyxgSC4AJ3QETmQsUT7efSKCwhS9P84qjYSoCyd,1792704160,460186288,177,7329124565779,-6608448594,9586720,-6598861874,20000
W22,3ZtwvqRgAaBgwiQLa3ZAq7Vc1RDCxLW32TPHBDQQwzotdCg6py9bHB4AavKy2DBvb5vPaG113wHRKchRVqJSDjPU,1792704160,460186288,175,-7655617979656,6677633444,0,6677633444,0
W22,2SGoifdrZCr9cCp1q4EzWMhtfWS4BBeZoWyKKBerPvwfN8Nt5L6cqy4VCvbCeLDnzjW1A3xTDr4FSo7rvsKc9wMr,1792704167,460186321,128,-11052458719034,8883626891,0,8883626891,0
W61,y3m6kg1xBqNnXDcuuy1hfjKc41P4J4QRvXku7r1kddNtZYNPTwhUftcSpXpYKizaGUaynbs3Qj7wy3SNWGJoi53,1792704167,460186321,130,10592777464388,-8792382107,10753366,-8781628741,20000
W22,2kMxoSeLXwuKcq9A4XRMvf85hdWKtuVmKUD1x4LMLVDhKm3MBhLe5nyKufrUz8FpYtHyMAy5DajAD2p3wNn8gCGu,1792704174,460186352,369,-6514132507836,5044254444,0,5044254444,0
W59,3vdpY8qZUSnp2xKEM6sCZ5VnKZPiH1u9xLaz8r6vucCTTy4hgKnkphZuKKWmoWBXapYQvceSxnTtxJnrXf3ncAtu,1792704174,460186352,371,6232674549076,-4991403384,7616177,-4983787207,20000
W64,3BNQJKi155KL6RceciFiXo3BhsL98HyntKCuY6Uf1iJcpSYvs4LUb23WkALs8drMRduuP9uEFd39khJAzsCeC1YZ,1792704181,460186381,414,-503427099211,352673811,-12323176,340350635,105000
W22,Qwi6mUmW2hYupwjTpXtXxUkznvp7uzrSJqVNzvE363A9qzMo4SVrXa1wHC1dgzfdBrAq1wchgCgkassGvenzy3R,1792704181,460186381,361,-2785359083140,1916015234,0,1916015234,105000
W01,2WMaffNxYyCrnFnzPmxSgV74euG2FD2W98rDP8LQihwGXvNd2dDbsXVQcnd5ZSvSNeTa3urc9j8cBF84qASVtcj5,1792704181,460186382,29,-3261213817649,2143391764,0,2143391764,105000
W32,2G8HaqNp83HqYkfCgBNc2A3ZLK8f3GfYRLejUqnz9AKE671ogXoZK4RLUQ1eZXCqBC6A2mBTJEf7hPQ9mqooiSx3,1792704250,460186706,126,570130646307,-1351200,-586327635,-587678835,5000
W64,43YtaSHX31zh3X9avC8xH7rage4ozkff33ER6R6mMWWSwaP8vizEKd1LEWNncgweL2Gujg3ynZ3JhpL9K5BKinXe,1792704250,460186706,122,-10000000000000,-17000,0,-17000,17000
W64,67rpngtrYLAwC75FbzuEyZhGbQb4rpsxxkPC6DwfemR9aQw2tsKv4Rij2Yrpi3GQu3YuCM5BjMv2ycEWAxSNEFuG,1792704250,460186706,123,-600000000000,602501810,0,602501810,40000
W33,52oUeMNf1nZNtKgodBQ6Lqf9ReP6QnkMd1qRJ1wVdM8156P5Cuv3iDyfYVQjXTW4ao5efN6oAVaLsaHLAGjQ9Mv7,1792704263,460186771,17,-11516000000000,-1503440,0,-1503440,15000
W55,2mE4ae3uBoiEEQo1qT7QWgfZDQT4LGDvU6nezJQSCGxXS9voQT2XjHcueA3QUJxwwCXT3kBpnUmH4dF5eQe933xS,1792704275,460186827,187,-6550000000000,5359389658,-9550082,5349839576,105000
W37,4Pk7L7mkRci8qun6vLPFsnHCW53obYdEF8fvDinJ9R2BukTufTBw8CJL2gtJLKVYmxzo2xyawinHXQgEmkqwPxb4,1792704278,460186839,264,-776423683300,582380478,-11240032,571140446,105000
W55,5TZTFf73m8qryoHz5yHTiqcAkbKFd1T1GLpq9JAKdL5w5Ur721tKgUd9t7hY1FfET9RjBDvqKkgBPA6NkczbCGhc,1792704278,460186839,259,-5053576316699,3859595224,0,3859595224,105000
W98,voVnyYFqnQhDJV6Cfkrt8G5ntTLR8GEiUUAAgSbnRG3L5cdjECYmjSLTMA9ra9ETqbdMFQkbsRBw9PDQtuvMeMV,1792704299,460186938,33,-6310000000000,5709770376,-19715453,5690054923,105000
W74,4X2v4QjvGTDjKK1bDR2FSiB6r3wvrkenXvANRk8NAfHZ73qyimiTmj3apnP6Jvhkofm9DPya5JHJTC28qeBn4EG6,1792704316,460187020,162,-1160000000000,1067252069,-16760703,1050491366,105000
W44,3q5EXpnftUmYGPdqsekCMHihnbYv4Jte5SQQJT52utxN8kdK6D4pNgEQzdCdWHyRhAuk3scAxASHrqRaGv9HfPKd,1792704332,460187094,15,-1160000000000,1321722528,-5302225,1316420303,105000
W44,2k791Erp3VcSHGoMirtgZf2ACTsX5aDF56ywHSZDqLyZ7486Zt6GjMgNUrneEqUWR6CWUm8uQYXvdWBFjgmNYhTM,1792704336,460187113,295,-1160000000000,1411754309,0,1411754309,105000
W44,5PScqrHGuX7WTWEMuvGe2K3NQsbSNnQRJUGe5ati481FrjqptZyx2XtWVhNYvMGT14DHsXMbZBZyP51GGE2Nowoe,1792704339,460187129,335,-2980000000000,3599904419,0,3599904419,105000
W97,t1vc1jGRYHkHnNkrwwEtreDrrCrpqmQZMpUaGiWCcdUQyuuEsHZGvTvmCWAWpeYwAdjsj6jV6DwpnCi7fW1qnW2,1792704350,460187183,330,-5520000000000,5865518306,-18300311,5847217995,105000
W37,2SnfXiroJacWMZLryeEh6Gs2kiqrFYNXJ5aVk4ALyo5Vg793g1rnmTJytTNUdW6Wd37h7xdSGXBaHXxSteQUoiKq,1792704364,460187248,468,-10363500000000,-1503440,0,-1503440,15000
W61,55pvyvdvWJD6JdYVTfRAXDSM3PUF23cToFS7bKPuKAJTckayQBDoKHs6VUatkGv4rKmYAao1K5FjUNnp2hjrmMCC,1792704372,460187281,392,-4719999999999,5214313522,-16203212,5198110310,105000
W82,4jMbzg6mNKjo6NPjYd63toBM22Zezg4SZQzFBLPvRggxMKyJ3STGdPVuagNUtuGnpRaRgKAfpeA8VRQ9MvyNLx4K,1792704400,460187414,34,-5990000000000,5772226618,-10070038,5762156580,105000
W58,4f1qu8SRQ5bhTQPQyHkRVdYNWSDnHkMKgGXh4ya783JSv8trQzNKy82kmTgjBWwxBELYUpFGyPZrYHJY8hL987Ah,1792704420,460187507,232,-2510000000000,2574852735,0,2574852735,105000
W60,5XYjUGrqizMdoKDZhvyyoXVeNGQyzVJwHRQPMukqpoUdmHPxfs3173KPcpx3pGySrX64D7PewBtGES3hEBy69QrZ,1792704487,460187823,97,-2510000000000,2321361489,-8863193,2312498296,105000
W47,qQatBX8dnGN5hro4ZMYyGpLp55eX2w8S6dKR3vVVQNjpgpZHBnKEYoHcVi3GwmZBNXEeptYjycoXNZEibxixiyJ,1792704497,460187869,209,-1160000000000,965508503,-4869127,960639376,105000
W44,5rFNJ2sTJPoXvG4Eeo9EG6zPPU2FhixsxDavDRg8okdu5NNMutw8QrpAeEyfRef9LQpYNk2NDDunKRbdYVxb71A7,1792704515,460187951,90,-5505359299947,-1503440,0,-1503440,15000
W97,4dQjhjA3G7Nf9y6RiRFYcKXKKdNLz2oXWCZ1jzfUEBGFySoquLNTagtSnijcomt1hCM94YFP2w6AjAsxDpm9Wzth,1792704515,460187952,313,-4618275700052,-17000,0,-17000,17000
W97,5eYyUyJKEUhHyrLj7bfguxYEq5o6jVH3VhNHY2jgc8jPK3mBHjzW59KQuQtB7fWrExze9neZqZjFMwE2R3DRE9dz,1792704515,460187952,314,-277096542004,282376144,0,282376144,40000
W63,5oENTkWssUGR1Nk8DMXhTxfSLuMmAxtMaiKNy5d33eM79RZkjkSP4XUQn1nKzztTDrkxbr1379rc4k2GEzCeYfDk,1792704515,460187952,317,261480241532,-1351200,-272942756,-274293956,5000
W92,5KTTbWWKWqTRt3brWgaR4REJkbXXXowVd96bVNvj2PF6wJSjukQ3zwHa32NckEN2a2bpCgE6z7jWabLVMfjDeS6V,1792704520,460187978,281,-5000000000000,5013715079,-16931309,4996783770,105000
W92,3GrAgCEDsnfi9dnJfR28AnCZrBV3bMabt5wswF7DwKbmkxPt5HZxbzxazeQRPVEYYLpepUmvpTiCF8e5SFyw8zy,1792704527,460188011,155,-1790000000000,1913195602,0,1913195602,105000
W83,22zaKNyCYiBxtKXXDhV32Wz7PP6hwyHWCYgLqokR3gu5VunpFcL4VJHZMvCSjziexjrGGYqs9fsFAHqGnBJx1RMD,1792704553,460188133,210,-2270000000000,2337777652,-18001925,2319775727,105000
W74,2CmvCwjwB51E6nXjQ7c9NzZwb7nApgwPK1mvqE4NfM2VwNVM4iaWdAVkuSh12MPtemYq2F675m8QQp4KtnmBsg1,1792704589,460188303,364,-1400000000000,1220224417,0,1220224417,105000
W74,4aXWtEQxYZqehLfcAMWbyBceERCQVq9Qju1gpoNxffyPHgyHeRoJ1QdrJ9SQaN6QED9KEwjLKRpVVnNoYF66SKYc,1792704595,460188333,431,-1400000000000,1142495787,0,1142495787,105000
W28,5VFRLXU7uZgd9ceX1SGcMpKFhv7s4wLTSCMfuEct8VBLrj8WmZ6vM2kohyKD3fHaktsyB6fDhdnQEdV7tynTjZCu,1792704605,460188381,173,-1400000000000,1483188687,0,1483188687,105000
W28,2sns8S7AxipchEw2s8wMbxpFZLgapR1VjQXGtJSrLdMW3sYupvLT2Ro9osti6XtUFLRza19seewE8QwctYHqRfjf,1792704611,460188408,366,-3380000000000,3619344450,0,3619344450,105000
W50,5QMPNk4uQJy4JBFqAfh1cfdj3soeeRBfMofVQKgH3hxZst3s8SZPGwgK9krU2utaWMmxcDTBFEr6QGydvWpGUyXJ,1792704623,460188465,316,-3380000000000,3633625429,-4310994,3629314435,105000
W47,5FxxhEzPV4b5mUK8ywrtUbVaNLcA3iWiZ6pT4Hj9q3dzhrJgPAewHhabVeZJWHakYgNsxL7FmzrRniKFKMMPS2zu,1792704641,460188549,245,-3060000000000,3066960762,0,3066960762,105000
W36,49VsTFZkrP1yFa3xUuQeX2k7YME6RARnMQd5NhQ46Z3LSc9QEXDkV2ZbRGWNnHVtX7UYj5z3eNBXHHAFcGT72LwX,1792704656,460188621,165,-1240000000000,1189381352,0,1189381352,105000
W86,5QvV78f74tLhELjqfsvTRm1RGWKhsjVp83gCN72MbeGT3qpnS1MeDkdm2Ddcdk18wcjXki1kJw2Nsgf6PE1r458Q,1792704689,460188778,329,-1240000000000,1115831751,-7274446,1108557305,105000
W61,3ByhuLS6P4xTTnaer1x3A2PKKXBeXHNSmxdkqdzWvBRsR3bCbiH8ErLq7H4PXphXQqZCPhSUmN5q7d5YA4MUXwZF,1792704781,460189209,114,-5000000000000,-1505440,0,-1505440,17000
W61,4EyJP64dFrmPgNmKUEcDWTD3gpZFLAK5DCDQbFrTxE1a41ZvAPexYafPmueeVvjAS3EGdPG9pkVsdx3opuawZFW1,1792704781,460189209,115,-300000000000,299363989,0,299363989,40000
W96,U6cRtpSeZZR2oYq2P9Yig2iarjkwFnnQ4oaCnhkYscznwv5L5gu4Z42MwX11yL7FuMdZNxKLBbubbTNtWi9G5rf,1792704781,460189209,118,283302539452,-1351200,-289573223,-290924423,5000
W42,2NvgckTXfP6wjXXckxPjyccqqXR8HnGAFMNL3oNtBDrPdNgsAWnjaAef8qUXeAFWPHnLcbSKAebnWmBF4pBtqdfr,1792704786,460189232,323,-1240000000000,1087931640,-15405054,1072526586,105000
W68,3DdhoA26nUbDMvxqQ5z6UmQ79wfZX82UGnbeik89Vai1jRJqkn1BdncSpUgnPEoizqbUXirVVq11ZqxiK3eqLK4x,1792704827,460189424,593,-1240000000000,983278840,-13842286,969436554,105000
W75,4cmGsJDoHVpcJNP3HTj9UUswsKHQznq6RFU9tdA5sUxzES3hQHvjnsbinMm5cYbfmX9EAwJyETtZPMn1TtAFpNij,1792704838,460189475,339,-1240000000000,1087220704,-7707091,1079513613,105000
W31,4oaNjyuiHFjEzXmLqKPxS3XSd5Jxdg8qgzgrkjHDW9AgSdvdhFsYfJhiX4Ev3AYpuUFqZNhLPX6hA7MM6XnVACAp,1792704858,460189569,257,-1240000000000,970196712,-6850078,963346634,105000
W72,BEUUVJSpjKsXZjumA2zofKt3Z3f98PT6txuS4avcrvW3HbwHHN8pj1ZK2BZCBv8Qw492patn33Hv4oRwyoGwyEG,1792704888,460189711,70,-1320000000000,1070370573,0,1070370573,105000
W72,3SJ7J5Y2zUtBkeYHC812WmrCsQ6ZaSZ3MsqCU7PDXG8u4k55BbELMoe3uLEue7H7inQPyGWTRbwVBgSjqufsh9N3,1792704892,460189727,152,-1320000000000,1176679040,0,1176679040,105000
W77,273wi7gYHuVUS92bc4NgcT41ibJvLWPfnzi9dUHw4suiUBsYqU2rMPHn9rgdLwyDKeCmLhswY1uQG4gBZMRVK59Q,1792704901,460189772,158,-1240000000000,1007566670,-6921915,1000644755,105000
W90,RVjxUX3cBxGU4hxnNJ7XsmCxqonr9Qqrv8iRTGzjMHr11sAGsbMH4evh7bumcm22uTQudaiVp4frGjEqARjqgUJ,1792704922,460189867,19,-1240000000000,978233738,-14331727,963902011,105000
W58,4J16dvYbtvwz4Z7qec1pDbcpggS53kYj57jUEanFWooxitBE5U8dhEAufnyqzhu3LXk1DKhqt29sZbXWgdPiaUB8,1792704984,460190159,469,-1550000000000,1178231318,0,1178231318,105000
W58,5NSQqUB8c38GMrF8BeWzTU7tAbmxsGKfwBEaA6mDcFBwhzWKprimaZCmkKtCDbaGoWmAiALu98TS9odszdNhQTMd,1792704991,460190191,337,-1240000000000,924082741,0,924082741,105000
W60,4NrwsNh6PKrxZptvcArVQB6Nxz52YTKdPMeqadhpT5hAUmucWxytqv43w2xs4LAvuAvTmGc9beQZueus6AvsoCrr,1792704999,460190230,203,-1240000000000,887943110,0,887943110,105000
W36,2HbDm37KhpuNQUwEbsnsnos9n9S15QWdfSkPD35d5ngkNVf8AUtY8XVQH9v9Dn51CfQeatUJNkRmvCnrgRxcEACj,1792705031,460190383,326,-1240000000000,786644684,0,786644684,105000
W29,4GBPhuuwkiYvLM2Nq9QtfeqUKaFMwqeEA3wyHLZ8ibKonrc2ujMHWPd6aznMQ84XnCHLa5SGJj9Ms7rddD48cB9C,1792705047,460190455,271,-1240000000000,895126994,0,895126994,105000
W54,5ELnwRHB2N5krdNBQLrZtjzPkjaj1dzYw8YE7hT4Ao5kQvBDtiNrjUebtwh5ifZSH7pP8Ado4nErETHHoKDRwLwn,1792705069,460190565,91,-1240000000000,973165634,-11581915,961583719,105000
W86,4aJio6y7FJp61n9eNv1DwcShVK85E5WpZu5TWaCmL6HhFeV5hrBT39TpXXHigvb4m6scawdbRbyj6zfMv2qcjNof,1792705145,460190923,24,-1240000000000,881475496,0,881475496,105000
W83,4kuq2B9g699XCpkY7yQpXC89WHMjpgNo1aoh1pxec5tBVP7xwNhEfBmXU2rPZd1zURytZ4z65A5VYxo43zC5zTEc,1792705224,460191298,75,-1240000000000,985235349,0,985235349,105000
W42,3UdwBY8M22fWdx1qqZZi89Dc1ZC6ii6DZ9Ug1GsccPiVXB1QVNnrpABd7WdsVTj4zck7e6ZcqPq5vgRgDSHCC8Qt,1792705244,460191395,141,-1160000000000,919317717,0,919317717,105000
W68,5EivXrb96Dh9YgvkZLxabLoZvaVgDX8Ax2AiYuRMDnX8dPZbf5bnSv8dRgb3AWQneLzYhybNrretXwQjrg3FU9Qa,1792705262,460191482,37,-1160000000000,757977096,0,757977096,105000
W75,4qEW6GMzBYoSUA2poGcJ5trzuNRYRQrctVntxJ72uL7tjShYTd7beLza9pdxBykE2HAzDXJARy5kUS8gXM2fmuyf,1792705310,460191713,304,-1160000000000,784401532,0,784401532,105000
W66,2ad19eTXvXZfreqQQL3hJu3FrtpgfkZ67Wa1eV3rgurszEPmU7PWZVf2623t9i49ThNsUktYXDysb9JEfERybGSx,1792705384,460192053,102,-1160000000000,817525316,-12048731,805476585,105000
W46,8f7eNUhmydzSi75jnGftZTDLUjhMszJbZ7aci1LwwaF1yPFwdBMdimHAwunSSxzYWgpkvBRFr1nf6NWaNfZYxud,1792705441,460192326,160,-1400000000000,1144387351,-10786228,1133601123,105000
W31,5bvfAyAJhHyZNETscX6MDuKcdwCNrbGUWDaDeafEE8ajjbbvCASvEuxqirVMs3QetwLiGsVcHJkj9FVqUicEbMiu,1792705458,460192412,54,-1400000000000,1287292435,0,1287292435,105000
W31,2u598hHYeyBFDd2oZwiREDESynySYs7RQFk1octL2eDHLAjnt2ETEcQ9Sz3To1MoJouauRWuy76ESHcogbTa6RW3,1792705464,460192436,105,-1400000000000,1269758167,0,1269758167,105000
W45,2kKofS1WRtKxZAVpG6ajWEcgNwXtHSxfESp8BpQh3vQSxF2smu47BUwhp4DyWb6FGDrHBXVWcboTss8LhP93SJK9,1792705474,460192482,62,-1400000000000,1199662286,-9554265,1190108021,105000
W71,2zTrHnuWePiyqoNUC4pJPVwQPdPS5u74zGUkx53mxFqKbNf9EG93thPEUqN6wrpF6gUXtZaPQjwDcuwMhKs1heg1,1792705491,460192565,248,-1400000000000,1188862228,-6115393,1182746835,105000
W41,5KaNYBWHHBjsvEF4oVRRR7AgUtX93fNfcQ99irSiDQjMvPpdibfye658umY6LU4pdG3BiWYFyEGh41vyq5Hz5HRd,1792705503,460192624,540,-1400000000000,1119417233,-9367258,1110049975,105000
W67,3cfX2uiFwaCBRKW5iRQGvLpdM17RNxV1qqnWfEiQ3aAkfZGKvFomRn6ezZfxz8sn53cY3H1SbXV4miA8rwdnazaQ,1792705511,460192661,66,-1400000000000,1060676566,-9369231,1051307335,105000
W77,5GHuFXb5bLF9WwP3eZSF7B7ffNtjuGxfvD1Bwm2XWsbXqYoqoLvUV4daPCkBmy7YjbetG9r4fTcpdDvH4beRyWVv,1792705535,460192776,97,-1400000000000,1078866972,0,1078866972,105000
W74,2aPgzY3oe4AXpjK4KBVRMXTTAZdDfTg8xQpC6vrRcDUcdwiu4VGL28rp1sxrH5kYoPnVuvnHjt6yYjBLMHmBAsBz,1792705580,460192990,275,-1400000000000,1100877982,0,1100877982,105000
W80,YC7PgCHYtPefZJ659QGdA46cLw1cqTanpBFqYKQ4N56jLfJfL9SdFaqKLELPvUzZyEUo6rAk4ieh1RmKTQ9ZrpP,1792705612,460193146,234,-1400000000000,1201181553,-9898846,1191282707,105000
W90,5D1NEYGjVBfMzZVQhfrM1um2PZ6U19EDqy1iXdvTQ2k9DPjBdTgCPxikjqgxGBzZ3uyjjWtnsujVPjX6fGSY9pbZ,1792705631,460193231,401,-1320000000000,1052508399,0,1052508399,105000
W79,2UP6ERhD9umAMVzsgLZii2sNSFf4nMKbpCLTb5L9tE5Ac5HadMRqRHybGRk6GadJtHYmTLPwPiEfojBAcdBboTFX,1792705656,460193353,1,-1320000000000,945473288,-5061388,940411900,105000
W95,Nh2Xcx3PFbozj1iZWdocXiJuLNdoJ3gp8cAP9HzGJiDLu3xrreg2ViZbqPkt8k4t6Dv5x6fPSRo9zWqvsdGDDEF,1792705664,460193393,262,-1320000000000,927225532,-2847202,924378330,105000
W52,5cvpEsVuoN2sF9HrsVxB4ZG9uZHmeXwLf49mXaezQrWDLKYcywfP47a8yFfkuS2RLsqjyb5Q6LEqzTHga55BTs6q,1792705733,460193717,90,-1320000000000,911012899,-9969280,901043619,105000
W60,2KtkL2otzBtGxeG8NPCsvA2UDvt1hRP8BtQxZpUgwmn3hPShEwRGnDteJKaX4kpq1GxnEkjusaLE4kwtNbZJFeCH,1792705748,460193789,239,-1320000000000,717200662,0,717200662,105000
W36,4mqNLoPctxmouBnjn9oEaeW3zZv5PbMsGa5HXpemA4BptFbHWo6W6WYaVzrNaRv7iXTNcyfYoqq8FQFcN4MLZJfR,1792705774,460193911,81,-2030000000000,1123190712,0,1123190712,105000
W92,3PCMhDUGwNaMW7yM7btuxwrKsRJ1wto1JaSt8X1W9jb6EYNKCh6tTfg13fLfcX9SkQXqRHkT8i8PYc1p3W2hNxje,1792705855,460194291,160,-3077010238375,-15000,0,-15000,15000
W98,4yjbK6QaSGwB4mse4bBP8GSMGQ8mv27bioCybsXSak7Z44tj8anso5NqFtDFHzNJuLDq49KZN8VQpew6h4mcACjV,1792705855,460194291,132,-4877742482928,-1503440,0,-1503440,15000
W82,3Ty1mQk1YVk3J48bVAKAbhmxGU6nko3HV2ktwHWBL2tNiDMV8DiAYgyfXWsZyLJdiXpWYAbRdb7hq3cYtcFyJE9u,1792705855,460194294,195,-122714836722,56214709,0,56214709,40000
W82,4GHkUvYLhPgN94YkdgAvyT4MpuS7hq7pWDg6Tfjk6sbuvVGYiYUvU7YB1HoK4UfYJLf8W4Y77dUhFhpFNUsbfP2m,1792705855,460194294,194,-2045247278697,-17000,0,-17000,17000
W56,5Kp3gw11apV3vXinVJJjSvF5gyX6L6HKVnQkcZFn3mnitS4JcVzTuaVFTaDPP1mH6iAnr94sGyqsDahMejn937Ue,1792705855,460194294,198,109759248086,-1351200,-51534597,-52885797,5000
W81,4wgeFscPLVqnBVehELn9q1M3qWCKt6J9kjiha9umBANpurajJeyReGt2mdGP3tC4wAv1fAEy4wUEyUfAUE7CiifA,1792705858,460194308,222,-2030000000000,756970347,-11020318,745950029,105000
W29,4ujKGATbSVzzQZ2ew1yqdWruNGmSQAYYTxSa76HRWZHR7cmr1N5nKCNjQ7rmtzgWQQbmffgc5yo2EddbPvzEf3Pk,1792705894,460194476,29,-2030000000000,600793029,0,600793029,105000
W54,2hsZwZXcfVCfhLub2igR5M4qQSxaUqYe5DsKeFTHxsm15ZCoBfHFZgxSAUYyqWSdWiL6zWkxQPJDbRy5ys6ACCaT,1792705942,460194707,112,-2740000000000,788260335,0,788260335,105000
W57,3KU1vGhce8J2AUebW9bTVdFozoXcJhdMKcfmT1axxoxv1xUvEhQXUaGkNGNcBzmC8TrXcRxFtdGBakJwGaxYC7iU,1792705957,460194781,456,-2740000000000,829680446,-5001142,824679304,105000
W86,235ruWLiHtrJDhzAySnDJBDuwpAnkdnEAZzGoUxnBhsL2rrBp1QmBdCHMzexZmPtZCJ5kpX8fMdPE5vT2kPZuCBU,1792706059,460195261,187,-6297587821056,1362849003,0,1362849003,105000
W42,3PnVZgWSVYAt9q7iZa4ET15zpwva3gDHy8uRdLVJXq3jKrb4tZvegptoAwfPoQ7XnqrEVyDTuVMAbgQmWioJVYpV,1792706059,460195261,137,-6286898867842,1492317192,0,1492317192,105000
W59,4fBg2dtaCLA3qgDjAdqLksUycfqcVUTcWfzA1JJjvQCCMNdW3V25KmNRVzgdAkNcQ5medmU4hcf11cxYCjZpbhAQ,1792706059,460195261,139,-6166185895678,1405921090,-7616177,1398304913,105000
W83,5rY7Jou1ywYvWNLSYeB831gtUnSR19bQF9fWzsn3Ji6Ng6LJQX6GnrQ8zqEdN93imLwKoA3mQvYhMaBFLrxP6odT,1792706059,460195261,118,-6249327415424,1556618982,0,1556618982,105000
W76,3RmjQY8rGREVBZ15SwrfRxSSWiy6p1Fvapbv96ot1epULbFaRviB9xLnHcpSuWZY9PESSwbcv7cCLJLK5nueH7p1,1792706060,460195270,182,-6203497612468,1246281014,-4304780,1241976234,105000
W91,44yLYyLf8w5yUbqwhs1FYyie7sTCprX5N2AcvBwPzRNQNBqfAhfi49gPgZucm9Bs5W1XQqee3FXrL2FTSjWHFyHr,1792706060,460195270,188,-150197151404,35402827,-4640084,30762743,105000
W59,5RSbSrJ5bS1QjpFctLPBEdGiJViPcvtJG32nCZpK3svT9FKE9hERCS4pJ4Xf8Gvd57hs78iw9gPmdzfyqUBFgbZ9,1792706060,460195270,194,-66488653398,12890800,0,12890800,105000
W68,onvQwEACWssYsnMcrR2LD9UAXYZDqByDUQ7S4YK1ZqJkPEvjY6Q1ySeKpDCRgH4sqQXAFqzvhcdxandGLtdXfWN,1792706060,460195270,198,-6231541690327,1192031772,0,1192031772,105000
W66,2hbxi7PoiRSfPixMP2C9CKA2DmzMrtwxLXsCrcQf2i2eyyPqtRVSqTFzuke6Q5dSJ8RkQJ3Az5a447PixmYvdANy,1792706061,460195271,306,-6173048415417,1084839126,0,1084839126,105000
W75,faPwrQY2gugHg73CRQbmH3pGmfeu5n4FMWFQwqVRXcPfPvCRRcEu4FnK8EoSue6Y5CP1xdymKMEEvN1J6Jggrhi,1792706061,460195271,10,-6175226476986,1132835606,0,1132835606,105000
W43,3R5pA7QNM1yxPm7oVjiPYXfcexLaGkB7huYnQijtDCG1Y4Ni68YxFfcjqv9H3mSauK5r6jDv4aZKdpigjcernmg6,1792706065,460195294,31,-1280880635483,206380478,-4451292,201929186,105000
W50,3SBqVTyrYe14PxtfJrM8RLHgEe83PxWHMjCjgqPJubJhNpixsyKNt5QPmQTBuCALkYJ2Z8B1aZJuSmPo7NQjJ44A,1792706065,460195294,14,-5916319588774,983211629,0,983211629,105000
W91,4d8CNtcKWmNmJ7EbTjtMen4yNmQDQ2LZ2yYDzDNeuiypAerVb4q4SDXaZBWqNjA7hUbPfF7oZ8KKmXu99kE6ZJLi,1792706065,460195294,12,-5922509605593,1022337306,0,1022337306,105000
W47,52guY6QuVr191fJor2e7Z3RfrrraYtBXBs8CiBJdT971SGwWu4G1XS78MuB2MmMZchwwVCSzofbA4L6ZgLxQEtpS,1792706065,460195294,43,-5951165604371,911294777,0,911294777,105000
W46,QbhGM7hEDGcuJWJGrJt5WBKdsTre7WmkQiZRgo4fVUqMgm6wk4Z5yRi2uDeRqvzbk9qnP7o5GobRkGDcAbw1Rw6,1792706065,460195294,19,-5929124565779,949274110,0,949274110,105000
W65,2wDAoeGiShkKAuv4k8yYocrHR9xAHzLtp1dQFJkKb2Eb4YzjU5Chou8wAk2PnBGRhp586oAqxJmXFDHrG5AE8we2,1792706617,460197909,30,-5858651836896,316650463,-7880842,308769621,105000
W41,58cvBmJ8BnPj4c7K31JuHXf83tb5V5kNZM3pppsQUw3xZcYoEKJ1QRuMfPPRzDV1zTqRwZid7ahYZ7sYNSvVA24u,1792706617,460197909,51,-5708797713034,287355308,0,287355308,105000
W45,yYMvG3eCi3za6ucn7B9d7f6FGgs2BhLWD6e8RZKAztUD2kBhTZ9S3JmrzheAkpfAwyn63XYzK7ruQAAqbtCYhRG,1792706617,460197909,50,-5852341701056,300631765,0,300631765,105000
W30,4NQkdAzDGPAnfgypRddY2mg3Zk4FBB5twBmUzKzCJHLHKwFbevmAXPkuJdbbNFRMx6FAKwgE5NLW5tdbVzTKTF76,1792706618,460197914,200,-5685423820389,280649280,0,280649280,15000
W72,xoUGW6hpexawxxdnrtqRjGQ3FLb9FoF2pMZjcvtVT6LCyobvkT3gE95Vp4mNCEj7KkbocvXEyNDKnYkwNDa6EjY,1792706618,460197914,291,-5844770974531,282841914,0,282841914,15000
W74,2epN87vJaCKj3yHGUEMmr1ABYqwMoWNZ4KJSpnxkmkpSBpLDhfyUSxEccXzqm2YCmpoXUBAAZB794F4UML1o1GdY,1792706619,460197915,343,-5469523956921,245224183,0,245224183,105000
W71,3tpiPEFHPZGNhn3QQE8t1452Ckyh7gRHjVjGJ7apjFkcs4zi3eijt5cdrUyu5STHrK4qc88RPpnNgixvRkNnfTSF,1792706619,460197915,108,-5800721127798,275189411,0,275189411,15000
W84,7QrGfCPhUo7id48AwG249sEssb8Jdj9r2tPjEcMcHexdHavN5JbmZmvJ2TZpnUuPghXDtEsSQhEhNRMDTCyBAFm,1792706619,460197915,338,-5456283865757,257348298,-6756928,250591370,105000
W67,YuuDWZ5q2v3xNiFMaTyuLKSkxPZu19vhpYLCtCN2rhP1SSCPxsgkvfBxLgJ4oB4odqTSq2qQmxMQeg4FJJqbn3K,1792706619,460197915,337,-5677215662185,264068808,0,264068808,105000
W53,dX9E7AFjseogZV2Xxc3xa5bKu9K39QuN8gN21YL5xZkZGJ2Loy4QvpCbc8c8SYLnzm9dwXVjwBeRss4hvtFJUCS,1792706619,460197915,346,-5475985298843,249565894,-6940234,242625660,105000
W38,5QCy9UrfKASm2DwxMF689gpNpGocjV6NyJYor6FekA5HuWTrRBwes1x2z9PxZ8Jw2pe4vCqQPgsFJimM4yiMWscm,1792706619,460197918,285,-5493835208791,238105467,-2144447,235961020,15000
W90,2pAX3FMnMk1rYPEhkbB8548fSykKMGeh4U35QphmGVyVeniW8vwt3KEE7d9kWQ6Y5hbJVZh1qEZgmfgsMzQSseyc,1792707944,460204152,51,-5442839070096,187532073,0,187532073,105000
W80,3BPvzSWRW8jQpkgHmG2MZ2zkEimpCGoaJhX4WEvVTyBGv2BKtdBtEehBwMkReSsAixotFUdkb7z7vBosGRuvbcij,1792707944,460204152,48,-5386916083418,191661890,0,191661890,105000
W77,426LQ7QR7diGVkXJregudZuhRP4rbpfp93vYMtsahkKFGryBHENFHoPNscRGGKjKfLXyuEM7FDPxNdPiK2x32ec3,1792707944,460204152,50,-5591287407176,195763807,0,195763807,105000
W94,5t1Yr5cS8E5hG53eF1GnQetopmL6DZFUPpvRuazPRHsaoQjAZDXZZBg6KyBx9JvufcEpgzjuvnQt7PDST8LWxJxb,1792707944,460204152,52,-5354463769945,190476050,-7352017,183124033,105000
W95,5CHtXKmA6JoM4yv3iRjzV3nZkJdgocfBmJszQ1RgLV42gEjtozWFjHkv9kAZPZ2Xupzqxdt1mizRUCFtdhhWy3mx,1792707945,460204155,67,-5370140089960,179232725,0,179232725,15000
W79,5nXFPnD59w492kNeyb1t7B6eMVh8tpFxWZzxorNYw1FuF5bAYRNAN6pGjVudSJijBNf6KtT8kiPN3rGQtK2w63Nu,1792707945,460204155,73,-5437847475969,178732305,0,178732305,15000
W52,3gC5cBjACEsRWCGT19meKWyczbxJ8qGdwPzkBLuLq25Rz6AXeoTnucyFr8iKcy22UUBAGMXAS1XpPfQMMCjJM5rt,1792707945,460204156,79,-5305103971559,171662338,0,171662338,105000
W60,3Ro4VpGJkqThZkqANWqmQrwQmYyNwS7TFaK4u2bzjsLG1KJ1sjcuS3bnENDz77w5wYD7zZzpvv48gWRzmGZaQWaF,1792707945,460204158,311,-2111402131877,67641426,0,67641426,15000
```

### C. All 72 preparation entries

```csv
payer_id,signature,unix_time,cash_lamports
W25,LtxaaNxL3RPCf9CrLidTy3WHaNKkom6Z4PvnfzHtP15RfoXbcm2oQYos9uGHWALHdFX8U9nYSfM8mvGJ9HgyJzH,1792704045,-61691542
W25,5xCpSXrtLD8R6cV8rzf4b9W9BusxbDj14no576qHiHXmsaJgqtuuR48NZK1uFphaqSP9GzRMgFgwGSrpivVbNTjr,1792704060,-9142502
W04,pb1Lgmw7bksYjxNFr5zH7Yq4hXg2cHTiKJXVE2uXRZg6pGwosuiHcjv61nn7fCKHkS248J6eLwHvuVbrbM6QUbg,1792703776,-43238557
W21,4CAv9yngtoWtaUTKdqA9fs9jePxYm2RewVfsDUwR8mZu4zsa7Lhfg3ZaykvFBbr6kqy7f5QEaxjrKne1vcicG2eX,1792703842,-37625492
W23,3Ycy4LQrJMNUViDBZDEjy7zXfafhRzyCUar1WDdTkkCbggLTjajLxSGXwN3EYPwc72sauKNM86Xw23cFtHpLwZ9r,1792703893,-29562849
W11,5cXXk1mWUGC6tA5dQtvNLVCdByxWqA55vxEqtYF8qssKTMFzBWbNgXdHZs2erZmHxyDsbQVapQf4obGtUW2pS61Q,1792703935,-33338233
W06,4Hiip5pNDNxuqRxQHeadzx5hBbYtVn2mAnERizExb2bMrhQyhtdVBJahBVvQthJwaQM111qofVACV4KyhxvtNLmF,1792704132,-53791324
W06,4iKR8KrWq3ctzDugvA7FYV61HZFQpAR2aeRA4okfctEUXGvngc3hymBAWf9tiu5w4fGzypqUrDAb49uStgMubWCX,1792704139,-82069590
W07,DMAjAGkcc338FVtkMZdYiwGmyiDsobHQRYD8m15jKYgnpLxJSatkZMGwRrXxZCPh4no1gyJ5U4kn9pErSTjRtRJ,1792703714,-39546971
W09,2TJsaPiBB7Vj2DMtZGJZ4R2vWFAf9xtzdXCfR93vUMttji4A5BPpe3aLo2y9o8dH4Mv3xZ1jpM3NaQAjLwPy56eL,1792703994,-64102436
W61,5XkdzmJmmGPhpQ3hvcVBFkLqwRmrVUbKfsMmsoNQ7cKFp5po3urvirQwhBVnsSxVuG99bmMRby8tDUCoiVim4Poq,1792704781,-6011904
W17,2ethEHNkiabudy3sWRwaCfr1oafsTo6ZiZEvjzKurHJAzQuFGZ9SfDXxGXtYKYzotV9k3ESX5fZ7A3pSpRdMoZ5p,1792703957,-110727330
W19,7nruYszW53HqkAqEd6xB2qUZ6g9XURd6eWVvvRqkjCahkgZhtcd34mbFjkNTDu5nsccshoHqmA1caXg4EQmHZmr,1792704016,-106304801
W09,3MgG42eTMAGgQpdmT5K6PFwS8VuVQhBEQ1etvsAhQZpKLxo6jhFDjrV61MCkG5Sm3kpZ9PFnDNrwbHGMwKJMx8mM,1792703987,-66178254
W10,2ppkpheEWEwv2UjYC8nmZrr697zCTwXFKWM5JENZZFWTpfwR13dcLUXCcuBB4acifAALivzn6mmX1QtMSJagqkMV,1792704067,-90996808
W06,2KXppmHx8B5x6kySMwuPrAGFXDuxXB6hRUMdRvv73Mjg3VGJ41aL28Yp1RwGxU9wvAV1GD8Pw4xsx6nXwXPxkRKr,1792704153,-25711146
W04,mYk3NuNmY6G6qibV9EstoDpYv4emAwi87At2HueDrd9KX1nWiG4fnUmx4pJ1d8mjic9MWbC65KNeSEU31Kg3xFT,1792703799,-33047832
W26,5NDQpaUm5h5E9Hkarv2vwtBDoiywmL7jnMyj1GURnUR87rh1NZaiSokozDiX3sQ1m34o89bvHDmD9JMUT4TAEYA7,1792703821,-56590425
W22,6SP5DZgJJoj62Md9bQTKD9gyCN5Zs7GEpVSpf2CBruVoppdUAqxU4X1td8EsYo3yhxG5i2PXeWnt6qBgpeFTXRG,1792704167,-90343284
W21,3AiwdFRiHr47ZR9c9SWw1GmBhk2UkgcefUgywB6YQfGRRP4Rmztjkpg4bv5s9wD2FitgUd2eq442GGzBEGgcvpV4,1792703850,-49237938
W19,2wH1RWQQVBfAenjxUsDsW7fe3GCK32PeDgSaU5zKVtYTnGgVYnbzZ3eB4YsTnZsBWced5y4r4jiLmoRuaGXA9sF7,1792704031,-22671663
W07,2gWW3ZfS2q3rBxmmnEYyJETYQcckdZd3dnwkrYo7r2L6a3rKfLUhonrYWTc6y4SNuydd9nt1xxPz7U6rxjCdo2xa,1792703707,-32031471
W02,2Q68QRkCHWL4GGwTDufUs28rzBptmcwbrxxSiGowZTSGhZ7sFir8SsX9As76hh5LiVQPLtEJu7NJR2uALn2wCfhf,1792703686,-24062553
W26,4LUZsVFAZ4TFTnqjpuTjxHavsEFaafHxy9RTB76BqZZhHTFzTfK6upj6d7Sg36CPPRA4WQdkazUeaZD2wPQ5ojWw,1792703828,-62610848
W17,3CbzXMF2sFGiNgtBbtMAFvTo51GfTwvJzquYzxstH9wyu2GfXvZwhbtE9HhFvEj2p6SoGAF3btsitMxWEPEGbnFo,1792703965,-52700127
W12,3nMBAdYTpbTjAUcW6RmcAD1SKPMx68DWuU5rpxdN5cax8ZQiGYMFdNFHyiPmifa43pEF9CSoB9J6mnHnE7H2wGVL,1792703762,-49313119
W10,h2PDzP7qaa9kc5hJHmfQvsLNpBLZmwiQ5NNiKkFfEs9pkb9mtUXpc3R5VEaDf3FtpW2h9G41Y2qdGNMRxTFm6t9,1792704081,-86911565
W22,64ZawyvreHNVUFcbQmv1V9aHN54AWHmHK7FLLeXzJh9i8e8gxtGf2AeiEJVo2z7Gyxna3vNho54K5cDk2fEJyoCV,1792704160,-68283350
W02,4rZyfGaHTRYGCp1WMmc6Q1f6Jvt8jhRmo1BSJnaVTGRjdgou3HKTDboYCztXbFu2UdBANTSQCE5rCqg1T1LeX9gw,1792703671,-15688538
W19,kAUZ5REMPkBGiBekm6WrvKHNYqfreJGYTih1ugnynUwbMtw457TEpvY1EarQmVD2HgXy3s5PQBaLJ2TVStKGpHu,1792704009,-37606759
W21,TV1AbxFofU2WnDzFrjPMaLeezAPjN4QHir6PCNRNXxHvuiDNGUFJQDkZConrtsMzZuKbdPqCsnofQxQ4U4heaqM,1792703864,-43754880
W04,3T6MNVrqz5wgZjoWooCZKEayfdPi9LmNxsYneuRi5DapX9ShiWPQ7jaqsEs87bA7uSQx8d7v9JJnEFpXMVX2Ts1Z,1792703792,-46724318
W82,4jQLguqmqiUMWDYrGoKgXn2E9sjTXoqigmF6vgepxTQNQ8AvNNYyPPx81mPniVddhGvvKYpSaaywcwJTHpRjctzX,1792705855,-3580411
W13,3rPQvHukLEdDw2mfuMj6oxCmXU5ZksjjmV7EE9pZZV7rGWKn2WsdPDqe1W4hF6xQviPr7gzb3gVxTsQ2pSLW26Mn,1792703972,-73486289
W06,5zPk4Y8HvWW4hSrgTCkWBQjNC3p5AqpD7TmxixoB9Mi4YJHHZkziQDxVpPV5wckUGcNhY7jKoFaQWyKjp2c2rsM,1792704146,-43625669
W23,21zLDvQSGNL2UiU7BuQu62pVLeKJXJ8b6PLFPMxusnwNA1Fe72BUnxvQ2BtLAT8ZTQ4ZHb16VPUidekRxg9cfFta,1792703900,-29163621
W23,3LdgEGmSxxCLT32a3Fm5ECd6B3Z3vvg6Ag1zAHsyx8RmXS1kRA2bE9mBM4Yq7LC9khWNnDr85huxd3PzpoxY3i3o,1792703886,-67520748
W09,25uCQKbdwnAb65xkZ8LBnKiTVG2rQQuZVzKiwgZiJsXSPN21Hr9jM4UZ2QPPmLs8x4BWQ78S2kydAhqZXEsa8ugx,1792704001,-39650228
W04,FrYRc8qWLD77CtN1s15nriRgnMyVZdud8Gdi8PBuX7HiBHosVV2RpcxUhswSzZHjputUUH4chDvNSWob19tmNzQ,1792703806,-6407090
W22,2EW7fditrUbqSWtitiiSBxYJefpDDFoh5g6KngVe4yU86f5PHy8NoPyCoGBUDVvAUEw19w4avMK4CS1weh22bgYE,1792704174,-53438000
W15,2e3Ar5MjYSYvBLmP79Zo8nvfF9oouJQt72HfRv3sxiyGgBPTD75KXFq51aZhX7qanpgqQLfHBceY22Y1j8aQxCAG,1792703878,-51768965
W11,6tJt9mN92Wz3Kcrj1QvSqaFMtwewmeZyCwjX8g5P18Px6uZqbxY4R4XAukc68LV4FP5XRtT6s4E1rPWRRE94HS6,1792703914,-35519612
W20,3CcAgNXcv1co8VnDbNEAB5hLzSBRwCcKwyHxadv6fXhCyzi49umywsnHKwee2zgBMipQucUYGSgarK1Rq9VS1bd5,1792704110,-48636994
W24,Usivx6eeCqxvTs2Ud1RwkoPvhF65KvwvZT5YyWKVyZ5MRFP53RDy3Wv1cLzroy41pmL4F1uFpr3CjgeFKUGzCQF,1792704117,-94025517
W15,j3jBxrb672erBq7EMwKgzmEKVriqodDPqfWLz3tCjFrEsbavjvbWiE4BPpMXBZbcvBv3Uf76LRLDPZvfc69Bn4L,1792703871,-72104465
W10,gLKCcTjwTXhHFT2hV6NtLsLd8UvdU88s6ohw44L5PjVWnrzyWmkiiyrNN1x2u8mADBBsXQJatocRWH3Lw3QgVL8,1792704074,-70737953
W02,4sXEJj1SmXLTyZtBvWrDsrNcU7JGMQKxnRR2EUDpYFrWGp1qDVjU8wneyCRm5KEqwUyVoWbtiAXXnfoek7CCecbM,1792703693,-11159705
W20,9wD2RAjNZKcPiMohypvPpjoHBN4qTd8u1nbes6LPFyvQpp7tSkKHvMJZDynpNqVbeayDjos45x7MjybCEVV6MGD,1792704103,-74859727
W10,63GzVmb7Hbb3G7G8PVjzRaBDcNwhdFp1fBxYy8X7iF3BdRVR6otTDDMWBxXw1n4dgR2NahTyhx9hJuz68JvHutDe,1792704088,-37542268
W12,3H3Six5JaYtKTdyQD6bFW5M1hQT2iXaeBJHZcRCiaG756BKbGDgj1rz2tv18Js7BBeDDzuySRKSWtRJCf4sqY2h3,1792703769,-27225471
W02,4SRLr7VLHvhbD1T693ZoSxbpUyJSyXziherhvcm6qsuihpAWH9RumeMAnEu7RRVpEFGSu2k27LbNMcfJXiG8ASPF,1792703679,-30894552
W25,5CRByfUJV2UHubqJMcoJWzhrwcTXvzj5WnnAHxWzohzLb8tJtCJKWVF4QR6EaMHPAgwUXgbwMWNsed2dBjmR3JDQ,1792704053,-96200889
W26,3bPEtSd2cJoFYDcFt9rqQsi4qpQMJjziU2yAPw21fY7QGtwPLZMoUv46MsvJhRR5Tqe9NVP92PA4qUWxtxfZoT1m,1792703814,-37721354
W20,54NnkwMFgmUkhyWjrDndPXhwiFghzToLMCp7P9EuYbE1Zzvozd8J2wF9o6KNC6Q9FoF1FWckiwMU3VBymj4oST1v,1792704095,-99769472
W25,4T2usb8MBUzxP5qQwTPVDZPcuj1yGNoQW9L8d6yg8M6UBbpWz1M3HZxreU89pxRavTV3K99s9p3DSZVfyPnN7hxF,1792704010,-8584718
W13,59pprxxbdh5a1HB9x5EdBy11QHF1vmxVev22NS24Ss81Y3KC3ZhtoBZMt56iFMttfkXRS8TJVGDL3oQDehLdAAb1,1792703980,-45379726
W04,5CHM3F5SngqnfMbgcEfXqfarbvqEdb4UDzPdfbSjFkXeEmDtLjzPv4pNEaL9rJaM9to8ZPJ7x99Gw23PNzvCfh9Q,1792703783,-19925306
W12,VvwjG6b8oKiVPeiWbJgjap8XTaRdahTwsQFHjLEeErH4H1LgMbkAbfSpM1EZ1TEZm7giwsZ1BqHRiYXxzRGeg1T,1792703722,-21369531
W64,2B7GBZXrUNMWgTQ2aUG2pyM7JvKqfw6KQw8tkNitFsy5eGRnako1hhhQ2GoMnsnFGkYve9mQwZwnY2YFECNMLjjA,1792704250,-9043282
W07,4GmGfpEt2AtzKMf63voRF2wyK7gFSKt3SjC1JAbUXTH9M3odqw9WTYrecZLBphXCi3GUqoSFd2GUXwo9dqj4jbQ9,1792703700,-32847787
W21,3SvFSaDjKiawMMqwjqo2qkqvqktvrARGUJDnUSAsjH3BGNVJEgDeD2N5TXDmhLnb9whNGUBJgPKHHF4oUa5pv27N,1792703857,-47665163
W11,8bFsurq4fydyfDr9V383pCtP89tWfR1iwFWJhPfnwxtVEbMfmNksfZsN3Y7XajMAQHkWkQ9RUXRxopweHLWLhUW,1792703928,-59076701
W14,4gAa49cv6QnUcHFP4dnpXkWJ6m46bRjZ4H6VhCGQ7FuGjnFmY3BBgCR9t9xauB2jGftvXgK1KUqLpPzXjodXUetm,1792704038,-62325039
W19,GeWsBmhLck1nXwqf8dYhxw6fSbmHzpn5Aoe7H8bdTtMNacZXnBqQQzsEMFGCGWJSdvGwAuwk1tvPqrvpDaLjT7c,1792704023,-34699967
W24,3okJwpx7zbijfmc4FuqRUDVo6nUTgLjVtQBdVHXLApR2GCAytZvAXKR7jjLF9MnFCD7em1D2Djwvr1jQ4afLnyo3,1792704124,-100993839
W97,3yZpgSkrKFuMXdEKizH8cGUTkNwMHZM1gU8ga49n7X4EGRuXLZagPLoEZzRoLYJt4d1hGD38VuTuCZZgsJ4uUYYG,1792704515,-5842025
W11,555MTDK4RLLkeTb1EeVXEMGJJs1Vrr4HtJCaC1nxLLiqKHXwHbGUQRTTJ7o3q2c2wK5mynEzLR8aMdKCFzRhnfkh,1792703921,-32952688
W02,4gYydYM4dzmKSQ2Wu2Va6JGSFMNggQ2uGyGkMxevUHc7T7mk4BC2EmEe86rSEQ1CJq2jBPHmGxcS1vsYrY7xuxMy,1792703664,-21614539
W17,43msJxqu77sYsKHnXNBYWVL7wZ7vzQAMP7hfyuE1e6EBjTkFTUCHTX8NV5U8q7GZNRWDSmbK1SvTmZWbAtd9Uwkt,1792703950,-62298278
W23,2P3rdQDnBqX1ivvA2PY3W4jjhTZS5rSoox3tXY2CKQ4ihiVHbbopzSUtSUHTryHuGmb3FQCQHypycHP2fBtcpQDk,1792703907,-47072652
W26,3DWBHBxNbBZFuuFyCwBG6pqM61frxtL9goWhvtvt92yhLccTgmzEUNFCuMT7mAL9ebJsFSQSMHR2A6xdFVhTEYTe,1792703835,-22550136
W17,33idSWpp1hwYs6z2SeLGaSfcjYksCttyRMsju4QjtMibcfGd3wH9XLJmaksaV661CocbWJKHQum22a1NCc8C5KS,1792703943,-47485540
```

### D. All 75 funding records before first buys

```csv
wallet_id,source,received_lamports,source_delta_lamports,unix_time,funding_signature,first_buy_signature
W01,Hg29Zv3GY1Bbp7JQ7Lbawk8e3cLDs67EKGifT1JUUzL3,931677825,-932177825,1792703161,57Qr2qZW6nCQdujAjDeLNhtNUGGjrcZ7c6SJxmn2JfRAPzpBBvcAvauA2DiA9dRaXnLDGJ6Sni5KYy2ao89fw3vn,S4Bn9DB515KSegkgevrckrauMih76e4FCE579ZmCu6x8fPk7F6FQKtJeiKN4wxdcKHEW3vtLdfqG1N7EfcmkLzW
W01,Hg29Zv3GY1Bbp7JQ7Lbawk8e3cLDs67EKGifT1JUUzL3,1156179651,-1156679651,1792703162,62dgrixrVBYdRoQvTYafzhc28PVLbGZy9kveFBVYUGFLXpzjMQ85BizkHj1YnHwchEfJcwVYEa2kap4uw4qgsXDJ,S4Bn9DB515KSegkgevrckrauMih76e4FCE579ZmCu6x8fPk7F6FQKtJeiKN4wxdcKHEW3vtLdfqG1N7EfcmkLzW
W02,Hg29Zv3GY1Bbp7JQ7Lbawk8e3cLDs67EKGifT1JUUzL3,1300576109,-1301076109,1792703164,3XVPP81HUm4LtXM8gVZm2SzyYcPnTzeKiS7iWCtq46RyfnNn3F9xcaubhbkVSJpiPhw4vuPyA9qCfoRPnaMpZnGT,59rkxLSEZH6SpV1syk9y7pqASGSjeF8yFmKwDb29sY1ZciJ7jFrmW1WgRE2RfoQ8gcwKD8yPkPyPpXbyJ8ognMN2
W02,Hg29Zv3GY1Bbp7JQ7Lbawk8e3cLDs67EKGifT1JUUzL3,969026218,-969526218,1792703219,29mEdQCJEoC3qKBfYXRxqjwvgfAPvdxhPHMbHALe1judvh94JStdqghojJmSQp4vrKTVqhpZLWJiSEWopkadpoqx,59rkxLSEZH6SpV1syk9y7pqASGSjeF8yFmKwDb29sY1ZciJ7jFrmW1WgRE2RfoQ8gcwKD8yPkPyPpXbyJ8ognMN2
W03,Hg29Zv3GY1Bbp7JQ7Lbawk8e3cLDs67EKGifT1JUUzL3,1073182734,-1073682734,1792703164,5aLkBzfcJhRiEuEUynpP4cr2cpwhTk41F4ozmNDcmwBwUdgpsXviDMRnAdUj37cKLqwYhVGGcE6TH7WEfVdvZXJf,48cNJCTefPoP6mJh8yE7TLmqPd8gEHHe5gtCu9iwPps5XW8MPS4uXYKXXRyDQhHNW7Dna7hULhehXh69BLKEy8RB
W03,Hg29Zv3GY1Bbp7JQ7Lbawk8e3cLDs67EKGifT1JUUzL3,1069977168,-1070477168,1792703161,3bxHcP6rLBVC8ZW1SYy9ZG39xgVPWvWBLJ4hUWjXsTstJz7T9LCqam9VB11B5bmsMtAx18ExWzsmXEy8XyHoXUMb,48cNJCTefPoP6mJh8yE7TLmqPd8gEHHe5gtCu9iwPps5XW8MPS4uXYKXXRyDQhHNW7Dna7hULhehXh69BLKEy8RB
W04,Hg29Zv3GY1Bbp7JQ7Lbawk8e3cLDs67EKGifT1JUUzL3,1183636695,-1184136695,1792703221,5RmqmqEZydcVNL26nnk7RMP9vWBPKNCRNfTqiPT6FQJpVcNYAgpfZQZ8UQRAFbkeXQ7ivkiAvDMMBJsKMdtogjB5,2YpCR4wGKZhmGYrDZ7UEYy6x2wFA7j4F5pjRyPehSuBVmQ4VkX5WLdpYzr3oV1NRmZytdbxwLoFETtknhae3GJpX
W04,Hg29Zv3GY1Bbp7JQ7Lbawk8e3cLDs67EKGifT1JUUzL3,972443356,-972943356,1792703341,2vLn9RkVkef7Mk7BxMPWbBen21cTJMPvnkbUv9H93B7FbAa9DtEp9rqqzDdTDKghsdKDBRtzceELrN49QnKEBdMQ,2YpCR4wGKZhmGYrDZ7UEYy6x2wFA7j4F5pjRyPehSuBVmQ4VkX5WLdpYzr3oV1NRmZytdbxwLoFETtknhae3GJpX
W04,Hg29Zv3GY1Bbp7JQ7Lbawk8e3cLDs67EKGifT1JUUzL3,87578533,-88078533,1792703252,7SYUwBfQPnXsBEwoaFhgezXLywzohvDuKDe9DCybx185RrqmZpvanH1jmujv3tfbJVpmtLHCGMArk5B1s7iymB7,2YpCR4wGKZhmGYrDZ7UEYy6x2wFA7j4F5pjRyPehSuBVmQ4VkX5WLdpYzr3oV1NRmZytdbxwLoFETtknhae3GJpX
W04,Hg29Zv3GY1Bbp7JQ7Lbawk8e3cLDs67EKGifT1JUUzL3,6075808,-6575808,1792703236,5KuaGc3PsXGqhaKFdXyp9CT94eyQrAvpJjFR8nUgkGqXjMsGfXYxPsG4i8zeEm6CKn4LJ3Z8sNg3SwHgezNZYSDQ,2YpCR4wGKZhmGYrDZ7UEYy6x2wFA7j4F5pjRyPehSuBVmQ4VkX5WLdpYzr3oV1NRmZytdbxwLoFETtknhae3GJpX
W04,Hg29Zv3GY1Bbp7JQ7Lbawk8e3cLDs67EKGifT1JUUzL3,1103613742,-1104113742,1792703574,3WQmHzh36jvC6dk5zmiJnuZ5ZfZnxNLcRjEoK2v57TG2AXQqudtJ5bdS1Lw7FWNSULkfHYHGidah8QGcm5jmqjex,2YpCR4wGKZhmGYrDZ7UEYy6x2wFA7j4F5pjRyPehSuBVmQ4VkX5WLdpYzr3oV1NRmZytdbxwLoFETtknhae3GJpX
W05,Hg29Zv3GY1Bbp7JQ7Lbawk8e3cLDs67EKGifT1JUUzL3,217403808,-217903808,1792703550,4y76MJm361ApZUL2Ex4igeZmCpNVkwEfvDqEpBMifSwYexufzZytcm1bFFEfayHCqHNHHMSxQ3od4dMfWGyTunpH,2AZdGuSV7doS8hhCoGmSmEaQ6mx3a97UpBNZTTSUo4GM6gmPvVmKNMoHLN63toXb8a1vcMjqPuMBumk3JiZvjmKa
W05,Hg29Zv3GY1Bbp7JQ7Lbawk8e3cLDs67EKGifT1JUUzL3,3548486,-4048486,1792703520,5nyuRXjX41YN9184xsVCg92w52tDyaGRhrkLBT5yT979U1ZC9oq3D8MgzCc6964LNsy5xVRV8DLK9HaKg7AvPPW5,2AZdGuSV7doS8hhCoGmSmEaQ6mx3a97UpBNZTTSUo4GM6gmPvVmKNMoHLN63toXb8a1vcMjqPuMBumk3JiZvjmKa
W05,Hg29Zv3GY1Bbp7JQ7Lbawk8e3cLDs67EKGifT1JUUzL3,1276317729,-1276817729,1792703162,5xpoTWAbQjntVwbmZkN6fbo1PtPro8bb94kt8Q1FVdtjtZqHXNUkpWbpUofS12uSSDnVMXWvxgQA7qp1oFkMTwtv,2AZdGuSV7doS8hhCoGmSmEaQ6mx3a97UpBNZTTSUo4GM6gmPvVmKNMoHLN63toXb8a1vcMjqPuMBumk3JiZvjmKa
W05,Hg29Zv3GY1Bbp7JQ7Lbawk8e3cLDs67EKGifT1JUUzL3,21220501,-21720501,1792703322,WdFGPyJG8FosiPBk43YaUunRnLgcLmdgeKavE3GZNR3fBfDUA1fzK44RrottNyYAtR9vvkZGLpsZ4AqVTVR6RVB,2AZdGuSV7doS8hhCoGmSmEaQ6mx3a97UpBNZTTSUo4GM6gmPvVmKNMoHLN63toXb8a1vcMjqPuMBumk3JiZvjmKa
W06,Hg29Zv3GY1Bbp7JQ7Lbawk8e3cLDs67EKGifT1JUUzL3,1424809796,-1425309796,1792703222,2HXpmGBothnvj73d61GN9ZtvdWoDovgcKAFinoN6ywVAswYXhJUMqRUej9RdGcqPGJXjVkHhsrAvr4x5K1gWciaU,4tQBM8myG9pMeVPVAz5TqSep5FRZzczwNzUetctXnWx7kPMq437md1becgHkpsKWsX9sZb1FeNdp3tyFZ85V1czy
W06,Hg29Zv3GY1Bbp7JQ7Lbawk8e3cLDs67EKGifT1JUUzL3,907118687,-907618687,1792703238,2Bf37B4L9ESr3aKrpfUHRSm2H9iQaeRGS1QCoMW4ZoZFLrKMfhGznQn3PRr2DeJfFXpJYJFWroHJLxRq1g9bScs5,4tQBM8myG9pMeVPVAz5TqSep5FRZzczwNzUetctXnWx7kPMq437md1becgHkpsKWsX9sZb1FeNdp3tyFZ85V1czy
W06,Hg29Zv3GY1Bbp7JQ7Lbawk8e3cLDs67EKGifT1JUUzL3,834651625,-835151625,1792703576,23NZ75ecG5XyUPeUGV4mrwJnoHLotvtRV1AAAebZjXADVEJ9e5dNkgMzrgXHXusDJwcdeAABGhRYU6gsxQokoDGE,4tQBM8myG9pMeVPVAz5TqSep5FRZzczwNzUetctXnWx7kPMq437md1becgHkpsKWsX9sZb1FeNdp3tyFZ85V1czy
W07,Hg29Zv3GY1Bbp7JQ7Lbawk8e3cLDs67EKGifT1JUUzL3,1349603466,-1350103466,1792703569,WbPnKEGeqeHBM4CVWA3hic3iqG47m8YaWnPbwXQJDUzbWyySMfHF2eZaZHQGT42P5gb93SfCT2MjtcxdCRqkqHo,5bjPnDyqkWbkBV21HcHX2aT5YRNKmAxfF99bMzMjY35RrKjWnJLF1B1iebtzQimmoudJf6nHb4f9hpskschKCPL9
W07,Hg29Zv3GY1Bbp7JQ7Lbawk8e3cLDs67EKGifT1JUUzL3,104143158,-104643158,1792703254,4ankrNhxbXDtWz89BMkZ5Ecrjb32SkR3vzTK1qKx71DHzYnkT9eWaQantqx7tcdLjz1kB5Kk9Kj369yJvzG6mDmL,5bjPnDyqkWbkBV21HcHX2aT5YRNKmAxfF99bMzMjY35RrKjWnJLF1B1iebtzQimmoudJf6nHb4f9hpskschKCPL9
W07,Hg29Zv3GY1Bbp7JQ7Lbawk8e3cLDs67EKGifT1JUUzL3,1327758222,-1328258222,1792703232,2QZfxX3FBzPBsTU48tfVXVjJdYRk6Bp41aE7W2jvPJnRa6PqayaH9MYHgBM1gVZfgAcdBexpF99WaCi8dF5yNpxq,5bjPnDyqkWbkBV21HcHX2aT5YRNKmAxfF99bMzMjY35RrKjWnJLF1B1iebtzQimmoudJf6nHb4f9hpskschKCPL9
W08,Hg29Zv3GY1Bbp7JQ7Lbawk8e3cLDs67EKGifT1JUUzL3,300479845,-300979845,1792703255,2dKP2NqNrETLanVm49RHCWj4G2JSTDfznyuMCr7RgAMeBoLbMfuTs9Fj6Fkkx6Dk9Jwvm2w1jamxmHvR7nz6ZCrp,4WYJ6ajzS9WboC61ChMrhUuYh6QQS1LQeH19bAMLakYUZ3oQyyct779GRqa5drjy9ECQwKGEMVhCjWdxM8boA6cX
W08,Hg29Zv3GY1Bbp7JQ7Lbawk8e3cLDs67EKGifT1JUUzL3,61020902,-61520902,1792703351,3CuKihYXPu5McS89rtRdRrZi5qZH1TCiBNRriGFf8EBHgTM8z5ADpMjSgoM7tTjELUFK7STaCFPgjQ2M9NQzvcGw,4WYJ6ajzS9WboC61ChMrhUuYh6QQS1LQeH19bAMLakYUZ3oQyyct779GRqa5drjy9ECQwKGEMVhCjWdxM8boA6cX
W08,Hg29Zv3GY1Bbp7JQ7Lbawk8e3cLDs67EKGifT1JUUzL3,1321903034,-1322403034,1792703233,4pG8SnajZ7mezUp66AcK2NHP7WgEQZzCH1sQGfEbLmALmWRZEJMPMCvsL3wBrkqEhkTu8xPMDWZuvk6Hx3zf4KzU,4WYJ6ajzS9WboC61ChMrhUuYh6QQS1LQeH19bAMLakYUZ3oQyyct779GRqa5drjy9ECQwKGEMVhCjWdxM8boA6cX
W08,Hg29Zv3GY1Bbp7JQ7Lbawk8e3cLDs67EKGifT1JUUzL3,325660692,-326160692,1792703571,5SxHaKts8ckRrSUifYtWYBRWHiGgWVr4ASU2aRRaUqT2agCfyuQySPXhAHCssawxoEmpZyJ2KD8APQDbJmq2Eogh,4WYJ6ajzS9WboC61ChMrhUuYh6QQS1LQeH19bAMLakYUZ3oQyyct779GRqa5drjy9ECQwKGEMVhCjWdxM8boA6cX
W08,Hg29Zv3GY1Bbp7JQ7Lbawk8e3cLDs67EKGifT1JUUzL3,1388194256,-1388694256,1792703363,59yTtqXACZqdAoMvr2bp9YM8zCycUY9bvKbUTDCqwR3d3Q1SVro4SFHk9ybbgyzDfZdWxW2pZ7Vx8C2vppxSUCPT,4WYJ6ajzS9WboC61ChMrhUuYh6QQS1LQeH19bAMLakYUZ3oQyyct779GRqa5drjy9ECQwKGEMVhCjWdxM8boA6cX
W09,Hg29Zv3GY1Bbp7JQ7Lbawk8e3cLDs67EKGifT1JUUzL3,146839881,-147339881,1792703572,eFH5w1h6oVJRnCpSyeSurXxmynhgcgvBh6fQm9j14Yad9ie4WD5g4GdJFu1WdDKHbXiauFMR3QQA2v2vDxbbp5p,3EKNC3AkTVhSicwaJ1YxggkSywZYkYbh6PHKxsH5R2DRy9z26iZjM3hVWPgVtCB4gDUuv3v8NrgSTQDTLDz8hQ5E
W09,Hg29Zv3GY1Bbp7JQ7Lbawk8e3cLDs67EKGifT1JUUzL3,14441836,-14941836,1792703257,3NzfZUve5KSN95voZ9u9QyejUV1Ym8pYHjBq1CR9THhDvmH3qFgNH8nUA2kQ7gCRUA4qUZxtLfP3w26zycUQPE8W,3EKNC3AkTVhSicwaJ1YxggkSywZYkYbh6PHKxsH5R2DRy9z26iZjM3hVWPgVtCB4gDUuv3v8NrgSTQDTLDz8hQ5E
W09,Hg29Zv3GY1Bbp7JQ7Lbawk8e3cLDs67EKGifT1JUUzL3,1563736197,-1564236197,1792703234,37Zgub1ipTmKWiAm8HNyTvUFXyYiwjCW21TdJjZRiQXPRTsRJccudPrs4JFqdy2CRk8NSuucC2CTUXSFLappv23X,3EKNC3AkTVhSicwaJ1YxggkSywZYkYbh6PHKxsH5R2DRy9z26iZjM3hVWPgVtCB4gDUuv3v8NrgSTQDTLDz8hQ5E
W09,Hg29Zv3GY1Bbp7JQ7Lbawk8e3cLDs67EKGifT1JUUzL3,1092139804,-1092639804,1792703394,4hptRzxW4EfjGCAp2KVkUp84M6Ct2NFXksbxbhkYGzZrKVgt8yNUBfWZ47JEhsrvBtpyC2gJo9MwhrDAPYNso4wx,3EKNC3AkTVhSicwaJ1YxggkSywZYkYbh6PHKxsH5R2DRy9z26iZjM3hVWPgVtCB4gDUuv3v8NrgSTQDTLDz8hQ5E
W10,Hg29Zv3GY1Bbp7JQ7Lbawk8e3cLDs67EKGifT1JUUzL3,1390076974,-1390576974,1792703353,mdypKKwjGKBtPYR6FKNinTQywnVjmRMnwKj46gYrVTUu8aZWrz7SsBw3gTdb8uS8bkPUAj1pnp4UzgL5FgyMGwp,3Pt5u2uT4z28YG6HsmMXchHXgj9xBgoxYYxxuRuuAfnGFh9opacemwYEVH1fEzigepdCzgC84MKJN2Q7jRU2JBA3
W10,Hg29Zv3GY1Bbp7JQ7Lbawk8e3cLDs67EKGifT1JUUzL3,13078518,-13578518,1792703628,2mMrhi3qXFaKVnDYsdaDNcz2A3yuExk2eqrpRsf2FPAAadRoYpcmWDTWFdDkzpeHiy4nqQ8rx6EWGpirnkrVQBBZ,3Pt5u2uT4z28YG6HsmMXchHXgj9xBgoxYYxxuRuuAfnGFh9opacemwYEVH1fEzigepdCzgC84MKJN2Q7jRU2JBA3
W10,Hg29Zv3GY1Bbp7JQ7Lbawk8e3cLDs67EKGifT1JUUzL3,515994401,-516494401,1792703574,3rNyND9LNavVkm2S5KcKJ8BS2oJhXN6zDjEYV1s7Vzz1BvbspADqQgRBy3h5t1RTNSVMG1CqjcMcJsj1oYMtNkQM,3Pt5u2uT4z28YG6HsmMXchHXgj9xBgoxYYxxuRuuAfnGFh9opacemwYEVH1fEzigepdCzgC84MKJN2Q7jRU2JBA3
W10,Hg29Zv3GY1Bbp7JQ7Lbawk8e3cLDs67EKGifT1JUUzL3,1564808217,-1565308217,1792703396,3ZtAuvimYSY7Z2ap6o2EB7HVbSetvc1A5F8DHvNicA4m6Prdu2zzNX553wngNG7xffDHfKcm5zFE9Z93Z7kpjwtA,3Pt5u2uT4z28YG6HsmMXchHXgj9xBgoxYYxxuRuuAfnGFh9opacemwYEVH1fEzigepdCzgC84MKJN2Q7jRU2JBA3
W10,Hg29Zv3GY1Bbp7JQ7Lbawk8e3cLDs67EKGifT1JUUzL3,1160184122,-1160684122,1792703627,3BFTbnx4KM14uDtgyWe9veRuBNeGX6GPq1y8cBqeSx183kqvU6xPhxejsknyUnzxYE9E1UnchzpXPiwcDkKxjWby,3Pt5u2uT4z28YG6HsmMXchHXgj9xBgoxYYxxuRuuAfnGFh9opacemwYEVH1fEzigepdCzgC84MKJN2Q7jRU2JBA3
W11,Hg29Zv3GY1Bbp7JQ7Lbawk8e3cLDs67EKGifT1JUUzL3,314246850,-314746850,1792703629,4HKd4kQARwx5NhhqJGirEFfTAmjeaq5wXTSmgXruRTJXyoFQREoQKTbovNXPms7dFLrWtKQUfnBFhZ2kPPfzv9SY,5rTEewq2xrWkyMafn4JSv4YCnio4QwLEdj6D8zEpJeGXowR8EWTVmJKXHAnJKhJDWVmP3SKqX8bhXqTp6EVWBNR3
W11,Hg29Zv3GY1Bbp7JQ7Lbawk8e3cLDs67EKGifT1JUUzL3,636900729,-637400729,1792703575,5nBp1BkZ9auxa5Y1P3KR3qkvUiLzzkgjyW1FpUTKymwkXoBddD9MYdhbbokiCs3c2QjRJsBegkvc3FmwMSKSF1pc,5rTEewq2xrWkyMafn4JSv4YCnio4QwLEdj6D8zEpJeGXowR8EWTVmJKXHAnJKhJDWVmP3SKqX8bhXqTp6EVWBNR3
W11,Hg29Zv3GY1Bbp7JQ7Lbawk8e3cLDs67EKGifT1JUUzL3,1420047786,-1420547786,1792703354,v4avVbJDE5yeELLT38NRCr29V1Gj7tQTrrD1XhBJcbejFhVuzSt3HT2NQXTCJqoKEVEF2r3ZH2m28qisGGtUud4,5rTEewq2xrWkyMafn4JSv4YCnio4QwLEdj6D8zEpJeGXowR8EWTVmJKXHAnJKhJDWVmP3SKqX8bhXqTp6EVWBNR3
W12,Hg29Zv3GY1Bbp7JQ7Lbawk8e3cLDs67EKGifT1JUUzL3,395696813,-396196813,1792703630,ox1x1ddb1Tavvph9RdRnj62gAAM39zNUnxDe27Cv15BoYvpx7xqB8wiYxJq5CWAyikQYDNZL3Ey8o8gGXWEnhLV,4nLf9afFmXEW66zZ7JrMHegJ16JU1fs38KGqiEVnHKPPBSg19TFPyfPffF3sytnPqVaaU6CgM58Hc2fKN5m2b5mg
W12,Hg29Zv3GY1Bbp7JQ7Lbawk8e3cLDs67EKGifT1JUUzL3,1706755635,-1707255635,1792703386,2qXeQdYAYy39aKnPt8Jd1vYdobWpfaDgM3RzBUtso6U4dAfQfC26ZZe9Dc1omhC94fTeSzh8wY8roUnjMwgieBQw,4nLf9afFmXEW66zZ7JrMHegJ16JU1fs38KGqiEVnHKPPBSg19TFPyfPffF3sytnPqVaaU6CgM58Hc2fKN5m2b5mg
W12,Hg29Zv3GY1Bbp7JQ7Lbawk8e3cLDs67EKGifT1JUUzL3,1221635046,-1222135046,1792703577,VaNN4k4svqtLjsdaHmBuppLX61eyQPr3A8ZX1pBtp3BDmeLBVr1Njye1YyDtqieykKZVhwtJRf73L7inEhBerm3,4nLf9afFmXEW66zZ7JrMHegJ16JU1fs38KGqiEVnHKPPBSg19TFPyfPffF3sytnPqVaaU6CgM58Hc2fKN5m2b5mg
W13,Hg29Zv3GY1Bbp7JQ7Lbawk8e3cLDs67EKGifT1JUUzL3,646579351,-647079351,1792703632,3BH9R77T8zkn8bmZRKxLzvRoTXNMDipmmsQPtbihvAmETsX39Rr5ejKGYcDie4CFRSoSgsWWoNASWGeow81AtEyu,291t1SCEBrHq2t8KsibyfzTfwpQ2DwQZTibdiUqsrRXwpfkDPFKQkapMAgE6mG9ComkRPaQUJrf5Tf2HreAeWA7h
W13,Hg29Zv3GY1Bbp7JQ7Lbawk8e3cLDs67EKGifT1JUUzL3,596127000,-596627000,1792703578,CHduFYAANft58hXfXMogUuUGuYqwP9zEN9DjwjxSJTp49P3Ym5ukKpRVaBLGT38WVABWCJW5VUPN4hxPJ4R2FdY,291t1SCEBrHq2t8KsibyfzTfwpQ2DwQZTibdiUqsrRXwpfkDPFKQkapMAgE6mG9ComkRPaQUJrf5Tf2HreAeWA7h
W13,Hg29Zv3GY1Bbp7JQ7Lbawk8e3cLDs67EKGifT1JUUzL3,1878101164,-1878601164,1792703388,3HQrFiQAfv7ESF8BUZ7Kre34CPZ9Vik9ZjJTREsMdKnCXMxWkqUyWadvrbUKNPT4jp3AEkNRH3axfutJSbnosUZh,291t1SCEBrHq2t8KsibyfzTfwpQ2DwQZTibdiUqsrRXwpfkDPFKQkapMAgE6mG9ComkRPaQUJrf5Tf2HreAeWA7h
W14,Hg29Zv3GY1Bbp7JQ7Lbawk8e3cLDs67EKGifT1JUUzL3,2204593059,-2205093059,1792703580,3AJGvtuCk4PxKeyTVduS3Tvztv2T8RTjoPLoEW4PzqLpC3ChBeQE3gt3Wzh7hLxDnNUhMZS8bKdEEorK2fjX1tfV,u58mMoP98v2TGwBy25uLYRZfcFXo13LNTCjPVHe91W1KgMGMy77YfpukcVso8XdgLKrgU5Kp1CBZP11k6PXfvnS
W14,Hg29Zv3GY1Bbp7JQ7Lbawk8e3cLDs67EKGifT1JUUzL3,705624077,-706124077,1792703633,2rf6HvjXj8e4nxg3hTEAtRKk2VcRqMpeWzTaSVxUDUkvCQVqcDFKveycznJbZddzukpMewWxMrCSUrsfQzcva4C2,u58mMoP98v2TGwBy25uLYRZfcFXo13LNTCjPVHe91W1KgMGMy77YfpukcVso8XdgLKrgU5Kp1CBZP11k6PXfvnS
W14,Hg29Zv3GY1Bbp7JQ7Lbawk8e3cLDs67EKGifT1JUUzL3,1945064038,-1945564038,1792703389,4aGao5HaFayTchaJfM4RAgaKCgsFQvHQFU7pzdtLFA8YUo1vsmJ6NiSUN9pVQHtUZhhedVe1CxMNG6H4YJeKiS1V,u58mMoP98v2TGwBy25uLYRZfcFXo13LNTCjPVHe91W1KgMGMy77YfpukcVso8XdgLKrgU5Kp1CBZP11k6PXfvnS
W15,Hg29Zv3GY1Bbp7JQ7Lbawk8e3cLDs67EKGifT1JUUzL3,1931652411,-1932152411,1792703391,2XMZspPz9o66qG659AR4cN5Wn9BUQaCmdNcKZuNzBJKWQapbcTMxcsq7giAjJKoJJYhYUuxbVBLMwh4ZsZYMxSi4,2J1sDvrEydtTcdVqE3N3j7dEuR7ze5Nf2xihVF7s84hMo7XsixFnfzYmwjdmEkvjdwcT5XUGHfc8AgykuQk5P5U6
W15,Hg29Zv3GY1Bbp7JQ7Lbawk8e3cLDs67EKGifT1JUUzL3,993617592,-994117592,1792703581,XKXT2jH1ruhBSQLpe8j28Tce2KBm3pE9ZcFzc1QNbuPpjdBbcYqBEPNnBYGw1UDJET31SYw6n7bguQWzrt185yA,2J1sDvrEydtTcdVqE3N3j7dEuR7ze5Nf2xihVF7s84hMo7XsixFnfzYmwjdmEkvjdwcT5XUGHfc8AgykuQk5P5U6
W15,Hg29Zv3GY1Bbp7JQ7Lbawk8e3cLDs67EKGifT1JUUzL3,1303125622,-1303625622,1792703635,Lqrf2adX2CpPnXp1btm87bbXf5hzKWwDzXkztyvFCdFMWKH11E43CH9XSJDK9CCTkRtM3H3ci49VUwYRCKAiSt3,2J1sDvrEydtTcdVqE3N3j7dEuR7ze5Nf2xihVF7s84hMo7XsixFnfzYmwjdmEkvjdwcT5XUGHfc8AgykuQk5P5U6
W16,Hg29Zv3GY1Bbp7JQ7Lbawk8e3cLDs67EKGifT1JUUzL3,794234854,-794734854,1792703583,c6BTp4S4Ux3KEAiWYByFuzGqSV6tAPwiixwnygvg4VAkKCQQSSc2VPNpPv3QWsvyWrxxLUeczktKoBFH8AZC4aH,65om18EdbMt1PRYLdjqPUnopgJZYccHnPPg4LKkdKKoKmECv9zMfi7MVUJFqwiKeAMNGdaafZcgZg3tBDijUDoRQ
W16,Hg29Zv3GY1Bbp7JQ7Lbawk8e3cLDs67EKGifT1JUUzL3,2153776491,-2154276491,1792703392,3Zzd43odwbEAu7EMGjJYYemg7cJpGP35eNThRMWGhFCEg7yFM5vjADp4RTLGBoER9HA3vDsmbexuuZJfdJf6dF5v,65om18EdbMt1PRYLdjqPUnopgJZYccHnPPg4LKkdKKoKmECv9zMfi7MVUJFqwiKeAMNGdaafZcgZg3tBDijUDoRQ
W16,Hg29Zv3GY1Bbp7JQ7Lbawk8e3cLDs67EKGifT1JUUzL3,1494982587,-1495482587,1792703637,4xvE9DxkG4gxHRTfetFLB36WNHpSbaLUfXFC6DH5j74YNS4zXqxAQ65z9SfUSo4vgfxTC8rwoeqxMLMDJJ4ZMbVk,65om18EdbMt1PRYLdjqPUnopgJZYccHnPPg4LKkdKKoKmECv9zMfi7MVUJFqwiKeAMNGdaafZcgZg3tBDijUDoRQ
W17,Hg29Zv3GY1Bbp7JQ7Lbawk8e3cLDs67EKGifT1JUUzL3,2623380537,-2623880537,1792703393,h2Mogr5H8jSyjGovogsgFakSeiiygis6LXVF5DtjWFqgamtStQMFvssuQ5xwuwmPLGdK2vGZhZPTmKqBhP6vBdV,3JtmnKcAg8tfqQ4fkmrf2SCaDXBDBL9hnoayKG26XhBAeFzLzCQDuvzBpMbvf8bMxJGoJa5DwNRpRDSdTDRs8kpc
W17,Hg29Zv3GY1Bbp7JQ7Lbawk8e3cLDs67EKGifT1JUUzL3,1782062382,-1782562382,1792703639,3L89gg4sMXpSKSmanmUCRYe4WC23sFNmK1p96PJTozf9ZqcdtLMs8gLmqGVtieWAq8yjTrqDzyqbKMbpz1D4PtrV,3JtmnKcAg8tfqQ4fkmrf2SCaDXBDBL9hnoayKG26XhBAeFzLzCQDuvzBpMbvf8bMxJGoJa5DwNRpRDSdTDRs8kpc
W18,Hg29Zv3GY1Bbp7JQ7Lbawk8e3cLDs67EKGifT1JUUzL3,2828496643,-2828996643,1792703394,5XvAoQ4dLFN4gidotBiJL3vr18Lu1Q4yFdWJD5yJh5iBSMVLaUcmeuZyE4xeKXvdBD769feAjHCYxUJV8Z8MyRph,5PG4DQa2UYU7YeXa5gKwseY9ymACvyuYoaTH3YWmfQSDz4dWrfnSr7QVXbWSCNFPp7YM6VBmQRQ4htZ5AJ43Qpzg
W18,Hg29Zv3GY1Bbp7JQ7Lbawk8e3cLDs67EKGifT1JUUzL3,145315516,-145815516,1792703590,5C3bKZ6TSXhQSaBrt9Uiun7khQhjAHrq6q4wP4oZFwtRMg6oBzrc9pdPkcM9ttnJDJLhMrccxkFxpvEte9YDQQer,5PG4DQa2UYU7YeXa5gKwseY9ymACvyuYoaTH3YWmfQSDz4dWrfnSr7QVXbWSCNFPp7YM6VBmQRQ4htZ5AJ43Qpzg
W18,Hg29Zv3GY1Bbp7JQ7Lbawk8e3cLDs67EKGifT1JUUzL3,3493495297,-3493995297,1792703640,EFXRNMNzfSYfe3mbCG2uQN1USUx9eoCMxQwNAUTh19zpkkbXwfTpqmm4wh4gDzKcmT8Rpn8Pn5N1aCrL7C9VeYK,5PG4DQa2UYU7YeXa5gKwseY9ymACvyuYoaTH3YWmfQSDz4dWrfnSr7QVXbWSCNFPp7YM6VBmQRQ4htZ5AJ43Qpzg
W19,Hg29Zv3GY1Bbp7JQ7Lbawk8e3cLDs67EKGifT1JUUzL3,3513251499,-3513751499,1792703642,2iRS7RzM2jiR2iWD5w95VphJddi2Man1HyjQMHk6PWQKXrwEjTzPT9MwoUmsbzxzZYQfX2ysnt9BZzYqix4FnMAj,4AHNG71usdo12nnF8KZdyQv6kAQcEzisnfWZo2khYon4DVqNFA112evNEcSrkkwjLGMji5jWYDGjjKb4tPRfjotM
W19,Hg29Zv3GY1Bbp7JQ7Lbawk8e3cLDs67EKGifT1JUUzL3,61325870,-61825870,1792703592,5A6cgz6aMKv5M3nECKVAY1pnLJnHLsL9Z5TGkPa2TopxaLUhMms9JwfXqMUC3NWYAdqyYSnekruZ7QsqsZ7A3Dtr,4AHNG71usdo12nnF8KZdyQv6kAQcEzisnfWZo2khYon4DVqNFA112evNEcSrkkwjLGMji5jWYDGjjKb4tPRfjotM
W19,Hg29Zv3GY1Bbp7JQ7Lbawk8e3cLDs67EKGifT1JUUzL3,2801357739,-2801857739,1792703396,5EbhGJge55ud2x8T2udvwBwjAzS9kYTq88YnJi9wcJhAyHYXjYqJgsAJp4FPm7G6iX1G8wGDr14VpUcV8fKRJVWV,4AHNG71usdo12nnF8KZdyQv6kAQcEzisnfWZo2khYon4DVqNFA112evNEcSrkkwjLGMji5jWYDGjjKb4tPRfjotM
W20,Hg29Zv3GY1Bbp7JQ7Lbawk8e3cLDs67EKGifT1JUUzL3,2613963717,-2614463717,1792703643,8sFoteH5ekmSp3nGbKUUomQixvQWTeTkCjzyfrCzyWzm1hLivfmt9XT2jm43pXABwShtBKHqcUv1GdmEXMprcgk,579BNqHEZjRRzVE1vZNoSG7VaVE8hczYYPTQF5W3z9TYdXWpZvMpCf1LdsjQhYESB1VXiq2g3MbGSSe18vnnxCUG
W20,Hg29Zv3GY1Bbp7JQ7Lbawk8e3cLDs67EKGifT1JUUzL3,3228452529,-3228952529,1792703398,2uMSdcsgn78tCRhBUWXMG4P5cpMWBJ7f1nXdAHjapR9uRYpn3S3ok7rVstMYo5Mzxjp2jcxuFL63EYV2EkpAtnRX,579BNqHEZjRRzVE1vZNoSG7VaVE8hczYYPTQF5W3z9TYdXWpZvMpCf1LdsjQhYESB1VXiq2g3MbGSSe18vnnxCUG
W21,Hg29Zv3GY1Bbp7JQ7Lbawk8e3cLDs67EKGifT1JUUzL3,2120711155,-2121211155,1792703594,yKqWTmMkZdEXS3NJSoXfgfXrf72btaczAv8Dfw6qWJo95goM6ZQnD3R2Ld4iguyg4c8XoU99tET2MgRPevW6Vmo,5iDKJXqQfUrFUHgB473npxauqM1vY48bb8WEPWAkoXjuhRTS6ZjXdMzyij4vm1eRtCsrTtK6BvQpbHSmHei7S2jt
W21,Hg29Zv3GY1Bbp7JQ7Lbawk8e3cLDs67EKGifT1JUUzL3,3012576609,-3013076609,1792703645,5Jj7c1eV9CKJzbRc4oVrtBhzcddH9hcrSDcoxcNPTWqkcf4v6YLFGBq9cqzAaa9iYHCKd6KLatNuZ2XkGiUk2uYt,5iDKJXqQfUrFUHgB473npxauqM1vY48bb8WEPWAkoXjuhRTS6ZjXdMzyij4vm1eRtCsrTtK6BvQpbHSmHei7S2jt
W21,Hg29Zv3GY1Bbp7JQ7Lbawk8e3cLDs67EKGifT1JUUzL3,65283842,-65783842,1792703595,RbZszCWSGA4fS9SSEYcEr7KyKdWYVaBuvuJ3UqL4VeisYJ4yWLN4Aic6x6nxjrsJjvPAXxYQv1mATqHGkvqVNUr,5iDKJXqQfUrFUHgB473npxauqM1vY48bb8WEPWAkoXjuhRTS6ZjXdMzyij4vm1eRtCsrTtK6BvQpbHSmHei7S2jt
W22,Hg29Zv3GY1Bbp7JQ7Lbawk8e3cLDs67EKGifT1JUUzL3,5201383616,-5201883616,1792703647,4xAFCNqVfrzHicTy5WS1w6PUn9uVDidfM4jfr5c3WyJFNVddyjyRaq8CLtp9mRSFhZZ1mQ85hyACKx6qFnxQvPtB,3LCxHCPR4BCa4FgY2z3Zi38m6dANmSAdq1pDoBfjcZVV6kvG4LVA1fFMAdLenM2BnZr27VNuFJrmvUGajNk36VvF
W23,Hg29Zv3GY1Bbp7JQ7Lbawk8e3cLDs67EKGifT1JUUzL3,6417389207,-6417889207,1792703648,5h8LR1WW7tiPsnK9bhdSg7UH8hftZtfG7kwtNtTJLvttPrvHgwvPEApPiL7NXyAJ7BQHguBLyNAc3E8ew9cwV8wx,5fi9JXmWt1VZMcUPCnYiLCXrkeNPJxXrKiv6uh5GfxRT2n9gohTVwmzSS7Mc1txP693KUq6RVUaJgWL5kVkUQ7GW
W24,Hg29Zv3GY1Bbp7JQ7Lbawk8e3cLDs67EKGifT1JUUzL3,7377761037,-7378261037,1792703649,3TpiiShASMN1qKhjKh1rgyrwvJhKZaaFhTArZmTTuFtSrfu3AdqNV7GKCoDik9XCb1oDi61Pa543RdEYsutWbW5G,2jEkGBvev9gpH1Suuw9mEigEgYQGwHBcpjuhiaoFGwQMi4FKMpnYGn2RWt2gddkQUFXcoTkkvtBdhw744CZGXs4
W25,Hg29Zv3GY1Bbp7JQ7Lbawk8e3cLDs67EKGifT1JUUzL3,8341872430,-8342372430,1792703650,3ZLorwjMncWqh6M8gQCYQZUFZ89osGvqZgjCsRsnUe3EBrtFd9wURpkw9AWeuxUJz9mmGp4Ysob3tsfcUrhTbtKK,XRcufWFKByFsvrwe47XVFBravh9H759UznVgarzf4xSwtpAmgScfm2aAV1Ucv6Vrsf8D96egZHUPPEXQnu8FcnB
W26,Hg29Zv3GY1Bbp7JQ7Lbawk8e3cLDs67EKGifT1JUUzL3,11094775446,-11095275446,1792703652,3ic4C6tcHVEYsGMurQDRH933ESEgbKnUPvS7jHLuvZkLdtqNPGcZU2jUzQnLiaPqfzjLT38NUjgVXByn3zDADKhz,2ULqQtKh5ZgNSMX6vf58QoSparoRmSXqg2CVRGAr8SMyEPzs1BU7dPcQeQQCEi6UMvA66D29X8i3hpBUBCwvsQmx
W27,W02,1404710731,-1420399269,1792703671,4rZyfGaHTRYGCp1WMmc6Q1f6Jvt8jhRmo1BSJnaVTGRjdgou3HKTDboYCztXbFu2UdBANTSQCE5rCqg1T1LeX9gw,531vpMafcp98m2moq87PgV8JD9968V9j9UW9Wmmybd7kXw4pQSmfKDqjTQPBfVqti8sFpbV6mEohHthAcYaRe8gC
W28,W02,2910106146,-2941000698,1792703679,4SRLr7VLHvhbD1T693ZoSxbpUyJSyXziherhvcm6qsuihpAWH9RumeMAnEu7RRVpEFGSu2k27LbNMcfJXiG8ASPF,Pu5DvWRWMGZYP76jrQFCwUdPjkVMKVLMNEACaFoprAXnZoiyP7DgyezEAXMEiACpDwcRC3GRDNSo1hAHenVVMpH
W29,W02,2233738191,-2257800744,1792703686,2Q68QRkCHWL4GGwTDufUs28rzBptmcwbrxxSiGowZTSGhZ7sFir8SsX9As76hh5LiVQPLtEJu7NJR2uALn2wCfhf,4C6hNEtsaRrG8eqmkBsRSJUrywSZCGhwEyAYmGFKXtji61Lp5JLqkhPKqqF1YdRX2suAMNMcF4y4JfUh5bL9K8sD
W30,W02,1991384843,-2012999382,1792703664,4gYydYM4dzmKSQ2Wu2Va6JGSFMNggQ2uGyGkMxevUHc7T7mk4BC2EmEe86rSEQ1CJq2jBPHmGxcS1vsYrY7xuxMy,22YhTbQuZ5KkKLCCUbKBZmUytp4BXLPqDtTJ61qnA3xHqWxKoGxqmxrR84VFpVoLuEKfKE29tu5Qv18qb8Us5pTa
```

### E. All 68 repeat-purchase chains

```csv
source_id,destination_id,slot,sale_index,funding_index,buy_index,sale_cash_lamports,funding_credit_lamports,buy_cash_lamports,source_sale_signature,funding_signature,buy_signature
W25,W45,460185746,286,287,288,6018452707,5958859665,-5946910196,5hN9J7HaHRYViT5LR1rZrepbjHvsVc8egZegFBfNb26HFnR96b1mk3KDr5574JULmv4opDVosh4foaEM2sK2jWzp,LtxaaNxL3RPCf9CrLidTy3WHaNKkom6Z4PvnfzHtP15RfoXbcm2oQYos9uGHWALHdFX8U9nYSfM8mvGJ9HgyJzH,S1rgL6j3ypZpVwWd3q93U1rR6oFFbk5dw5pww2w5qjcahTtT53osTdkH87vjJQ37yWWjEwz9caDwX9dtgJVvKCY
W25,W34,460185813,408,409,410,614704685,609149123,-605442494,4PtomNu9kEazs5cuwfVzjJHBNLqwLNEDqpPa9RKkXR3Uq57o8FahtVF1zozf2QVrQX7EgYZjidq9ywkDe9fNbkzt,5xCpSXrtLD8R6cV8rzf4b9W9BusxbDj14no576qHiHXmsaJgqtuuR48NZK1uFphaqSP9GzRMgFgwGSrpivVbNTjr,2VggrS3HnUWD2USMdW8XAiGgWR8uTagoBisxigAwszHWA4qfWmLn2o75sdMikNreAnWwptxAsAm9Z8RidZqH2DYe
W04,W50,460184485,459,460,461,4024310236,3984658619,-3977347625,2qX5JoPAoZkoiPcySojtqL5oSABq4fCDEThdMQSNbkUUNmm2wbVCd3vP62jLJf8AsugRwnBiHfopFfQWxNw6ScZj,pb1Lgmw7bksYjxNFr5zH7Yq4hXg2cHTiKJXVE2uXRZg6pGwosuiHcjv61nn7fCKHkS248J6eLwHvuVbrbM6QUbg,3VAJ5fvW3X3YZC9ZH3PVmPRPGugb2MRXWEwhBFpn6Fc82rTzp6qtVvg5FgBqVwZGbX3cig6jXQhcEXUZ8DeTxNYq
W21,W57,460184798,240,241,242,3463003672,3428965120,-3420963978,QKYktGzwyqcXSg98YXgX5m3if1kxEyNPVrYyhAHn6foikgo3ZXCJgU3pRAo4eUGDERWiinawEDWFHVp3ZUyUdwY,4CAv9yngtoWtaUTKdqA9fs9jePxYm2RewVfsDUwR8mZu4zsa7Lhfg3ZaykvFBbr6kqy7f5QEaxjrKne1vcicG2eX,5AAnHGGv6dMvp7PMccn1TQ6iZqL7sheh4QjTaC5X72CJoLPrb8RCYTnL6QkrEYf52xYwxX7QcU4YjwRTmA6V6mDt
W23,W49,460185032,806,807,808,2805583394,2778119045,-2772750858,25PRmrnpbAhiqHgnN995cvGZzrHQv7aH59AoUhxKxcK3LuAKvvsVEGqXYrTYCoRMp2n7eDgfijF7UvVx25t38u5q,3Ycy4LQrJMNUViDBZDEjy7zXfafhRzyCUar1WDdTkkCbggLTjajLxSGXwN3EYPwc72sauKNM86Xw23cFtHpLwZ9r,3bb4tj5sRR7mhwQryaURNTR8MncpXFhFcbPbbXiMUTEqrzJRznWMbiZovJVznyB6QWz6jmu4T1EoeMty1fQKxe6a
W11,W76,460185229,253,254,255,3034277807,3004526514,-2997221734,5qrvvbTzn8aL4anaxL9TgPNjr6PhgHcRsmGMm2FWDnp8McWxsj6R19gmChHrD8CGWHN9WYkDbNNPnSDUVDjm2efM,5cXXk1mWUGC6tA5dQtvNLVCdByxWqA55vxEqtYF8qssKTMFzBWbNgXdHZs2erZmHxyDsbQVapQf4obGtUW2pS61Q,dWcMQo9zujtYXpcraL41qXmww5KtrQhoit3DemXuCQrWrxB2a4LQDpRVLEnA5vgyotuUmAGdE6vq7eyHtTLpuYd
W06,W65,460186152,225,226,227,5228430854,5176738030,-5173430519,Fh6oP2QXrEJ2sKiXgtnmseXtMnv7Rpc2wrg16tAEMq97S61GsTYNr4xr3vZDZUKMpCyWQsYLdAYSAwTvfh4kCjD,4Hiip5pNDNxuqRxQHeadzx5hBbYtVn2mAnERizExb2bMrhQyhtdVBJahBVvQthJwaQM111qofVACV4KyhxvtNLmF,3cuofvpVGi41U5u7bNmLxHnDrHeCskzvcUoBwj8ujv8RvZB9BBZcjD1NPE1MB6Y72ZF8GPVCyNoew4Hvw8aL6zWL
W06,W68,460186186,256,257,258,8056257513,7976286423,-7960936496,5XTRKtjKJLquXd2rxZjeTqyUuHbhztufAWzCytjLmimyTfdqqqEgsDqgUG57fnBpqoDU4Ddbw1WLTFbPZkeUFTMW,4iKR8KrWq3ctzDugvA7FYV61HZFQpAR2aeRA4okfctEUXGvngc3hymBAWf9tiu5w4fGzypqUrDAb49uStgMubWCX,2jRXVAWVrhaFVX9VCBeT9QLRD9Nj8EER6bkkpSrzFcrxsZ3Jko14LYxJfozxS3YhVKnNVUjNSeYqXTJdVqepT19Q
W07,W58,460184190,10,11,12,3805634024,3766695613,-3614620986,5KJQuXsbWsY9bcys6uGXUCVov9pt2Mgwo6Vic1MdvRRHwLqGZ3w2hPBZxzUzYRQbCEDwZh9M2jZstsKP6Rmy84mG,DMAjAGkcc338FVtkMZdYiwGmyiDsobHQRYD8m15jKYgnpLxJSatkZMGwRrXxZCPh4no1gyJ5U4kn9pErSTjRtRJ,M8PeTrdBfSDiRjJLM8HdTueqDCVR8WR8MFKFmNZfRMbPD24hxya1DgBb9GrJVfsKn8q9saayZJn5rFy8y3oBKL4
W09,W80,460185505,301,302,303,6259542137,6197538201,-6184985831,E3hwMFT5GWJoefJDUNMpeuPcHqcFUDM46NDCKgAdthwqKAko1pWrLGxBvVEXT6fjewkKvDi9PuycCs8qJp55Vf3,2TJsaPiBB7Vj2DMtZGJZ4R2vWFAf9xtzdXCfR93vUMttji4A5BPpe3aLo2y9o8dH4Mv3xZ1jpM3NaQAjLwPy56eL,KydKyHkYPMfQ9wtAB8Lkb69BsQV2VXEDGkto87WNzvsu3nrJ6va2vp5vqbyzd9xuVbNJUgEAnmWBTvt6skG9zJV
W17,W33,460185332,75,76,77,10774546585,10666047095,-10642076619,2qT1rvjnECzsa6BYmkLS9djTdh3obsrG9WbgHBx8xi5z5U4anbVRahr8AbSobMqT8A87q4t63Y4JqCDgep2k82n8,2ethEHNkiabudy3sWRwaCfr1oafsTo6ZiZEvjzKurHJAzQuFGZ9SfDXxGXtYKYzotV9k3ESX5fZ7A3pSpRdMoZ5p,2Z9d2EP2VrLqBtWFHf25ejwrTa7YrGbiduyMKBXFEQPcJSEmrg3HdmQgsBNQCnWhJPYVi4suHoqh2TVC6zUbaaLo
W19,W98,460185610,155,156,157,10330934562,10228216701,-10205501248,2djuU7TokLSTZPgtSsQMxNthV1Tdc1KXYsYZNswjiv6r6xwQV57abm97XHsynPsmUwJXLhuTG2Ui7xqwnsJZR239,7nruYszW53HqkAqEd6xB2qUZ6g9XURd6eWVvvRqkjCahkgZhtcd34mbFjkNTDu5nsccshoHqmA1caXg4EQmHZmr,3AMmVM2LvgXmrArojG3DaX8BRL33PF3fLmzpAzEXV3GmrYCdwfthhQzQj5Qy2QF19DYH1xbon56T5ykx74ZMsSaz
W09,W52,460185473,227,228,229,6318279933,6255688619,-6242719339,3QPnGwQvVn3sdfnqBuAvFtqS9xJqLF3UNdHr7K8LDFgXcsxr8kMdoAXYTuwLNF34rfUviABQ6TFhPnAdG8q8cC2K,3MgG42eTMAGgQpdmT5K6PFwS8VuVQhBEQ1etvsAhQZpKLxo6jhFDjrV61MCkG5Sm3kpZ9PFnDNrwbHGMwKJMx8mM,4njjhJGvuyNwDWzF7jzuHFU62vrbc4EeBaFT5qu52K2xsj6JoMNN1fxNxvYWdrCNs7wPtrCtiYFGMm1bu5GtKLTM
W10,W42,460185847,118,119,120,8800135275,8712725407,-8694320353,tTuQg5h3oBfRtLhFHhkne8rAEdKiDjp6koGDaSarj1MLtSHkMzHij7zzdEP4uC842NY3u4yiWYyzWqYdYgSQw1h,2ppkpheEWEwv2UjYC8nmZrr697zCTwXFKWM5JENZZFWTpfwR13dcLUXCcuBB4acifAALivzn6mmX1QtMSJagqkMV,2Pvkx94LejT4BmY7bPox8i9FCoUetUncKXCFFdBw4Ax5BavXq1Ck7XgqA3VLnktk5Q8SHYvpb5hQCnoRmJpvCerL
W06,W40,460186256,488,489,490,2420413087,2396800441,-2397007429,MkbCZyDwuCPCMthmCZ78nH47YRLALBSiHi7smyKCYVtYHwYzpHQXYEtUMau3JWqhrqR2pXPdFUd8KCVvk9HuW3T,2KXppmHx8B5x6kySMwuPrAGFXDuxXB6hRUMdRvv73Mjg3VGJ41aL28Yp1RwGxU9wvAV1GD8Pw4xsx6nXwXPxkRKr,3C1j2RvqymQkZiL5NttchEgD7ZvAjDPypfQxkrHcxwvKt3GZkcHed2iBwDM78wLB3ZGcFJSX13mYzZPGLo1U9ftk
W04,W95,460184595,320,321,322,3006596807,2975776815,-2969929613,Zx5ku4px4Dg5h8JbLLp8MRQdckg9boMP7zQZxRg6zsMG2GuoyKoatDj1jZsThRhUnzz7DF8Dj6ANK5BFmAW6o6o,mYk3NuNmY6G6qibV9EstoDpYv4emAwi87At2HueDrd9KX1nWiG4fnUmx4pJ1d8mjic9MWbC65KNeSEU31Kg3xFT,4EEHnUpvNBa21czHFjgwSQy8vf7iSdpxHUnPUKAirxQvFpriWpvyA3hPGJem2xRkNhnnpuk4oVPcSUVjUWc3AMvF
W26,W60,460184699,312,313,314,5359496948,5306493463,-5294630270,5vwrJcCBZqpDhH37mjRVzbHBvDUfgsg2ANPFBgC4AraqStBDZHySwrJrDiVqLzZ3YEYvmAFPCbYh2irPEkhvan5F,5NDQpaUm5h5E9Hkarv2vwtBDoiywmL7jnMyj1GURnUR87rh1NZaiSokozDiX3sQ1m34o89bvHDmD9JMUT4TAEYA7,2gmezaPT6nHigeGABhC5dL5oZEoMnoTJBeZkuSAovYfnXcMuyRfYdwiLBAZ9XqpKxUuabqbTpRGsWy4LGdT1yudC
W22,W61,460186321,128,129,130,8883626891,8795382107,-8781628741,2SGoifdrZCr9cCp1q4EzWMhtfWS4BBeZoWyKKBerPvwfN8Nt5L6cqy4VCvbCeLDnzjW1A3xTDr4FSo7rvsKc9wMr,6SP5DZgJJoj62Md9bQTKD9gyCN5Zs7GEpVSpf2CBruVoppdUAqxU4X1td8EsYo3yhxG5i2PXeWnt6qBgpeFTXRG,y3m6kg1xBqNnXDcuuy1hfjKc41P4J4QRvXku7r1kddNtZYNPTwhUftcSpXpYKizaGUaynbs3Qj7wy3SNWGJoi53
W21,W86,460184831,442,443,444,4624248302,4578597304,-4568322858,tS4YX3BBfQKpuy8a3dRtqVr1MEBf9bz1wn822E7KUxpQSqiHt8NhKWqvZdVZp5nwJLPaxcoxymFkCvYRKCyPZn6,3AiwdFRiHr47ZR9c9SWw1GmBhk2UkgcefUgywB6YQfGRRP4Rmztjkpg4bv5s9wD2FitgUd2eq442GGzBEGgcvpV4,4P3BQYLkynw7tz3gsrk23awq4zRypffzABktr9cjH3viEXi7wa5KtftCXUjD9C8iC86MCfRcBFMeJbvgWXXmCpAe
W19,W88,460185675,106,107,108,1967620765,1948536042,-1943086039,EEtRxdSdd7j5Bp2pd6aP5SkM9U2NMctBXxPsfUxsPZTzHDfDg6ccL5UUzGJDU63m955YxBBS9zLrdreziFqUBz1,2wH1RWQQVBfAenjxUsDsW7fe3GCK32PeDgSaU5zKVtYTnGgVYnbzZ3eB4YsTnZsBWced5y4r4jiLmoRuaGXA9sF7,28s3ep37ABXZuwfyMqaaQ7Ztyf8aDMUYqYVwVn42RCBoFnmrFrZeENzjfRaoEP9gnMHeFjDggu4tKfu8SM85yYtz
W07,W72,460184157,491,492,493,3054084048,3022661137,-2900648509,24Q69tzba8eb8cZnFb883X2PcxB4d5WfnmrGJgi23w4YzqomDr1sDv2WkXgYGHdafKyKDkdf3rA9fYgs9eucMbAa,2gWW3ZfS2q3rBxmmnEYyJETYQcckdZd3dnwkrYo7r2L6a3rKfLUhonrYWTc6y4SNuydd9nt1xxPz7U6rxjCdo2xa,7YesDqRrciRcmuYc9YjGiyG5rbVLPr7eBANhvdkbtZEbkNVTazdQspT6M1QDBp1pf7nLMmvUfzegH7GWd2nAjbP
W26,W82,460184731,492,493,494,5961539260,5902515352,-5889445314,4m9XSv1AV8abUZETMb8i9giAUSrCVorL5npZYWiuWhRssLeT7wCndTkYUYNSphufb3usLP1zQTmBfMvPittHackG,4LUZsVFAZ4TFTnqjpuTjxHavsEFaafHxy9RTB76BqZZhHTFzTfK6upj6d7Sg36CPPRA4WQdkazUeaZD2wPQ5ojWw,LrZHeTuWLZRysQnibFWXtthuSAfaj8MkP4rvpGYxBZ51sA52cuh8knrhZ4fZQW1gmYzkg8h8pUfRg513HDoCQth
W17,W94,460185367,39,40,41,4971826312,4921354025,-4911002008,6ekc4xDoVF2Z4uNjWaHfSVsYJXwSjzcFceLNxLL1aGX4kjRqcfwrtNHvyohAs6BQZckYT8egfVcVW9XBtqqzcGD,3CbzXMF2sFGiNgtBbtMAFvTo51GfTwvJzquYzxstH9wyu2GfXvZwhbtE9HhFvEj2p6SoGAF3btsitMxWEPEGbnFo,3ngSUD9SqCG5Lbf1yAKrUkivittNtA2dCqtZxhXVNdSansuW7XcUwfAr3afPY5dqdQXsAKc6KbgSBZPVXWV95ekp
W12,W44,460184416,242,243,244,4631766369,4586040190,-4577737965,63Wm6hyZv8REvSayLkQsmxjvgS2W1eMiSCDTB4jdLCM4ZrGnUDkgRr7d7ucQ3XV4oRa7xJJMT8w2ZrAzuRQuWU5g,3nMBAdYTpbTjAUcW6RmcAD1SKPMx68DWuU5rpxdN5cax8ZQiGYMFdNFHyiPmifa43pEF9CSoB9J6mnHnE7H2wGVL,2kyvb4JvnkzomWtZ71aq3hePRJZmaVx5A2AmNCkdqRfDwfuetzFA7sJmxYvLeKPaJCjLGSagniXeXjyM4LhMry5N
W10,W90,460185917,244,245,246,8391610999,8308286374,-8290954647,6tUYktbsiQsPqxfPRpmZnJW3SDZorYDgdTNjAeNPjY93NPVH9qTJmxi9GEEgDtPjC8ULdRqzDxUYTc9k5dqCzdf,h2PDzP7qaa9kc5hJHmfQvsLNpBLZmwiQ5NNiKkFfEs9pkb9mtUXpc3R5VEaDf3FtpW2h9G41Y2qdGNMRxTFm6t9,jHLX8CgeWvUE5wS2J8XBjcaVbucKfxSrjAoHvgbNMj2orwYUA4vmiUnth3UbtbuczKJjce2hnaa9dH9odt5mwwz
W22,W46,460186288,175,176,177,6677633444,6611448594,-6598861874,3ZtwvqRgAaBgwiQLa3ZAq7Vc1RDCxLW32TPHBDQQwzotdCg6py9bHB4AavKy2DBvb5vPaG113wHRKchRVqJSDjPU,64ZawyvreHNVUFcbQmv1V9aHN54AWHmHK7FLLeXzJh9i8e8gxtGf2AeiEJVo2z7Gyxna3vNho54K5cDk2fEJyoCV,2wv6KQ3c1CTRQq5v8kNbnHZ7QiXM8aevx9UNjzgECu1jJkNHqgyxgSC4AJ3QETmQsUT7efSKCwhS9P84qjYSoCyd
W19,W51,460185576,122,123,124,3461130411,3427110592,-3419409232,tVUwbhjTAwE4bGCD9AkKAMj2hXVz6V7SStuk5jX8jeEkjuqCqU8TJT3h8YvQoJDwuFMcLWfoRiDWvZF71REAwAh,kAUZ5REMPkBGiBekm6WrvKHNYqfreJGYTih1ugnynUwbMtw457TEpvY1EarQmVD2HgXy3s5PQBaLJ2TVStKGpHu,75Es17Vd3yLhqdmbuN2zyETaLpXR2h5xtBZDTmnVFvAVi9WuSGM3ggydwErpG44zNuUq4Sh29RixXzsz4sQpEXg
W21,W71,460184900,206,207,208,4075942486,4035774546,-4026659153,4LesW7WiiikjPSR2727SjkLUVm9NPLrz7zfd8BfGk1n2bD7j1QX5gTYupRYa7Fn6wi8y8QUdZ4o7wNHd4TfCoArF,TV1AbxFofU2WnDzFrjPMaLeezAPjN4QHir6PCNRNXxHvuiDNGUFJQDkZConrtsMzZuKbdPqCsnofQxQ4U4heaqM,2D2oeM8B8oyj6ZpR7TMAYLwnogciMKbWXJVciwXbJQ3CpPt82vxCbnCVyun2mC4Sirz6qqaxRtL2HcKfrMVd5s1Y
W04,W47,460184561,542,543,544,4374245416,4329748938,-4321879811,1czc2KBrY7qyRnc6CbFxX5tu4wAMXMRoNyepJcSQk1dTtLqeLdGWsrwAeX9wPxPSfUXFWNTk88t3YSBLPB29mKt,3T6MNVrqz5wgZjoWooCZKEayfdPi9LmNxsYneuRi5DapX9ShiWPQ7jaqsEs87bA7uSQx8d7v9JJnEFpXMVX2Ts1Z,2hxJnNN6sHWyMsHJ5nFVRih71nTbDLHQi6Mrjip2D9wAMW1ryN8nLTr1AYRxTPBPfsth5fm7Cg7KdUfEHVVTvgPi
W13,W54,460185402,143,144,145,7049083411,6979184062,-6964602147,2ncky5ju1R2VSxEzisAXv88hLpshbb8YqGDu9wpcBjxoEC9eCwWQ3cPYscM4y2E4HYBhmWUqCqkS6wjQxYHtyaKS,3rPQvHukLEdDw2mfuMj6oxCmXU5ZksjjmV7EE9pZZV7rGWKn2WsdPDqe1W4hF6xQviPr7gzb3gVxTsQ2pSLW26Mn,37bi16WCqwTUwrmzLJdZVABMnCo7NxzwDxCXZHpNCmE4aSFCPEjEkVeSspDbcitMCxpu5YFRuthHhDxqqaLvTJKA
W06,W93,460186221,294,295,296,4063021435,4022982706,-4014276729,2nnyDMz4d9NmCqffmqfu3BA9LrVvnwuSajo25pi3Y7niAx9PA9M6hHCMfDZzU3v6SwsPNSPfX5RzRsi6dCHdZrhP,5zPk4Y8HvWW4hSrgTCkWBQjNC3p5AqpD7TmxixoB9Mi4YJHHZkziQDxVpPV5wckUGcNhY7jKoFaQWyKjp2c2rsM,3DxGabD2ZVhRkDQugJa4Rba2eurQDLmcQGbhJ4xc2QhCHv3Z5eySEWkp9spiXqLbH5Fzo8KTRT4PB2gXYwkVGYb6
W23,W73,460185064,189,190,191,2616816562,2591239881,-2584668308,4zwmkYDrwx5dtu6MWhfhKFEu3XKYwRqGqzGEPWKKHfe7uqS8J8jfuhvBUxzqmRQbKZ1BDfZnnHKim1hLqdZBox3D,21zLDvQSGNL2UiU7BuQu62pVLeKJXJ8b6PLFPMxusnwNA1Fe72BUnxvQ2BtLAT8ZTQ4ZHb16VPUidekRxg9cfFta,5JDd6XHGcVztrycJTVpgHytd64Xmst8n2ASHbC7k4bwEC2PkWFf9EgmnJYaJef8YJYkQgxJ96MBj3j5ebzxt9A4E
W23,W37,460185001,302,303,304,6452529330,6388595522,-6374355490,657dHFXoptz5Ef5zscqT6Jy9fLsaECVUmcZW86vNwBorwW1iVSpBMxw7MPUZm1syTgSc36coEsUF9HSSXjejeyYW,3LdgEGmSxxCLT32a3Fm5ECd6B3Z3vvg6Ag1zAHsyx8RmXS1kRA2bE9mBM4Yq7LC9khWNnDr85huxd3PzpoxY3i3o,2rhwsK6hPcWqkuFP3FZPiEB76iLfWAXVoxqdJoV7GJjUPnd8Z8hx81eMnEC8qKp3Q3M2zEoaQV89aPvWL4uuY8Yk
W09,W39,460185538,499,500,501,3665477273,3629413985,-3621333588,4wrXEaD8x7g8LPLsEPUX5wR4wVCZARrjjAMMWbHoRNv3QN8M3zzQ1dW1CJSH6nTSh9VcTEKAdDC1VV8xuDDwP8D6,25uCQKbdwnAb65xkZ8LBnKiTVG2rQQuZVzKiwgZiJsXSPN21Hr9jM4UZ2QPPmLs8x4BWQ78S2kydAhqZXEsa8ugx,5pHWVD7TpxyCEw18sYUPG7Pidx2wHbbSrkCWRE6UzAbX3XM6rUc9yKixrgENLKDAoJvx6EkXiVzNCmp9W4DXAmpb
W04,W62,460184630,148,149,150,342522615,338343365,-334951180,4KsvAMRWHNmx2Lz53zH1iB1ARFkxvVVMyuagMtqxhJq2S93NQ8oLigLKtWDQuqSavyvt2YZpN2y1NPwshd3EVXsA,FrYRc8qWLD77CtN1s15nriRgnMyVZdud8Gdi8PBuX7HiBHosVV2RpcxUhswSzZHjputUUH4chDvNSWob19tmNzQ,3C7a8HMr6WVxwEUz3LZy5oryVNgXZ5WfoQqTo6yVgDD8nEtXmVA22MYB5VDjSWf2HPY1iQf7MK9FGjN9KnRLr4su
W22,W59,460186352,369,370,371,5044254444,4994403384,-4983787207,2kMxoSeLXwuKcq9A4XRMvf85hdWKtuVmKUD1x4LMLVDhKm3MBhLe5nyKufrUz8FpYtHyMAy5DajAD2p3wNn8gCGu,2EW7fditrUbqSWtitiiSBxYJefpDDFoh5g6KngVe4yU86f5PHy8NoPyCoGBUDVvAUEw19w4avMK4CS1weh22bgYE,3vdpY8qZUSnp2xKEM6sCZ5VnKZPiH1u9xLaz8r6vucCTTy4hgKnkphZuKKWmoWBXapYQvceSxnTtxJnrXf3ncAtu
W15,W75,460184967,340,341,342,4877350985,4829168960,-4818461869,xUUfFn2mgUsQH8HnVNv3f28PiazjZJvhK146tXhYkXu16f5UjrMZthbhZgkKRRAdwDDUz4aiqgxxfyskrmzw2Rn,2e3Ar5MjYSYvBLmP79Zo8nvfF9oouJQt72HfRv3sxiyGgBPTD75KXFq51aZhX7qanpgqQLfHBceY22Y1j8aQxCAG,4Hs8RgAjf58CBfqMHRvVtVYdJvkDFa8EQ6KWYo7NUpiUJVd8K1tyJv3HNUcRgPapZgM61cWnXk9sdcULY8JWGebK
W11,W91,460185130,321,322,323,3252415726,3220483054,-3212842970,4skJrRD53Vrq4tX1oGVbhC2jXVj4W5mVMHfTBn7ksRJu3AR9T6mxXKuuKDst4AE6UZHWKaMmaKyPjXabMWsd7og8,6tJt9mN92Wz3Kcrj1QvSqaFMtwewmeZyCwjX8g5P18Px6uZqbxY4R4XAukc68LV4FP5XRtT6s4E1rPWRRE94HS6,4uDsENMTxyNiBRtephNnkkoViQBm9mqPQUA54uLriQ5BiFYbbzYUV1kY3C93cSzhG3B1K71FKTimCwV3GkbXn74K
W20,W53,460186049,154,155,156,4712997918,4666459424,-4661089311,3Kcj8eCZ1CerQkvhFXkQhWmb7RDHwRym2nGj68BkSDQJmegpCEm7HnGsS15VfkMgXktqJ4UiWmY8JoempRNymoGp,3CcAgNXcv1co8VnDbNEAB5hLzSBRwCcKwyHxadv6fXhCyzi49umywsnHKwee2zgBMipQucUYGSgarK1Rq9VS1bd5,2CpqhjXpeP22QZvUKGtpYnDWekD9NBEHtiJNDri9NcqNbzypJ94qCcbD5uSMF6cNnbnKrsJELKM2yTtuSs9o7Qm2
W24,W74,460186084,116,117,118,9103006239,9012567662,-8992806959,5mDHNASyRtaC5SNTBnfwCPVeXXYKquStt8XajkuK8sWryfqMK2LntABnxRSe2XHFZjP3KoTQw4FcruB3KYPNHYQb,Usivx6eeCqxvTs2Ud1RwkoPvhF65KvwvZT5YyWKVyZ5MRFP53RDy3Wv1cLzroy41pmL4F1uFpr3CjgeFKUGzCQF,rik2udSXo4vU9WZnSMyLhfw4ScP56QzCjSguPyrNaaDq7FD3SjwjbwZbhRcpT76YudKkjqAo9npLKswnPC4o4BS
W15,W64,460184934,187,188,189,6910900975,6842383450,-6827060274,39rB75eyFqFCqiVnvuVWsz1cnJviSCJtynLReimBpBp4F9u6UUUFJbXNRZLWjmS2HDhxrXa8CEKgijG9kK6Uy4Tj,j3jBxrb672erBq7EMwKgzmEKVriqodDPqfWLz3tCjFrEsbavjvbWiE4BPpMXBZbcvBv3Uf76LRLDPZvfc69Bn4L,5vVWU6zouhmrtFoawjB1mSc1ZTnheKxXsd2Fc1HrVfAc5waoRfV1RfTUrjFE9faKjnqHisTRH3tUUubLiaLcn76x
W10,W81,460185881,399,400,401,6923093806,6854454353,-6841367238,5CcJsHiuSwaYcGUpWi1mtZbT73x33dq891cLhCrAvM1A62dV9RDqAeFgVPaqiJf6Ua8puh56AWcFNfUtd4Udfydm,gLKCcTjwTXhHFT2hV6NtLsLd8UvdU88s6ohw44L5PjVWnrzyWmkiiyrNN1x2u8mADBBsXQJatocRWH3Lw3QgVL8,rHuEFkCWgaNzqfFCNyw4g3yZwRnLvCwruPDwYw4zc72ZWSoumJDchDTd1LAYwxLoyiZsLKy1hFNDfpWPAVgpZP6
W02,W48,460184090,537,538,539,966907447,956356302,-917830738,mFKp9wBNcoh8UadddWioXha6Pz5Kq1q3ieK5PjecyMSsGpDMcszL5bJHmdgyWtKkC875TsoQzyt4FoXeGeUoi5N,4sXEJj1SmXLTyZtBvWrDsrNcU7JGMQKxnRR2EUDpYFrWGp1qDVjU8wneyCRm5KEqwUyVoWbtiAXXnfoek7CCecbM,ZDgLaBSfXA499JmyYwejYo96EkhzJK1n2PXUTgYhaN8CWdix21P8UWaqXGBwk6z7Fk4f8a9h9RyjUL6Y9j6YHSv
W20,W66,460186015,427,428,429,7335271214,7262509987,-7251406162,KVYnXnbzWZRpDNLi9ohhSf6aZTWFCBmUTnDwqemprTjqNqQnYBVoCLZ9RvgLn2HxxcJELwsgvNFLx5xAypCcvGY,9wD2RAjNZKcPiMohypvPpjoHBN4qTd8u1nbes6LPFyvQpp7tSkKHvMJZDynpNqVbeayDjos45x7MjybCEVV6MGD,55aL1G6eu9uqf7vcbTy9QyTj73sM59PRGiPxp4KvfxP96EqAvCh1WpJFkQtc37DM5UZsYTsGFUvRGQDF2bVu5hTc
W10,W89,460185949,267,268,269,3454681294,3420725966,-3413076019,43PKvAuMDiLfVnyny3YhXDJBSDfKTwLfWHp8HunWbu74GWYBPbJMkbxp86qV6MLxSQoG2eDekFNGDthPjfoN7WR6,63GzVmb7Hbb3G7G8PVjzRaBDcNwhdFp1fBxYy8X7iF3BdRVR6otTDDMWBxXw1n4dgR2NahTyhx9hJuz68JvHutDe,3UWy8tmhd5PtbD2W89NCJG1GZeaJnzJpcJj3HQtjQuD92Cq6SSwjkL2NVJjV6ysGNkH6CjAhuvUdJHL963ZzXnGK
W12,W38,460184451,198,199,200,2423001635,2399363104,-2394218657,5yjtAGgPQJyLcATrS15oLHHWM6b6rbMRqdduTimhSGSoWSNbJfwQQG8UvY486bomvqbdH2hicPdtFesVPXgQuNMQ,3H3Six5JaYtKTdyQD6bFW5M1hQT2iXaeBJHZcRCiaG756BKbGDgj1rz2tv18Js7BBeDDzuySRKSWtRJCf4sqY2h3,4e2KRT8ZkSPwV1VEq9GisMpNsMvTwTKWqYFpvHfoWrqixSV2HEyFMdooRXqyzKjd58BNNyG3GQR69RAy8zLN9HRo
W25,W92,460185781,15,16,17,9320543350,9227929401,-9207998092,4PdAUCV1vXbrAvnHMjzkjnq8n62fKdYUfEKaRZEavy4KNDEGpGgquVx7qWxcfyTBsfM2EaViii4CZ9VPYWjRuafm,5CRByfUJV2UHubqJMcoJWzhrwcTXvzj5WnnAHxWzohzLb8tJtCJKWVF4QR6EaMHPAgwUXgbwMWNsed2dBjmR3JDQ,4M6uE1aEpjUY8P58D8s9TQjG13CH1KJbfCWruKCCcrtSpCS4R2Da5Kxd8wkSNDQZdTXpFBLrAXqJp1PVvejtFbpu
W26,W79,460184666,290,291,292,3472589855,3438455441,-3430394053,5a8tjJWbE2LpSN84JVbZyRKPzLsE5eRN4CxgosKA6RevceDGSRDjPDDB3dmScSsEQKzNMi4QuBQL8ZbQdET1WZBy,3bPEtSd2cJoFYDcFt9rqQsi4qpQMJjziU2yAPw21fY7QGtwPLZMoUv46MsvJhRR5Tqe9NVP92PA4qUWxtxfZoT1m,2LC1ywqikbgyF4FD3Eo3qGhth1xgs862Wicb9wmBcFDJQ94yoGAmdrREUZT1nLMyssybGKYR24bdHNHEv8NBg7vJ
W20,W83,460185981,349,350,351,9826245676,9728574704,-9711513567,2fA6jFQkTjZ3JkabHzmnYvCR8vi5vkKQq2EPL1jPgiD5XmnEYacfx6AXGHro2GrLW8jFM24AvKiVdETMz3qUaEiB,54NnkwMFgmUkhyWjrDndPXhwiFghzToLMCp7P9EuYbE1Zzvozd8J2wF9o6KNC6Q9FoF1FWckiwMU3VBymj4oST1v,4CJniMjLqyrBJWXkVBnQ6gaJb8w1h4Js3AQwznHia7bhif8qBAtr3D2Kxa4nC2L8g6dw9v4hMEkKsUSBStptdFom
W25,W35,460185578,823,824,826,556645387,550573201,-542787858,B5Zq7tCucNjH32xzY2C7ua8eygTzFPb1b6Y5YH3nHcDbYD15DLwE8qeRHqJCvFu2TriXDQrzWQn1Skj49tcECNe,4T2usb8MBUzxP5qQwTPVDZPcuj1yGNoQW9L8d6yg8M6UBbpWz1M3HZxreU89pxRavTV3K99s9p3DSZVfyPnN7hxF,5zJNVvY1GpVwzEzGeqQNAwKEWmYF2q52UdNwktVpgb8qbLedSEsjZzMxwGWsQhz1QCTvogKph1tTsGCAAeqA7dtg
W13,W69,460185437,576,577,578,4238427112,4196634326,-4187640427,4RaYwtCXtLHrAeEPTVc4jQZbYhsBn1UigmNWgXSj3YFN2SCWCqVVvnd4gFAUjikprVyauNbuYFRxLRhWCC9uLkGR,59pprxxbdh5a1HB9x5EdBy11QHF1vmxVev22NS24Ss81Y3KC3ZhtoBZMt56iFMttfkXRS8TJVGDL3oQDehLdAAb1,3cUPNWrko1GqWn9Ct6RkgDYBTmEvC67Fb4oEwZFHeHnY1j93BPL1es6r2LdSpkP7fXMpc8ZuPWJT1QJwrQirHjWR
W04,W87,460184518,260,261,262,1694387983,1676646758,-1672286544,3KjUVPvVLqDWimgKH3fBTVmYPqUwEMP79BfP7KDBeAx1DEcxPijYq49X4uGKqqgaTyzeGryCtbJsWKVPZsfZ73xP,5CHM3F5SngqnfMbgcEfXqfarbvqEdb4UDzPdfbSjFkXeEmDtLjzPv4pNEaL9rJaM9to8ZPJ7x99Gw23PNzvCfh9Q,2DzWauFdj1ytWuBaTY7tHSvxuqL8xsUaKZz8c1A63ZyLQQj2LoRKYwNRjvrZanoXzLYaDj2Fxun72qtd9CBE8RDD
W12,W85,460184223,99,100,101,1987890020,1967129049,-1887764183,2X5GdpnniTQWLWPqeXCq1LKPTinA9Wn3e8ksBSnkWpWqaPddPHE7U7oWV1u5KBL1PqDAkPNbqAA8rJXvMMiyQ6f6,VvwjG6b8oKiVPeiWbJgjap8XTaRdahTwsQFHjLEeErH4H1LgMbkAbfSpM1EZ1TEZm7giwsZ1BqHRiYXxzRGeg1T,c1AZv1KM73LmHyiu3n619g1sghoFMJb4Zf9oJRgMHbgYJvA4tKgJ9NF7TJnGBXDvMnu733ofpyodEXJ1KYSqkYE
W07,W36,460184124,225,226,227,3135715595,3103476368,-2978198479,3VM1bJNExj23EqZXJis77QnU37JiT7fSuUUXtQggxLT184uhGYFEj5Fu5DMVBe76Sjg9Zotei8bREr8XTCESauvZ,4GmGfpEt2AtzKMf63voRF2wyK7gFSKt3SjC1JAbUXTH9M3odqw9WTYrecZLBphXCi3GUqoSFd2GUXwo9dqj4jbQ9,57EYicFAUC2S22JrH93srj7g8TX97YoUW5JEhH8uAet9Y2nm6tfxgh3fXqoHHi7xWCFxvnPv5RqjkN74uJMjyLhn
W21,W77,460184864,123,124,125,4466970747,4422892524,-4412970609,sgbVxGKDpxwuNXEvJevs7K3Y4T67vpheBL9TQAjP48sfcXrYE89F3JyHnDpj3WpNcmVAzXeZ2EvDaMvbPospbRM,3SvFSaDjKiawMMqwjqo2qkqvqktvrARGUJDnUSAsjH3BGNVJEgDeD2N5TXDmhLnb9whNGUBJgPKHHF4oUa5pv27N,4f1LfAEBzZUmFYg9YeGBn4Sq7X1GzfdiTS6R4YrvEkxjC9LKpUGQZp8zZG5kFcxW3QzTLjRtm3YsvmrUkS9ajKzy
W11,W55,460185196,371,372,373,5608124612,5552634851,-5540084769,y5wCnp8BHMscGmdsTb2nDbvjprF3ZCNMMr1qiH5SyGXSAj49ng5EqXVqikMy8dYXV4ViSecJxNikgFvj3P851SM,8bFsurq4fydyfDr9V383pCtP89tWfR1iwFWJhPfnwxtVEbMfmNksfZsN3Y7XajMAQHkWkQ9RUXRxopweHLWLhUW,XszQSz6YdPTFfgMJYSEG1MWYqSjwnYKAwzuTmmt7UAjJpUBmstf44CJWtzxqF3w6zTQ844DwjThcuntwwjt384Y
W14,W41,460185709,158,159,160,5932958386,5874220287,-5861853029,5Fq7NAFt3FETJskD7o52K4r3wJctWPoziBzJicDJQxGTRwaCxis2uSE7m5fpoW2qskzvoZXXDy8B31XHyLiUZs9X,4gAa49cv6QnUcHFP4dnpXkWJ6m46bRjZ4H6VhCGQ7FuGjnFmY3BBgCR9t9xauB2jGftvXgK1KUqLpPzXjodXUetm,2Fs4yraLjNe2VBtdx8zNHPHBk5r7WWcjLr9AZjmAzxNBdUsdaNFHaNUvgxyrDLynHCN5wYfWt22m9t15sctUmbv7
W19,W70,460185641,114,115,116,3170451219,3139338192,-3132108473,5T2Aa8qeNWUWWfkJSxwHVJqYRRBK9dwWYQ8WG5771Jj6JkTcpoxUd1rRb5Pmfk1zKNk3ouZmNDdPVZ1rJmZ9argi,GeWsBmhLck1nXwqf8dYhxw6fSbmHzpn5Aoe7H8bdTtMNacZXnBqQQzsEMFGCGWJSdvGwAuwk1tvPqrvpDaLjT7c,5coW2XtqWcev1jwBWkfmP5kkiXnYXr8x9nj9RW5PbEK6X7NZdHkk2swGaCEWa2Nw7ymJeCNwxnMnsKg4YEguE9Bx
W24,W97,460186117,163,164,165,9799838343,9702431444,-9681131133,4MPQh1s8A1Dm4pJ25o9ZEGtnnx9LLiDhzvKE2a6fpweo7idU44jRrVSLZ18QPFLT8nV2CTtWH449WMELf49zFrjc,3okJwpx7zbijfmc4FuqRUDVo6nUTgLjVtQBdVHXLApR2GCAytZvAXKR7jjLF9MnFCD7em1D2Djwvr1jQ4afLnyo3,3CGcbvz7iDC5Ret4tUkfqKttaY2LXJc65igByD3LcTaVNvBXy4DU8q3YcobgihZda8682xTHTuGAFvGoCQwucgDQ
W11,W43,460185163,243,244,245,3144567319,3113713131,-3106706749,4pUrNNGwTnRJVtmh5exNi3rzos8NJEQTHoVYjyC3ZzL3oSKCxkCqsPZWiSb7oYc94dQgFTvxVRTtDNPmF49si9f6,555MTDK4RLLkeTb1EeVXEMGJJs1Vrr4HtJCaC1nxLLiqKHXwHbGUQRTTJ7o3q2c2wK5mynEzLR8aMdKCFzRhnfkh,5kw2L6DPBBNgPzY1faExqgGu8g63tkRbkQQtMsGrAsQUbvQnFGJTamanrQ9nNr4sQbBnGeySxbJHtW2NgNJ1nhv
W17,W67,460185299,295,296,297,5931663273,5871570955,-5859201724,B8qqEJGqc8yUSgScAwEcyrWMtAaV4spK8UQgQKNEVonKRrmJKH5pxjCWRuzbQvKda6qqy4VcU5Ej3JzTnP1cZzi,43msJxqu77sYsKHnXNBYWVL7wZ7vzQAMP7hfyuE1e6EBjTkFTUCHTX8NV5U8q7GZNRWDSmbK1SvTmZWbAtd9Uwkt,3ktGxZgHySKQ3DY9KC6EY4dUUAHRWuy8mfbQeiMf5go6iQCPpv8BcNqDd2W7LpzGqbRja8VjRDfyUjjYZ2rTve5Y
W23,W31,460185098,215,216,217,4407719698,4364233986,-4354383908,7qvkePwwRbMYu3pzsW5G68N1STcABt13tBs8eHE4R6xFY6cp3YjVPe2MbX8BJqnPZruA6HTgRE6qFC39puE5Jkq,2P3rdQDnBqX1ivvA2PY3W4jjhTZS5rSoox3tXY2CKQ4ihiVHbbopzSUtSUHTryHuGmb3FQCQHypycHP2fBtcpQDk,5amWAeMnAQurvu68sA6YVcPjEgvr84UXobUAy4jvRA88PFDts8iPZWq2CpbzNpaPSzPBppMR1FcDvNVg985kByp7
W26,W78,460184765,369,370,371,1955468121,1936504925,-1930998479,65vgt8rZ1xs4JTZc4shkcodryjGPwwqVtTJWqS7zFNbXPUEECQzpbouLCUE6DmNvxLAQA3AUEA1vorwaeUjULPfs,3DWBHBxNbBZFuuFyCwBG6pqM61frxtL9goWhvtvt92yhLccTgmzEUNFCuMT7mAL9ebJsFSQSMHR2A6xdFVhTEYTe,2CixoFBzjcAatw7iGoB73TpfpMYdL6p7RgC4GFpFQ5G1Yw9ADuFZgxoP3tTxoXWPRDdRrEitXU3eoJyFawHK5Jpz
W17,W84,460185264,381,382,383,4597852497,4552465457,-4545580220,4PRXEwQEXXyyzwwizdx8PixX2EejakB9wA7dq1pfy4m4EiupdWL8SJ7HpdFTNmWxqPLoQb5FEx9CHMYkEvibekCo,33idSWpp1hwYs6z2SeLGaSfcjYksCttyRMsju4QjtMibcfGd3wH9XLJmaksaV661CocbWJKHQum22a1NCc8C5KS,4hAhsB37wVFmDspTmhg6zAURFqLpcpTn855LxbuaqMb6CGrqENjWXefs9TiaEKDWL85vEhMGEajRDFxcNaMXwpDf
W61,W96,460189209,115,116,118,299363989,295864617,-290924423,4EyJP64dFrmPgNmKUEcDWTD3gpZFLAK5DCDQbFrTxE1a41ZvAPexYafPmueeVvjAS3EGdPG9pkVsdx3opuawZFW1,5XkdzmJmmGPhpQ3hvcVBFkLqwRmrVUbKfsMmsoNQ7cKFp5po3urvirQwhBVnsSxVuG99bmMRby8tDUCoiVim4Poq,U6cRtpSeZZR2oYq2P9Yig2iarjkwFnnQ4oaCnhkYscznwv5L5gu4Z42MwX11yL7FuMdZNxKLBbubbTNtWi9G5rf
W82,W56,460194294,195,196,198,56214709,55146830,-52885797,3Ty1mQk1YVk3J48bVAKAbhmxGU6nko3HV2ktwHWBL2tNiDMV8DiAYgyfXWsZyLJdiXpWYAbRdb7hq3cYtcFyJE9u,4jQLguqmqiUMWDYrGoKgXn2E9sjTXoqigmF6vgepxTQNQ8AvNNYyPPx81mPniVddhGvvKYpSaaywcwJTHpRjctzX,5Kp3gw11apV3vXinVJJjSvF5gyX6L6HKVnQkcZFn3mnitS4JcVzTuaVFTaDPP1mH6iAnr94sGyqsDahMejn937Ue
W64,W32,460186706,123,124,126,602501810,595971060,-587678835,67rpngtrYLAwC75FbzuEyZhGbQb4rpsxxkPC6DwfemR9aQw2tsKv4Rij2Yrpi3GQu3YuCM5BjMv2ycEWAxSNEFuG,2B7GBZXrUNMWgTQ2aUG2pyM7JvKqfw6KQw8tkNitFsy5eGRnako1hhhQ2GoMnsnFGkYve9mQwZwnY2YFECNMLjjA,2G8HaqNp83HqYkfCgBNc2A3ZLK8f3GfYRLejUqnz9AKE671ogXoZK4RLUQ1eZXCqBC6A2mBTJEf7hPQ9mqooiSx3
W97,W63,460187952,314,315,317,282376144,279046651,-274293956,5eYyUyJKEUhHyrLj7bfguxYEq5o6jVH3VhNHY2jgc8jPK3mBHjzW59KQuQtB7fWrExze9neZqZjFMwE2R3DRE9dz,3yZpgSkrKFuMXdEKizH8cGUTkNwMHZM1gU8ga49n7X4EGRuXLZagPLoEZzRoLYJt4d1hGD38VuTuCZZgsJ4uUYYG,5oENTkWssUGR1Nk8DMXhTxfSLuMmAxtMaiKNy5d33eM79RZkjkSP4XUQn1nKzztTDrkxbr1379rc4k2GEzCeYfDk
```

### F. External-recipient swaps

```csv
address,swaps,SOL_net,USDC_net
4FCBP2WKhfkEDvTg2YDCFzpcNVQ9jt6qwoKnPAEQqHiU,1,-8.6001e-05,101.314274
8zQherSLQCsGYBzAi6tPUBDW1VK9GNkTBhPQtDmRQpW7,11,6.522689489,397.886817
9Tfv6K5RadxWRbFuGCF56JY9i1yf8TDCY9AGYH4TjnB,1,0.0,99.496916
CgXBifeSeYzrDya5mgV5o6art3EdneQZ8dnubuMM4CcC,11,0.0,1146.242732
DNnrBVQ8Rk2vP7w2YhKHC1frPGmdj4kyqSTYD2QdDrpK,0,0.0,0
DqknfnupGSaYFRdwUhARsCnJC3iUMZS5kiMK9T1ShHKB,17,-0.06073468,1277.470569
```

## Review deliverables requested

1. Recomputed base and expense-scenario totals, with discrepancies.
2. Whether the 68 repeat purchases are included exactly once.
3. Assessment of common funding versus common ownership.
4. Missing evidence or alternative explanations that could reconcile 70 SOL.
5. A clear verdict limited to the stated scope; distinguish supported findings from assumptions.

Do not state that raw transactions were verified if you only reviewed these derived tables.
