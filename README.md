# heavykeeper-rs

[![Crates.io][crates-badge]][crates-url]
[![MIT / Apache 2.0 licensed][license-badge]][license-url]
[![Build Status][actions-badge]][actions-url]

[crates-badge]: https://img.shields.io/crates/v/heavykeeper.svg
[crates-url]: https://crates.io/crates/heavykeeper
[license-badge]: https://img.shields.io/crates/l/heavykeeper.svg
[license-url]: https://github.com/pmcgleenon/heavykeeper-rs/blob/master/LICENSE
[actions-badge]: https://github.com/pmcgleenon/heavykeeper-rs/actions/workflows/rust.yml/badge.svg
[actions-url]: https://github.com/pmcgleenon/heavykeeper-rs/actions?query=workflow%3Arust+branch%3Amain


[📖 Docs](https://docs.rs/heavykeeper)

Top-K Heavykeeper algorithm for Top-K elephant flows

This is based on the [paper](https://www.usenix.org/system/files/conference/atc18/atc18-gong.pdf)
HeavyKeeper: An Accurate Algorithm for Finding Top-k Elephant Flows
by Junzhi Gong, Tong Yang, Haowei Zhang, and Hao Li, Peking University;
Steve Uhlig, Queen Mary, University of London; Shigang Chen, University of Florida;
Lorna Uden, Staffordshire University; Xiaoming Li, Peking University

# Example

See [examples/basic.rs](examples/basic.rs) for a complete example, or [examples/ip_files.rs](examples/ip_files.rs) for an example of counting top-k IP flows in a file.

Basic usage:
```rust
use heavykeeper::TopK;

// create a new TopK with k=10, width=1000, depth=4, decay=0.9
let mut topk: TopK<String> = TopK::new(10, 1000, 4, 0.9);

// add some items
topk.add("example item", 5);
topk.add("another item", 1);

// check the counts
for node in topk.list() {
    println!("{} {}", node.item, node.count);
}
```

# Other Implementations

| Name                       | Language | Github Repo                                                                  |
|----------------------------|----------|------------------------------------------------------------------------------|
| SegmentIO                  | Go       | https://github.com/segmentio/topk                                            |
| Aegis                      | Go       | https://github.com/go-kratos/aegis/blob/main/topk/heavykeeper.go             |
| Tomasz Kolaj               | Go       | https://github.com/migotom/heavykeeper                                       |
| HeavyKeeper Paper          | C++      | https://github.com/papergitkeeper/heavy-keeper-project                       |
| Jigsaw-Sketch              | C++      | https://github.com/duyang92/jigsaw-sketch-paper/tree/main/CPU/HeavyKeeper    |
| Redis Bloom Heavykeeper    | C        | https://github.com/RedisBloom/RedisBloom/blob/master/src/topk.c              |
| Count-Min-Sketch           | Rust     | https://github.com/alecmocatta/streaming_algorithms                          |
| Sliding Window HeavyKeeper | Go       | https://github.com/keilerkonzept/topk                                        |

# Running

## Word Count Example

A word count program that demonstrates the HeavyKeeper algorithm can be found at [`examples/word_count.rs`](examples/word_count.rs).

### Usage
```bash
cargo build --example word_count --release
target/release/examples/word_count -k 10 -w 8192 -d 2 -y 0.95 -f data/war_and_peace.txt
```

## Running the basic example 
```bash
cargo run --example basic --release
```

## Running the IPv4 example 
```bash
cargo run --example ip_files --release
```

## Run the benchmarks
```bash
cargo bench
```

## Benchmark the sample word count app
```bash
hyperfine 'target/release/examples/word_count -k 10 -w 8192 -d 2 -y 0.95 -f data/war_and_peace.txt'
```

## Test Data

For information about test data format and how to obtain or generate test data, please see [data/README.md](data/README.md).

# License
This project is dual licensed under the Apache/MIT license.   
