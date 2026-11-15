# msbd5017-data

Point-in-time Ethereum mainnet datasets for MSBD5017 (Track B).

Each archive holds a `manifest.json` (`dataset-manifest/1.0`) and one JSON file per RPC
response (`data-envelope/1.0`), content-addressed by SHA-256 over RFC 8785 canonical JSON.

| Archive | Blocks | Files | `dataset_root` | Archive SHA-256 |
|---|---|---:|---|---|
| `weth-wbtc-is-v1.tar.gz` | 18,223,165–18,908,894 (2023 Q4 + warm-up) | 54,864 | `0x154d1344015a45be25d96686cffa78520c0620fb52730c147eb75b28a982857e` | `072597b30c26d61b82d39b5164bb2ceee3b2499c1168d0510697f93d7e12bb72` |
| `weth-wbtc-oos-v1.tar.gz` | 23,450,444–24,136,052 (2025 Q4 + warm-up) | 54,856 | `0xbb5659d01647e4e1e64347a6c34aab7643ffb3459df26bf4b9ba8873dba757bb` | `06dc9ff27118a5862cfd9566b275291edc79f74ad02a5a89cebd4e6679372f13` |

Contents: Uniswap V3 Swap/Mint/Burn logs for the WETH/USDC 0.05% and WBTC/USDC 0.3% pools in
100-block pages, plus `slot0()`, `liquidity()` and Aave V3 `getReserveData()` every 100 blocks.
Query version `queries/b1-raw/1`, metric definitions `metrics/1.0`.

Verify with the project's verifier, which re-hashes every envelope and recomputes the root:

```sh
python -m scripts.publish verify \
  https://github.com/arianaxinjie/msbd5017-data/releases/download/data-v1/weth-wbtc-is-v1.tar.gz \
  --root 0x154d1344015a45be25d96686cffa78520c0620fb52730c147eb75b28a982857e
```

The root can also be recomputed by hand: sort `files[]` by path, hash
`"dataset-root/1.0\0"` followed by one `path:sha256-hex\n` line per file.

Download the archives from the [`data-v1` release](https://github.com/arianaxinjie/msbd5017-data/releases/tag/data-v1).
