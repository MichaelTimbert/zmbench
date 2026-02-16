# Zonemaster Benchmarking Tools

This tool automates the benchmarking of **Zonemaster**, a DNS zone testing and validation framework.
It runs predefined tests on a list of domains, measures performance with **hyperfine**, and consolidates results into a single dataset for analysis.

***

## Overview

This script automates three main operations:

1. **Cache** — Generates cache files for each domain and Zonemaster test type to speed up future runs.
2. **Run** — Executes benchmarks using `hyperfine` for each domain and test, exporting JSON output enriched with Zonemaster version details.
3. **Gather** — Collects and merges all benchmark results into a single `dataframe.json` file ready for statistical or graphical analysis.

The goal is to make performance comparisons between different Zonemaster versions and modules easy and repeatable.

***

## How to Use

### Requirements

- Python 3
- [Zonemaster-CLI](https://github.com/zonemaster/zonemaster-cli) installed on your system
- [Hyperfine](https://github.com/sharkdp/hyperfine) for performance measurement
- `pandas` for data aggregation (`pip install pandas`)


### Input file

The script expects a text file (e.g. domains.txt) containing one domain name per line, for example:

```
zonemaster.net
internetstiftelsen.se
afnic.fr
```

This file is used by the `cache` and `run` commands to select which domains to benchmark.


### Example Usage


1. **Build the cache for a list of domains:**
   ```bash
   ./zmbench cache --domain domains.txt
   ```

2. **Run benchmarks:**
   ```bash
   ./zmbench run --domain domains.txt
   ```

3. **Gather results:** 
   ```bash
   ./zmbench gather
   ```

Each step automatically creates or updates the following directories: 
- `cache/` — Zonemaster cache files 
- `output/` — raw test output 
- `hyperfine/` — benchmark result files
- `dataframe.json` — final aggregated result table


### Options

By default, `zmbench.py` runs the benchmark for **all** available Zonemaster tests:
`Address`, `Basic`, `Connectivity`, `Consistency`, `DNSSEC`, `Delegation`, `Nameserver`, `Syntax`, and `Zone`.

You can limit the scope of the benchmark using the `--test` option, which allows you to specify one or more test types to run.
This option applies to both the `cache` and `run` commands.

***

## Future Improvements

- [ ] Generate detailed performance reports from `dataframe.json`.
- [ ] Create an HTML summary dashboard for quick result visualization.
- [x] Add an option to specify which tests to run with `zonemaster-cli`.
- [ ] Implement support for custom benchmark profiles.


