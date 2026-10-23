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


## Files

- AI-REVIEW-SHYFT-EN.md: standalone AI review packet with all key evidence tables.
- audit-data-EN.json: structured data; exact integer amount fields are decimal strings.
- SHYFT-audit-buybacks-EN.pdf: illustrated report with transaction links.
- interactive-trades.html: offline chart with wallet/group/time filters.
- tables/: complete CSV evidence.
- transactions/: raw public RPC transaction responses.
- verify_evidence.py: offline verification against raw evidence.
- SHA256SUMS.txt: file integrity manifest.
