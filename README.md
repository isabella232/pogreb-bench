Golang key/value db-bench (pogreb-bench)
========================================

pogreb-bench is a key-value store benchmarking tool. 


Currently it supports:

* [pogreb](https://github.com/akrylysov/pogreb) Embedded key-value store for read-heavy workloads written in Go
* [goleveldb](https://github.com/syndtr/goleveldb/) LevelDB key/value database in Go.
* [bolt](go.etcd.io/bbolt) An embedded key/value database for Go.
* [badgerdb](https://github.com/dgraph-io/badger) Fast key-value DB in Go
* [slowpoke](https://github.com/recoilme/slowpoke) Low-level key/value store in pure Go
* [pudge](https://github.com/recoilme/pudge) Fast and simple key/value store written using Go's standard library


Some tests, MacBook Pro (Retina, 13-inch, Early 2015)
=====================================================


### Test 1
Number of keys: 1000000
Minimum key size: 16, maximum key size: 64
Minimum value size: 128, maximum value size: 512
Concurrency: 2


|                       | pogreb  | goleveldb | bolt   | badgerdb | pudge  | slowpoke | pudge(mem) |
|-----------------------|---------|-----------|--------|----------|--------|----------|------------|
| 1M (Put+Get), seconds | 187     | 38        | 126    | 34       | 23     | 23       | 2          |
| 1M Put, ops/sec       | 5336    | 34743     | 8054   | 33539    | 47298  | 46789    | 439581     |
| 1M Get, ops/sec       | 1782423 | 98406     | 499871 | 220597   | 499172 | 445783   | 1652069    |
| FileSize,Mb           | 568     | 357       | 552    | 487      | 358    | 358      | 358        |



### Test 2
Number of keys: 2000000
Key size: 16
Value size: 128
Concurrency: 1


|                       | pogreb  | goleveldb | bolt   | badgerdb | pudge  | slowpoke | pudge(mem) |
|-----------------------|---------|-----------|--------|----------|--------|----------|------------|
| 2M (Put+Get), seconds | 512     | 59        | 199    | 89       | 62     | 56       | 5          |
| 2M Put, ops/sec       | 3922    | 69029     | 10344  | 27368    | 58135  | 59590    | 553112     |
| 2M Get, ops/sec       | 947348  | 64561     | 329248 | 125174   | 70613  | 86120    | 1014628    |
| FileSize,Mb           | 1010    | 296       | 456    | 516      | 305    | 305      | 305        |


### Test 3
Number of keys: 10000000
Key size: 8
Value size: 16
Concurrency: 10


|                       | goleveldb | badgerdb | pudge  |
|-----------------------|-----------|----------|--------|
| 10M (Put+Get), seconds| 216       | 190      | 253    |
| 10M Put, ops/sec      | 95497     | 70840    | 42116  |
| 10M Get, ops/sec      | 89390     | 202284   | 617683 |
| FileSize,Mb           | 608       | 1870     | 686    |


### Test 4
Number of keys: 10000000
Key size: 8
Value size: 16
Concurrency: 100


|                       | goleveldb | badgerdb | pudge  |
|-----------------------|-----------|----------|--------|
| 10M (Put+Get), seconds| 165       | 120      | 243    |
| 10M Put, ops/sec      | 122933    | 135709   | 43843  |
| 10M Get, ops/sec      | 118722    | 214981   | 666067 |
| FileSize,Mb           | 312       | 1370     | 381    |


### Test 5 (switch to bbolt from coreos)
Number of keys: 2000000
Minimum key size: 8, maximum key size: 8
Minimum value size: 16, maximum value size: 16
Concurrency: 100

pogreb-bench -c 100 -d bench -e pudge -n 2000000 -mink 8 -maxk 8 -minv 16 -maxv 16

|                       |  bbolt    | pudge  |
|-----------------------|-----------|--------|
| 2M (Put+Get), seconds | 186       | 45     |
| 2M Put, ops/sec       | 10950     | 46731  |
| 2M Get, ops/sec       | 539879    | 761240 |
| FileSize,Mb           | 120       | 76     |


### Test 6 (switch to bbolt from coreos)
Number of keys: 5000000
Minimum key size: 8, maximum key size: 8
Minimum value size: 64, maximum value size: 64
Concurrency: 100

pogreb-bench -c 100 -d bench -e pudge -n 5000000 -mink 8 -maxk 8 -minv 64 -maxv 64

|                       |  bbolt    | pudge  |
|-----------------------|-----------|--------|
| 5M (Put+Get), seconds | 515       | 139    |
| 5M Put, ops/sec       | 9891      | 39402  |
| 5M Get, ops/sec       | 509562    | 394072 |
| FileSize,Mb           | 616       | 419    |
