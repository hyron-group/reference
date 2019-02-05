# benchmark

## Environment

-   **tools** : wrk
-   **time** : 16/12/2018
-   **device** : HP 15R-020TU, core-i5-4400U, 8GB ram
-   **opera-system** : Windows 10 with Ubuntu 18.04 installed (developer-mode)
-   **test case** :
    -   **method** : get
    -   **result** : return "hello " + query.name
    -   **source code** : check it out in [hyron repo](https://github.com/hyron-group/hyron/tree/master/test)
-   **test method** :
    -   remove the first result (cache time)
    -   average of 5 runs
    -   Pause all running applications
-   **test unit** : request per second (rps)

## Load test

-   **nodejs** : ~12,200 rps
-   **hyron** : ~12,700 rps
-   **express** : ~9,200 rps

## Conclude

-   Hyron is about equivalent to the raw node (slightly better)
-   Hyron is ~40% more efficient than ExpressJS

## result :

**Express**

```bash
Running 10s test @ http://localhost:5477/showMyName?name=thang
  2 threads and 10 connections
  Thread Stats   Avg      Stdev     Max   +/- Stdev
    Latency     1.07ms  259.72us   4.74ms   88.75%
    Req/Sec     4.68k   415.42     9.46k    93.53%
  93571 requests in 10.10s, 19.19MB read
Requests/sec:   9263.46
Transfer/sec:      1.90MB
```

**Raw-Node**

```bash
Running 10s test @ http://localhost:5478/showMyName?name=thang
  2 threads and 10 connections
  Thread Stats   Avg      Stdev     Max   +/- Stdev
    Latency   798.07us  181.95us   3.86ms   87.81%
    Req/Sec     6.19k   644.89    13.79k    95.52%
  123746 requests in 10.10s, 12.98MB read
Requests/sec:  12252.14
Transfer/sec:      1.29MB
```

**Hyron**

```bash
Running 10s test @ http://localhost:5479/showMyName?name=thang
  2 threads and 10 connections
  Thread Stats   Avg      Stdev     Max   +/- Stdev
    Latency   772.87us  170.68us   7.00ms   89.40%
    Req/Sec     6.39k   251.13     6.81k    79.50%
  127074 requests in 10.00s, 14.91MB read
Requests/sec:  12705.44
Transfer/sec:      1.49MB
```
