
| Operation                           | ns             | µs         | ms     | note                        |
| ----------------------------------- | -------------- | ---------- | ------ | --------------------------- |
| L1 cache reference                  | 0.5 ns         |            |        |                             |
| Branch mispredict                   | 5 ns           |            |        |                             |
| L2 cache reference                  | 7 ns           |            |        | 14x L1 cache                |
| Mutex lock/unlock                   | 25 ns          |            |        |                             |
| Main memory reference               | 100 ns         |            |        | 20x L2 cache, 200x L1 cache |
| Compress 1K bytes with Zippy        | 3,000 ns       | 3 µs       |        |                             |
| Send 1K bytes over 1 Gbps network   | 10,000 ns      | 10 µs      |        |                             |
| Read 4K randomly from SSD*          | 150,000 ns     | 150 µs     |        | ~1GB/sec SSD                |
| Read 1 MB sequentially from memory  | 250,000 ns     | 250 µs     |        |                             |
| Round trip within same datacenter   | 500,000 ns     | 500 µs     |        |                             |
| Read 1 MB sequentially from SSD*    | 1,000,000 ns   | 1,000 µs   | 1 ms   | ~1GB/sec SSD, 4X memory     |
| Disk seek                           | 10,000,000 ns  | 10,000 µs  | 10 ms  | 20x datacenter roundtrip    |
| Read 1 MB sequentially from disk    | 20,000,000 ns  | 20,000 µs  | 20 ms  | 80x memory, 20X SSD         |
| Send packet CA -> Netherlands -> CA | 150,000,000 ns | 150,000 µs | 150 ms |                             |