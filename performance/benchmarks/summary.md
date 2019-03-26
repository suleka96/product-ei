# WSO2 Enterprise Integrator Performance Test Results

During each release, we execute various automated performance test scenarios and publish the results.

| Test Scenarios | Description |
| --- | --- |
| DirectProxy |  |
| CBRProxy |  |
| XSLTProxy |  |
| CBRSOAPHeaderProxy |  |
| CBRTransportHeaderProxy |  |
| SecureProxy |  |
| XSLTEnhancedProxy |  |

Our test client is [Apache JMeter](https://jmeter.apache.org/index.html). We test each scenario for a fixed duration of
time. We split the test results into warmup and measurement parts and use the measurement part to compute the
performance metrics.

Test scenarios use a [Netty](https://netty.io/) based back-end service which echoes back any request
posted to it after a specified period of time.

We run the performance tests under different numbers of concurrent users, message sizes (payloads) and back-end service
delays.

The main performance metrics:

1. **Throughput**: The number of requests that the WSO2 Enterprise Integrator processes during a specific time interval (e.g. per second).
2. **Response Time**: The end-to-end latency for an operation of invoking a service in WSO2 Enterprise Integrator. The complete distribution of response times was recorded.

In addition to the above metrics, we measure the load average and several memory-related metrics.

The following are the test parameters.

| Test Parameter | Description | Values |
| --- | --- | --- |
| Scenario Name | The name of the test scenario. | Refer to the above table. |
| Heap Size | The amount of memory allocated to the application | 4G |
| Concurrent Users | The number of users accessing the application at the same time. | 100, 200, 500, 1000 |
| Message Size (Bytes) | The request payload size in Bytes. | 500, 1024, 10240, 102400 |
| Back-end Delay (ms) | The delay added by the back-end service. | 0, 30, 100, 500, 1000 |

The duration of each test is **900 seconds**. The warm-up period is **300 seconds**.
The measurement results are collected after the warm-up period.

A [**c5.xlarge** Amazon EC2 instance](https://aws.amazon.com/ec2/instance-types/) was used to install EI.

The following are the measurements collected from each performance test conducted for a given combination of
test parameters.

| Measurement | Description |
| --- | --- |
| Error % | Percentage of requests with errors |
| Average Response Time (ms) | The average response time of a set of results |
| Standard Deviation of Response Time (ms) | The “Standard Deviation” of the response time. |
| 99th Percentile of Response Time (ms) | 99% of the requests took no more than this time. The remaining samples took at least as long as this |
| Throughput (Requests/sec) | The throughput measured in requests per second. |
| Average Memory Footprint After Full GC (M) | The average memory consumed by the application after a full garbage collection event. |

The following figure shows how the Throughput changes for different number of concurrent users. 

![picture](all-comparison-plots/throughput_30ms_1KiB.png)

The following figure shows how the Average Response Time changes  for different number of concurrent users.

![picture](all-comparison-plots/average_time_30ms_1KiB.png)

Let’s look at the 90th, 95th, and 99th Response Time percentiles. This is useful to measure the percentage of requests that exceeded the response time value for a given percentile. A percentile can also tell the percentage of requests completed below the particular response time value.

![picture](all-comparison-plots/response_time_30ms_1KiB.png)

The GC Throughput was calculated for each test to check whether GC operations are not impacting the performance of the server. The GC Throughput is the time percentage of the application, which was not busy with GC operations. 

![picture](all-comparison-plots/gc_throughput_30ms_1KiB.png)

<h2>Throughput Comparison</h2>

The following chart shows the throughput behavior when considering all results.

![picture](all-comparison-plots/comparison_thrpt.png)

Throughput (Requests/sec) vs Concurrent Users

![picture](all-comparison-plots/lmplot_throughput_vs_concurrent_users_with_hue.png)

Throughput (Requests/sec) vs Message Size (Bytes)

![picture](all-comparison-plots/lmplot_throughput_vs_message_size_with_hue.png)

Throughput (Requests/sec) vs Back-end Service Delay (ms)

![picture](all-comparison-plots/lmplot_throughput_vs_sleep_time_with_hue.png)

<h2>Average Response Time Comparison</h2>


The following chart shows the Throughput behavior when considering all results.

![picture](all-comparison-plots/comparison_avgt.png)

Average Response Time (ms) vs Concurrent Users

![picture](all-comparison-plots/lmplot_average_time_vs_concurrent_users_with_hue.png)

Average Response Time (ms) vs Message Size (Bytes)

![picture](all-comparison-plots/lmplot_average_time_vs_message_size_with_hue.png)

Average Response Time (ms) vs Back-end Service Delay (ms)

![picture](all-comparison-plots/lmplot_average_time_vs_sleep_time_with_hue.png)

<h2>GC Throughput Comparison</h2>

The following chart shows the GC throughput behavior when considering all results.

![picture](all-comparison-plots/comparison_gc.png)

GC Throughput (%) vs Concurrent Users

![picture](all-comparison-plots/lmplot_gc_throughput_vs_concurrent_users_with_hue.png)

GC Throughput (%) vs Message Size (Bytes)

![picture](all-comparison-plots/lmplot_gc_throughput_vs_message_size_with_hue.png)

GC Throughput (%) vs Back-end Service Delay (ms)

![picture](all-comparison-plots/lmplot_gc_throughput_vs_sleep_time_with_hue.png)



The following is the summary of performance test results collected for the measurement period.

|  Scenario Name | Heap Size | Concurrent Users | Message Size (Bytes) | Back-end Service Delay (ms) | Error % | Throughput (Requests/sec) | Average Response Time (ms) | Standard Deviation of Response Time (ms) | 99th Percentile of Response Time (ms) | WSO2 Enterprise Integrator GC Throughput (%) | Average WSO2 Enterprise Integrator Memory Footprint After Full GC (M) |
|---|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|
|  CBRProxy | 4G | 100 | 500 | 0 | 0 | 11178.81 | 8.89 | 15.5 | 101 | 99.22 | 68.229 |
|  CBRProxy | 4G | 100 | 500 | 30 | 0 | 3144.85 | 31.77 | 5.42 | 60 | 99.7 | 76.613 |
|  CBRProxy | 4G | 100 | 500 | 100 | 0 | 956 | 104.54 | 19.05 | 199 | 99.8 | 70.931 |
|  CBRProxy | 4G | 100 | 500 | 500 | 0 | 195.28 | 511.51 | 70.27 | 999 | 99.83 | 65.519 |
|  CBRProxy | 4G | 100 | 500 | 1000 | 0 | 98.63 | 1012.13 | 99.88 | 1999 | 99.87 | 42.525 |
|  CBRProxy | 4G | 100 | 1024 | 0 | 0 | 9211.53 | 10.79 | 16.32 | 108 | 99.26 | 66.728 |
|  CBRProxy | 4G | 100 | 1024 | 30 | 0 | 3142.73 | 31.79 | 5.2 | 60 | 99.66 | 68.253 |
|  CBRProxy | 4G | 100 | 1024 | 100 | 0 | 961.86 | 103.89 | 17.16 | 200 | 99.79 | 70.189 |
|  CBRProxy | 4G | 100 | 1024 | 500 | 0 | 196.09 | 509.47 | 63.15 | 999 | 99.82 | 63.194 |
|  CBRProxy | 4G | 100 | 1024 | 1000 | 0 | 97.89 | 1019.82 | 131.82 | 1999 | 99.85 | 56.412 |
|  CBRProxy | 4G | 100 | 10240 | 0 | 0 | 2222.14 | 44.92 | 44.14 | 219 | 99.06 | 74.072 |
|  CBRProxy | 4G | 100 | 10240 | 30 | 0 | 2101.8 | 47.51 | 13.39 | 100 | 99.15 | 75.998 |
|  CBRProxy | 4G | 100 | 10240 | 100 | 0 | 960.03 | 104.09 | 13.89 | 198 | 99.53 | 64.912 |
|  CBRProxy | 4G | 100 | 10240 | 500 | 0 | 195.3 | 511.83 | 66.12 | 999 | 99.77 | 69.543 |
|  CBRProxy | 4G | 100 | 10240 | 1000 | 0 | 98.65 | 1012.39 | 99.27 | 1999 | 99.81 | 60.955 |
|  CBRProxy | 4G | 100 | 102400 | 0 | 0 | 223.73 | 446.91 | 157.9 | 863 | 94.07 | 71.671 |
|  CBRProxy | 4G | 100 | 102400 | 30 | 0 | 217.21 | 460.42 | 145.6 | 847 | 94.27 | 42.397 |
|  CBRProxy | 4G | 100 | 102400 | 100 | 0 | 216.55 | 461.48 | 129.69 | 811 | 94.36 | 77.144 |
|  CBRProxy | 4G | 100 | 102400 | 500 | 0 | 156.92 | 636.5 | 94.62 | 947 | 96.19 | 48.096 |
|  CBRProxy | 4G | 100 | 102400 | 1000 | 0 | 93.17 | 1071.94 | 78.66 | 1351 | 97.26 | 67.657 |
|  CBRProxy | 4G | 200 | 500 | 0 | 0 | 12171.75 | 16.35 | 15.99 | 100 | 98.99 | 70.008 |
|  CBRProxy | 4G | 200 | 500 | 30 | 0 | 6152.01 | 32.47 | 4.66 | 60 | 99.47 | 69.275 |
|  CBRProxy | 4G | 200 | 500 | 100 | 0 | 1946.98 | 102.67 | 12.67 | 199 | 99.73 | 68.87 |
|  CBRProxy | 4G | 200 | 500 | 500 | 0 | 394.6 | 506.49 | 49.78 | 999 | 99.81 | 70.852 |
|  CBRProxy | 4G | 200 | 500 | 1000 | 0 | 197.24 | 1012.13 | 99.52 | 1999 | 99.82 | 64.843 |
|  CBRProxy | 4G | 200 | 1024 | 0 | 0 | 9896.58 | 20.12 | 17.01 | 105 | 99.03 | 70.266 |
|  CBRProxy | 4G | 200 | 1024 | 30 | 0 | 5830.62 | 34.24 | 4.94 | 60 | 99.42 | 57.87 |
|  CBRProxy | 4G | 200 | 1024 | 100 | 0 | 1939.31 | 103 | 13.84 | 199 | 99.71 | 71.963 |
|  CBRProxy | 4G | 200 | 1024 | 500 | 0 | 394.4 | 506.76 | 49.8 | 999 | 99.81 | 71.981 |
|  CBRProxy | 4G | 200 | 1024 | 1000 | 0 | 196.88 | 1013.59 | 106.47 | 1999 | 99.82 | 67.862 |
|  CBRProxy | 4G | 200 | 10240 | 0 | 0 | 2191.76 | 91.14 | 67.62 | 321 | 98.5 | 68.791 |
|  CBRProxy | 4G | 200 | 10240 | 30 | 0 | 2199.14 | 90.75 | 43.27 | 244 | 98.55 | 75.223 |
|  CBRProxy | 4G | 200 | 10240 | 100 | 0 | 1821.75 | 109.7 | 12.85 | 197 | 98.91 | 42.101 |
|  CBRProxy | 4G | 200 | 10240 | 500 | 0 | 393.59 | 508.03 | 49.65 | 999 | 99.61 | 69.133 |
|  CBRProxy | 4G | 200 | 10240 | 1000 | 0 | 197.95 | 1007.48 | 70.41 | 1019 | 99.72 | 73.841 |
|  CBRProxy | 4G | 200 | 102400 | 0 | 0 | 205.01 | 974.9 | 292.05 | 1791 | 86.17 | 313.976 |
|  CBRProxy | 4G | 200 | 102400 | 30 | 0 | 206.06 | 970.02 | 281.92 | 1719 | 86.98 | 289.154 |
|  CBRProxy | 4G | 200 | 102400 | 100 | 0 | 206.51 | 967.86 | 263.15 | 1671 | 87.3 | 272.941 |
|  CBRProxy | 4G | 200 | 102400 | 500 | 0 | 188.64 | 1059.21 | 238.49 | 1783 | 89.12 | 195.761 |
|  CBRProxy | 4G | 200 | 102400 | 1000 | 0 | 142.02 | 1405.16 | 254.97 | 2095 | 91.76 | 142.664 |
|  CBRProxy | 4G | 500 | 500 | 0 | 0 | 12273.55 | 40.58 | 21.14 | 111 | 98.51 | 69.63 |
|  CBRProxy | 4G | 500 | 500 | 30 | 0 | 10451.23 | 47.69 | 14.12 | 104 | 98.76 | 71.89 |
|  CBRProxy | 4G | 500 | 500 | 100 | 0 | 4858.75 | 102.84 | 9.88 | 143 | 99.38 | 69.04 |
|  CBRProxy | 4G | 500 | 500 | 500 | 0 | 989.03 | 505.02 | 41.55 | 515 | 99.74 | 75.257 |
|  CBRProxy | 4G | 500 | 500 | 1000 | 0 | 495.04 | 1008.09 | 77.07 | 1007 | 99.77 | 71.029 |
|  CBRProxy | 4G | 500 | 1024 | 0 | 0 | 9723.72 | 51.26 | 26.94 | 140 | 98.53 | 64.139 |
|  CBRProxy | 4G | 500 | 1024 | 30 | 0 | 8944.68 | 55.75 | 19.09 | 135 | 98.7 | 68.04 |
|  CBRProxy | 4G | 500 | 1024 | 100 | 0 | 4806.93 | 103.94 | 9.64 | 139 | 99.27 | 73.483 |
|  CBRProxy | 4G | 500 | 1024 | 500 | 0 | 989.84 | 504.69 | 38.6 | 519 | 99.72 | 78.285 |
|  CBRProxy | 4G | 500 | 1024 | 1000 | 0 | 494.81 | 1008.29 | 77.27 | 1019 | 99.81 | 43.606 |
|  CBRProxy | 4G | 500 | 10240 | 0 | 0 | 2043.51 | 244.51 | 129.08 | 631 | 96.44 | 71.196 |
|  CBRProxy | 4G | 500 | 10240 | 30 | 0 | 2065.78 | 242.1 | 112.68 | 583 | 96.64 | 64.889 |
|  CBRProxy | 4G | 500 | 10240 | 100 | 0 | 2037.17 | 245.46 | 85.31 | 515 | 96.89 | 67.704 |
|  CBRProxy | 4G | 500 | 10240 | 500 | 0 | 982.22 | 508.96 | 28.87 | 555 | 98.58 | 73.878 |
|  CBRProxy | 4G | 500 | 10240 | 1000 | 0 | 494.89 | 1007.26 | 63.12 | 1039 | 99.19 | 70.697 |
|  CBRProxy | 4G | 500 | 102400 | 0 | 0 | 136.46 | 3649.99 | 1222.06 | 6367 | 65.1 | 810.71 |
|  CBRProxy | 4G | 500 | 102400 | 30 | 0 | 135.01 | 3687.12 | 1256.6 | 6527 | 64.82 | 825.181 |
|  CBRProxy | 4G | 500 | 102400 | 100 | 0 | 137.84 | 3614.62 | 1193.04 | 6271 | 65.31 | 816.917 |
|  CBRProxy | 4G | 500 | 102400 | 500 | 0 | 141.11 | 3532.04 | 1096.84 | 6079 | 67.28 | 774.965 |
|  CBRProxy | 4G | 500 | 102400 | 1000 | 0 | 140.94 | 3533.52 | 995.43 | 5855 | 68.23 | 777.01 |
|  CBRProxy | 4G | 1000 | 500 | 0 | 0 | 12060.93 | 82.84 | 39.79 | 204 | 97.85 | 71.123 |
|  CBRProxy | 4G | 1000 | 500 | 30 | 0 | 11799.71 | 84.68 | 30.71 | 186 | 97.97 | 41.707 |
|  CBRProxy | 4G | 1000 | 500 | 100 | 0 | 8815.34 | 113.35 | 14.66 | 194 | 98.47 | 42.347 |
|  CBRProxy | 4G | 1000 | 500 | 500 | 0 | 1984.02 | 503.55 | 31.57 | 515 | 99.53 | 71.327 |
|  CBRProxy | 4G | 1000 | 500 | 1000 | 0 | 992.89 | 1005.49 | 57.69 | 1007 | 99.68 | 70.746 |
|  CBRProxy | 4G | 1000 | 1024 | 0 | 0 | 9597.04 | 104.12 | 47.82 | 247 | 97.85 | 60.365 |
|  CBRProxy | 4G | 1000 | 1024 | 30 | 0 | 9378.72 | 106.54 | 40.47 | 237 | 97.95 | 41.832 |
|  CBRProxy | 4G | 1000 | 1024 | 100 | 0 | 8152.27 | 122.57 | 19.59 | 202 | 98.18 | 72.245 |
|  CBRProxy | 4G | 1000 | 1024 | 500 | 0 | 1985.54 | 503.33 | 27.41 | 519 | 99.45 | 67.659 |
|  CBRProxy | 4G | 1000 | 1024 | 1000 | 0 | 992.08 | 1006.18 | 62.96 | 1011 | 99.61 | 69.44 |
|  CBRProxy | 4G | 1000 | 10240 | 0 | 0 | 1889.77 | 529.19 | 221.7 | 1127 | 93.26 | 139.201 |
|  CBRProxy | 4G | 1000 | 10240 | 30 | 0 | 1894.4 | 527.91 | 214.44 | 1111 | 93.52 | 125.338 |
|  CBRProxy | 4G | 1000 | 10240 | 100 | 0 | 1957.03 | 511 | 192.8 | 1055 | 93.41 | 134.776 |
|  CBRProxy | 4G | 1000 | 10240 | 500 | 0 | 1727.23 | 578.65 | 67.51 | 819 | 95.08 | 72.59 |
|  CBRProxy | 4G | 1000 | 10240 | 1000 | 0 | 988.11 | 1008.85 | 55.34 | 1079 | 97.3 | 70.62 |
|  CBRProxy | 4G | 1000 | 102400 | 0 | 0 | 87.54 | 11289.62 | 3023.98 | 16383 | 46.52 | 1518.93 |
|  CBRProxy | 4G | 1000 | 102400 | 30 | 0 | 88.68 | 11144.79 | 2956.14 | 16191 | 47.23 | 1489.154 |
|  CBRProxy | 4G | 1000 | 102400 | 100 | 0 | 87.64 | 11328.11 | 3077.19 | 16383 | 46.1 | 1517.346 |
|  CBRProxy | 4G | 1000 | 102400 | 500 | 0 | 86.6 | 11472.06 | 2888.47 | 16767 | 43.75 | 1521.143 |
|  CBRProxy | 4G | 1000 | 102400 | 1000 | 0 | 87.07 | 11394.52 | 2776.81 | 18175 | 44.51 | 1506.866 |
|  CBRSOAPHeaderProxy | 4G | 100 | 500 | 0 | 0 | 12007.96 | 8.27 | 15.01 | 97 | 99.21 | 72.141 |
|  CBRSOAPHeaderProxy | 4G | 100 | 500 | 30 | 0 | 3150.3 | 31.69 | 5.25 | 60 | 99.71 | 62.007 |
|  CBRSOAPHeaderProxy | 4G | 100 | 500 | 100 | 0 | 961.53 | 103.94 | 17.18 | 200 | 99.81 | 69.298 |
|  CBRSOAPHeaderProxy | 4G | 100 | 500 | 500 | 0 | 193.34 | 516.79 | 86.2 | 999 | 99.84 | 75.774 |
|  CBRSOAPHeaderProxy | 4G | 100 | 500 | 1000 | 0 | 98.57 | 1012.15 | 99.94 | 1999 | 99.85 | 69.917 |
|  CBRSOAPHeaderProxy | 4G | 100 | 1024 | 0 | 0 | 10424.4 | 9.53 | 15.5 | 100 | 99.28 | 65.361 |
|  CBRSOAPHeaderProxy | 4G | 100 | 1024 | 30 | 0 | 3153.04 | 31.68 | 5.09 | 60 | 99.71 | 43.172 |
|  CBRSOAPHeaderProxy | 4G | 100 | 1024 | 100 | 0 | 961.56 | 103.95 | 17.17 | 200 | 99.8 | 72.793 |
|  CBRSOAPHeaderProxy | 4G | 100 | 1024 | 500 | 0 | 194.01 | 514.77 | 80.53 | 999 | 99.82 | 70.94 |
|  CBRSOAPHeaderProxy | 4G | 100 | 1024 | 1000 | 0 | 99.26 | 1006.24 | 64.47 | 1003 | 99.83 | 73.002 |
|  CBRSOAPHeaderProxy | 4G | 100 | 10240 | 0 | 0 | 3306.84 | 30.16 | 33.27 | 183 | 99.35 | 80.393 |
|  CBRSOAPHeaderProxy | 4G | 100 | 10240 | 30 | 0 | 2648.39 | 37.7 | 6.05 | 61 | 99.47 | 65.139 |
|  CBRSOAPHeaderProxy | 4G | 100 | 10240 | 100 | 0 | 956.77 | 104.44 | 16.86 | 199 | 99.72 | 69.297 |
|  CBRSOAPHeaderProxy | 4G | 100 | 10240 | 500 | 0 | 197 | 507.35 | 49.07 | 543 | 99.8 | 71.908 |
|  CBRSOAPHeaderProxy | 4G | 100 | 10240 | 1000 | 0 | 98.56 | 1012.21 | 99.58 | 1999 | 99.81 | 63.679 |
|  CBRSOAPHeaderProxy | 4G | 100 | 102400 | 0 | 0 | 331.74 | 260.29 | 270.24 | 531 | 97.57 | 65.004 |
|  CBRSOAPHeaderProxy | 4G | 100 | 102400 | 30 | 0 | 375.51 | 266.29 | 93.28 | 515 | 97.69 | 72.822 |
|  CBRSOAPHeaderProxy | 4G | 100 | 102400 | 100 | 0 | 363.92 | 274.77 | 76.08 | 487 | 97.56 | 65.216 |
|  CBRSOAPHeaderProxy | 4G | 100 | 102400 | 500 | 0 | 188.46 | 530.28 | 62.57 | 991 | 98.65 | 72.064 |
|  CBRSOAPHeaderProxy | 4G | 100 | 102400 | 1000 | 0 | 98.04 | 1018.39 | 99.31 | 1983 | 99.31 | 62.229 |
|  CBRSOAPHeaderProxy | 4G | 200 | 500 | 0 | 0 | 13350.83 | 14.87 | 15.53 | 97 | 99 | 56.405 |
|  CBRSOAPHeaderProxy | 4G | 200 | 500 | 30 | 0 | 6275.58 | 31.83 | 4.62 | 60 | 99.49 | 42.421 |
|  CBRSOAPHeaderProxy | 4G | 200 | 500 | 100 | 0 | 1955.22 | 102.23 | 10.77 | 199 | 99.79 | 42.549 |
|  CBRSOAPHeaderProxy | 4G | 200 | 500 | 500 | 0 | 394.39 | 506.68 | 49.93 | 999 | 99.81 | 69.293 |
|  CBRSOAPHeaderProxy | 4G | 200 | 500 | 1000 | 0 | 196.21 | 1017.19 | 121.82 | 1999 | 99.86 | 41.616 |
|  CBRSOAPHeaderProxy | 4G | 200 | 1024 | 0 | 0 | 11351.09 | 17.52 | 17.98 | 110 | 99.06 | 61.041 |
|  CBRSOAPHeaderProxy | 4G | 200 | 1024 | 30 | 0 | 6030.36 | 33.12 | 4.9 | 60 | 99.47 | 70.149 |
|  CBRSOAPHeaderProxy | 4G | 200 | 1024 | 100 | 0 | 1949.81 | 102.42 | 11.8 | 199 | 99.73 | 75.236 |
|  CBRSOAPHeaderProxy | 4G | 200 | 1024 | 500 | 0 | 392.52 | 509.24 | 60.95 | 999 | 99.81 | 79.463 |
|  CBRSOAPHeaderProxy | 4G | 200 | 1024 | 1000 | 0 | 196.78 | 1014.06 | 108.6 | 1999 | 99.82 | 62.92 |
|  CBRSOAPHeaderProxy | 4G | 200 | 10240 | 0 | 0 | 3385.29 | 58.95 | 43.28 | 211 | 99.05 | 41.701 |
|  CBRSOAPHeaderProxy | 4G | 200 | 10240 | 30 | 0 | 3264.18 | 61.17 | 25.65 | 170 | 99.06 | 77.591 |
|  CBRSOAPHeaderProxy | 4G | 200 | 10240 | 100 | 0 | 1919.48 | 104.11 | 12.14 | 198 | 99.44 | 49.417 |
|  CBRSOAPHeaderProxy | 4G | 200 | 10240 | 500 | 0 | 393.86 | 507.56 | 49.69 | 999 | 99.74 | 73.688 |
|  CBRSOAPHeaderProxy | 4G | 200 | 10240 | 1000 | 0 | 198.03 | 1007.19 | 70.44 | 1007 | 99.79 | 74.721 |
|  CBRSOAPHeaderProxy | 4G | 200 | 102400 | 0 | 0 | 371.57 | 538.36 | 172.85 | 951 | 94.23 | 56.952 |
|  CBRSOAPHeaderProxy | 4G | 200 | 102400 | 30 | 0 | 374.11 | 534.61 | 160.45 | 923 | 94.39 | 70.626 |
|  CBRSOAPHeaderProxy | 4G | 200 | 102400 | 100 | 0 | 368.28 | 542.87 | 151.56 | 927 | 94.74 | 43.75 |
|  CBRSOAPHeaderProxy | 4G | 200 | 102400 | 500 | 0 | 314.2 | 635.87 | 84.68 | 971 | 95.41 | 77.101 |
|  CBRSOAPHeaderProxy | 4G | 200 | 102400 | 1000 | 0 | 186.71 | 1069.04 | 105.95 | 1391 | 96.7 | 66.358 |
|  CBRSOAPHeaderProxy | 4G | 500 | 500 | 0 | 0 | 12815.87 | 38.88 | 21.94 | 114 | 98.53 | 78.342 |
|  CBRSOAPHeaderProxy | 4G | 500 | 500 | 30 | 0 | 10837.74 | 46.02 | 13.42 | 99 | 98.81 | 67.148 |
|  CBRSOAPHeaderProxy | 4G | 500 | 500 | 100 | 0 | 4867.87 | 102.65 | 9.79 | 142 | 99.42 | 70.531 |
|  CBRSOAPHeaderProxy | 4G | 500 | 500 | 500 | 0 | 989.02 | 504.71 | 38.58 | 519 | 99.74 | 71.361 |
|  CBRSOAPHeaderProxy | 4G | 500 | 500 | 1000 | 0 | 495.91 | 1006.09 | 62.99 | 1007 | 99.79 | 51.426 |
|  CBRSOAPHeaderProxy | 4G | 500 | 1024 | 0 | 0 | 11264.24 | 44.22 | 23.74 | 124 | 98.65 | 41.381 |
|  CBRSOAPHeaderProxy | 4G | 500 | 1024 | 30 | 0 | 9904.4 | 50.34 | 15.4 | 114 | 98.8 | 66 |
|  CBRSOAPHeaderProxy | 4G | 500 | 1024 | 100 | 0 | 4859.2 | 102.82 | 8.37 | 127 | 99.38 | 51.534 |
|  CBRSOAPHeaderProxy | 4G | 500 | 1024 | 500 | 0 | 987.99 | 505.63 | 44.51 | 519 | 99.74 | 46.424 |
|  CBRSOAPHeaderProxy | 4G | 500 | 1024 | 1000 | 0 | 496.08 | 1006.13 | 62.88 | 1007 | 99.78 | 65.965 |
|  CBRSOAPHeaderProxy | 4G | 500 | 10240 | 0 | 0 | 3134.56 | 159.48 | 83.07 | 403 | 98.07 | 65.966 |
|  CBRSOAPHeaderProxy | 4G | 500 | 10240 | 30 | 0 | 3142.46 | 159.04 | 68.88 | 371 | 98.18 | 72.301 |
|  CBRSOAPHeaderProxy | 4G | 500 | 10240 | 100 | 0 | 3065.77 | 162.98 | 40.08 | 295 | 98.28 | 74.649 |
|  CBRSOAPHeaderProxy | 4G | 500 | 10240 | 500 | 0 | 988.04 | 505.77 | 38.4 | 527 | 99.36 | 72.354 |
|  CBRSOAPHeaderProxy | 4G | 500 | 10240 | 1000 | 0 | 494.62 | 1008.34 | 77.11 | 1023 | 99.57 | 70.941 |
|  CBRSOAPHeaderProxy | 4G | 500 | 102400 | 0 | 0 | 249.5 | 2000.79 | 763.66 | 3967 | 70.94 | 726.961 |
|  CBRSOAPHeaderProxy | 4G | 500 | 102400 | 30 | 0 | 251.92 | 1980.21 | 736.86 | 3903 | 71.17 | 737.606 |
|  CBRSOAPHeaderProxy | 4G | 500 | 102400 | 100 | 0 | 247.73 | 2014.46 | 724.13 | 3887 | 71.52 | 719.111 |
|  CBRSOAPHeaderProxy | 4G | 500 | 102400 | 500 | 0 | 262.94 | 1898.14 | 650.52 | 3855 | 75.49 | 685.867 |
|  CBRSOAPHeaderProxy | 4G | 500 | 102400 | 1000 | 0 | 266.86 | 1868.93 | 506.44 | 3487 | 77.04 | 696.224 |
|  CBRSOAPHeaderProxy | 4G | 1000 | 500 | 0 | 0 | 13199.4 | 75.68 | 38.61 | 194 | 97.84 | 75.439 |
|  CBRSOAPHeaderProxy | 4G | 1000 | 500 | 30 | 0 | 12773.89 | 78.19 | 29.23 | 176 | 97.96 | 42.028 |
|  CBRSOAPHeaderProxy | 4G | 1000 | 500 | 100 | 0 | 9050.41 | 110.39 | 11.47 | 158 | 98.56 | 72.786 |
|  CBRSOAPHeaderProxy | 4G | 1000 | 500 | 500 | 0 | 1984.2 | 503.49 | 31.56 | 515 | 99.57 | 75.307 |
|  CBRSOAPHeaderProxy | 4G | 1000 | 500 | 1000 | 0 | 993.14 | 1005.16 | 54.6 | 1007 | 99.69 | 67.73 |
|  CBRSOAPHeaderProxy | 4G | 1000 | 1024 | 0 | 0 | 11492.34 | 86.94 | 41.57 | 212 | 97.96 | 44.986 |
|  CBRSOAPHeaderProxy | 4G | 1000 | 1024 | 30 | 0 | 11033.41 | 90.55 | 33.78 | 201 | 97.98 | 68.191 |
|  CBRSOAPHeaderProxy | 4G | 1000 | 1024 | 100 | 0 | 8719.41 | 114.59 | 14.01 | 176 | 98.46 | 71.251 |
|  CBRSOAPHeaderProxy | 4G | 1000 | 1024 | 500 | 0 | 1984.56 | 503.4 | 29.31 | 515 | 99.53 | 70.521 |
|  CBRSOAPHeaderProxy | 4G | 1000 | 1024 | 1000 | 0 | 992.53 | 1005.55 | 57.82 | 1011 | 99.73 | 42.013 |
|  CBRSOAPHeaderProxy | 4G | 1000 | 10240 | 0 | 0 | 3031.38 | 329.95 | 143.77 | 731 | 96.03 | 70.032 |
|  CBRSOAPHeaderProxy | 4G | 1000 | 10240 | 30 | 0 | 2917.38 | 342.91 | 140.64 | 731 | 96.31 | 71.092 |
|  CBRSOAPHeaderProxy | 4G | 1000 | 10240 | 100 | 0 | 2902.75 | 344.61 | 121.55 | 699 | 96.5 | 72.243 |
|  CBRSOAPHeaderProxy | 4G | 1000 | 10240 | 500 | 0 | 1963.52 | 508.97 | 27.47 | 567 | 98 | 41.875 |
|  CBRSOAPHeaderProxy | 4G | 1000 | 10240 | 1000 | 0 | 992.04 | 1005.31 | 47.89 | 1039 | 98.83 | 74.621 |
|  CBRSOAPHeaderProxy | 4G | 1000 | 102400 | 0 | 0 | 176.22 | 5647.31 | 1726.02 | 10175 | 54.13 | 1294.421 |
|  CBRSOAPHeaderProxy | 4G | 1000 | 102400 | 30 | 0 | 177.77 | 5611.45 | 1683.61 | 10047 | 52.86 | 1305.995 |
|  CBRSOAPHeaderProxy | 4G | 1000 | 102400 | 100 | 0 | 174.84 | 5707.6 | 1657.62 | 10111 | 53.62 | 1305.653 |
|  CBRSOAPHeaderProxy | 4G | 1000 | 102400 | 500 | 0 | 172.44 | 5763.72 | 1543.15 | 9983 | 51.78 | 1313.188 |
|  CBRSOAPHeaderProxy | 4G | 1000 | 102400 | 1000 | 0 | 170.94 | 5824.79 | 1530.28 | 10047 | 53.59 | 1293.391 |
|  CBRTransportHeaderProxy | 4G | 100 | 500 | 0 | 0 | 16972.15 | 5.83 | 14.02 | 90 | 99.33 | 67.075 |
|  CBRTransportHeaderProxy | 4G | 100 | 500 | 30 | 0 | 3092.63 | 32.27 | 6.92 | 60 | 99.78 | 68.009 |
|  CBRTransportHeaderProxy | 4G | 100 | 500 | 100 | 0 | 963.37 | 103.74 | 17.15 | 200 | 99.82 | 72.394 |
|  CBRTransportHeaderProxy | 4G | 100 | 500 | 500 | 0 | 191.41 | 521.84 | 99.37 | 999 | 99.85 | 64.576 |
|  CBRTransportHeaderProxy | 4G | 100 | 500 | 1000 | 0 | 99.73 | 1002.03 | 0.94 | 1003 | 99.85 | 77.576 |
|  CBRTransportHeaderProxy | 4G | 100 | 1024 | 0 | 0 | 15992.72 | 6.19 | 14.58 | 95 | 99.37 | 69.262 |
|  CBRTransportHeaderProxy | 4G | 100 | 1024 | 30 | 0 | 3178.47 | 31.42 | 4.86 | 60 | 99.78 | 71.895 |
|  CBRTransportHeaderProxy | 4G | 100 | 1024 | 100 | 0 | 962.27 | 103.84 | 17.24 | 200 | 99.81 | 69.353 |
|  CBRTransportHeaderProxy | 4G | 100 | 1024 | 500 | 0 | 195.83 | 510.12 | 65.96 | 999 | 99.84 | 70.616 |
|  CBRTransportHeaderProxy | 4G | 100 | 1024 | 1000 | 0 | 98.59 | 1012.13 | 99.96 | 1999 | 99.87 | 76.523 |
|  CBRTransportHeaderProxy | 4G | 100 | 10240 | 0 | 0 | 12669.24 | 7.81 | 15.3 | 98 | 99.49 | 77.469 |
|  CBRTransportHeaderProxy | 4G | 100 | 10240 | 30 | 0 | 3183.42 | 31.37 | 4.26 | 60 | 99.77 | 76.651 |
|  CBRTransportHeaderProxy | 4G | 100 | 10240 | 100 | 0 | 963.45 | 103.65 | 16.56 | 200 | 99.82 | 41.845 |
|  CBRTransportHeaderProxy | 4G | 100 | 10240 | 500 | 0 | 197.28 | 506.45 | 49.95 | 999 | 99.85 | 67.853 |
|  CBRTransportHeaderProxy | 4G | 100 | 10240 | 1000 | 0 | 98.63 | 1012.12 | 99.94 | 1999 | 99.88 | 60.978 |
|  CBRTransportHeaderProxy | 4G | 100 | 102400 | 0 | 0 | 4236.58 | 23.25 | 7.71 | 48 | 99.74 | 76.049 |
|  CBRTransportHeaderProxy | 4G | 100 | 102400 | 30 | 0 | 780.15 | 128.06 | 65.6 | 459 | 99.8 | 62.831 |
|  CBRTransportHeaderProxy | 4G | 100 | 102400 | 100 | 0 | 769.94 | 129.71 | 22.8 | 195 | 99.82 | 71.862 |
|  CBRTransportHeaderProxy | 4G | 100 | 102400 | 500 | 0 | 197.97 | 504.83 | 36.24 | 507 | 99.85 | 42.142 |
|  CBRTransportHeaderProxy | 4G | 100 | 102400 | 1000 | 0 | 98.53 | 1012.17 | 99.68 | 1999 | 99.85 | 45.458 |
|  CBRTransportHeaderProxy | 4G | 200 | 500 | 0 | 0 | 18916.12 | 10.49 | 16.36 | 102 | 99.17 | 67.876 |
|  CBRTransportHeaderProxy | 4G | 200 | 500 | 30 | 0 | 6304.87 | 31.67 | 5.12 | 60 | 99.66 | 66.606 |
|  CBRTransportHeaderProxy | 4G | 200 | 500 | 100 | 0 | 1934.86 | 103.3 | 15.39 | 200 | 99.79 | 42.049 |
|  CBRTransportHeaderProxy | 4G | 200 | 500 | 500 | 0 | 394.3 | 506.78 | 51.46 | 999 | 99.83 | 61.06 |
|  CBRTransportHeaderProxy | 4G | 200 | 500 | 1000 | 0 | 198.42 | 1007.77 | 74.76 | 1007 | 99.85 | 41.642 |
|  CBRTransportHeaderProxy | 4G | 200 | 1024 | 0 | 0 | 17946.9 | 11.04 | 17.07 | 105 | 99.23 | 69.567 |
|  CBRTransportHeaderProxy | 4G | 200 | 1024 | 30 | 0 | 6365.53 | 31.37 | 4.09 | 60 | 99.67 | 77.085 |
|  CBRTransportHeaderProxy | 4G | 200 | 1024 | 100 | 0 | 1932.49 | 103.42 | 15.73 | 200 | 99.8 | 67.835 |
|  CBRTransportHeaderProxy | 4G | 200 | 1024 | 500 | 0 | 392.66 | 508.89 | 61.02 | 999 | 99.82 | 69.917 |
|  CBRTransportHeaderProxy | 4G | 200 | 1024 | 1000 | 0 | 198.2 | 1007.07 | 70.72 | 1003 | 99.84 | 74.305 |
|  CBRTransportHeaderProxy | 4G | 200 | 10240 | 0 | 0 | 13659.51 | 14.51 | 45.07 | 101 | 99.39 | 61.162 |
|  CBRTransportHeaderProxy | 4G | 200 | 10240 | 30 | 0 | 6278.9 | 31.79 | 4.56 | 60 | 99.67 | 42.163 |
|  CBRTransportHeaderProxy | 4G | 200 | 10240 | 100 | 0 | 1954.01 | 102.28 | 11 | 199 | 99.79 | 71.285 |
|  CBRTransportHeaderProxy | 4G | 200 | 10240 | 500 | 0 | 392.42 | 509.15 | 60.99 | 999 | 99.82 | 71.63 |
|  CBRTransportHeaderProxy | 4G | 200 | 10240 | 1000 | 0 | 198.15 | 1007.48 | 73.27 | 1007 | 99.84 | 74.143 |
|  CBRTransportHeaderProxy | 4G | 200 | 102400 | 0 | 0 | 3939.93 | 50.24 | 20.85 | 113 | 99.73 | 72.67 |
|  CBRTransportHeaderProxy | 4G | 200 | 102400 | 30 | 0 | 757.18 | 264.06 | 136.95 | 623 | 99.84 | 41.849 |
|  CBRTransportHeaderProxy | 4G | 200 | 102400 | 100 | 0 | 756.58 | 264.22 | 86.29 | 579 | 99.81 | 42.045 |
|  CBRTransportHeaderProxy | 4G | 200 | 102400 | 500 | 0 | 395.83 | 505.02 | 35.2 | 511 | 99.81 | 70.168 |
|  CBRTransportHeaderProxy | 4G | 200 | 102400 | 1000 | 0 | 198.04 | 1007.18 | 70.46 | 1011 | 99.83 | 70.948 |
|  CBRTransportHeaderProxy | 4G | 500 | 500 | 0 | 0 | 19219.75 | 25.87 | 21.47 | 111 | 99 | 41.168 |
|  CBRTransportHeaderProxy | 4G | 500 | 500 | 30 | 0 | 13576.78 | 36.73 | 7.16 | 67 | 99.26 | 73.9 |
|  CBRTransportHeaderProxy | 4G | 500 | 500 | 100 | 0 | 4895.93 | 102.06 | 8.58 | 135 | 99.67 | 69.494 |
|  CBRTransportHeaderProxy | 4G | 500 | 500 | 500 | 0 | 990.37 | 504.55 | 38.9 | 515 | 99.8 | 66.815 |
|  CBRTransportHeaderProxy | 4G | 500 | 500 | 1000 | 0 | 496.82 | 1004.19 | 45.92 | 1003 | 99.81 | 61.931 |
|  CBRTransportHeaderProxy | 4G | 500 | 1024 | 0 | 0 | 18335.24 | 27.09 | 21.04 | 112 | 99 | 71.389 |
|  CBRTransportHeaderProxy | 4G | 500 | 1024 | 30 | 0 | 13051.94 | 38.16 | 8.09 | 71 | 99.28 | 68.313 |
|  CBRTransportHeaderProxy | 4G | 500 | 1024 | 100 | 0 | 4896.88 | 102.04 | 9.16 | 133 | 99.65 | 74.99 |
|  CBRTransportHeaderProxy | 4G | 500 | 1024 | 500 | 0 | 990.3 | 504.49 | 38.63 | 507 | 99.8 | 41.475 |
|  CBRTransportHeaderProxy | 4G | 500 | 1024 | 1000 | 0 | 494.63 | 1009.23 | 83.72 | 1015 | 99.81 | 70.641 |
|  CBRTransportHeaderProxy | 4G | 500 | 10240 | 0 | 0 | 13203.49 | 37.75 | 23.31 | 120 | 99.26 | 71.849 |
|  CBRTransportHeaderProxy | 4G | 500 | 10240 | 30 | 0 | 11232.14 | 44.41 | 11.64 | 89 | 99.35 | 42.38 |
|  CBRTransportHeaderProxy | 4G | 500 | 10240 | 100 | 0 | 4888.9 | 102.13 | 9.07 | 127 | 99.65 | 69.034 |
|  CBRTransportHeaderProxy | 4G | 500 | 10240 | 500 | 0 | 992.67 | 503.33 | 30.33 | 507 | 99.79 | 72.657 |
|  CBRTransportHeaderProxy | 4G | 500 | 10240 | 1000 | 0 | 495.74 | 1006.2 | 62.89 | 1015 | 99.82 | 70.78 |
|  CBRTransportHeaderProxy | 4G | 500 | 102400 | 0 | 0 | 3453.79 | 143.82 | 32.02 | 230 | 99.69 | 67.665 |
|  CBRTransportHeaderProxy | 4G | 500 | 102400 | 30 | 0.03 | 836.06 | 525.68 | 2552.44 | 4127 | 99.76 | 41.829 |
|  CBRTransportHeaderProxy | 4G | 500 | 102400 | 100 | 0.03 | 654.32 | 656.56 | 2543.25 | 4127 | 99.78 | 72.699 |
|  CBRTransportHeaderProxy | 4G | 500 | 102400 | 500 | 0 | 883.74 | 565.45 | 147.23 | 1263 | 99.78 | 76.4 |
|  CBRTransportHeaderProxy | 4G | 500 | 102400 | 1000 | 0 | 496.43 | 1004.33 | 44.6 | 1011 | 99.8 | 68.535 |
|  CBRTransportHeaderProxy | 4G | 1000 | 500 | 0 | 0 | 19902.62 | 50.18 | 31.76 | 160 | 98.52 | 41.71 |
|  CBRTransportHeaderProxy | 4G | 1000 | 500 | 30 | 0 | 17971.08 | 55.57 | 19.4 | 127 | 98.69 | 68.616 |
|  CBRTransportHeaderProxy | 4G | 1000 | 500 | 100 | 0 | 9694.73 | 103.08 | 8.02 | 128 | 99.35 | 42.19 |
|  CBRTransportHeaderProxy | 4G | 1000 | 500 | 500 | 0 | 1983 | 503.95 | 35.36 | 515 | 99.74 | 41.594 |
|  CBRTransportHeaderProxy | 4G | 1000 | 500 | 1000 | 0 | 994.39 | 1004.46 | 48.39 | 1007 | 99.78 | 70.024 |
|  CBRTransportHeaderProxy | 4G | 1000 | 1024 | 0 | 0 | 18309.16 | 54.54 | 35.17 | 169 | 98.61 | 67.04 |
|  CBRTransportHeaderProxy | 4G | 1000 | 1024 | 30 | 0 | 17184.46 | 58.08 | 20.97 | 135 | 98.75 | 78.379 |
|  CBRTransportHeaderProxy | 4G | 1000 | 1024 | 100 | 0 | 9650.47 | 103.54 | 9.17 | 137 | 99.31 | 66.778 |
|  CBRTransportHeaderProxy | 4G | 1000 | 1024 | 500 | 0 | 1985.16 | 503.23 | 30.59 | 507 | 99.77 | 41.832 |
|  CBRTransportHeaderProxy | 4G | 1000 | 1024 | 1000 | 0 | 993.7 | 1004.41 | 47.35 | 1007 | 99.77 | 71.584 |
|  CBRTransportHeaderProxy | 4G | 1000 | 10240 | 0 | 0 | 13387.66 | 74.58 | 33.69 | 177 | 98.96 | 75.561 |
|  CBRTransportHeaderProxy | 4G | 1000 | 10240 | 30 | 0 | 13422.91 | 74.4 | 25.16 | 158 | 98.99 | 76.857 |
|  CBRTransportHeaderProxy | 4G | 1000 | 10240 | 100 | 0 | 9323.03 | 107.17 | 10.36 | 150 | 99.3 | 68.779 |
|  CBRTransportHeaderProxy | 4G | 1000 | 10240 | 500 | 0 | 1986.94 | 502.96 | 28.02 | 507 | 99.73 | 74.511 |
|  CBRTransportHeaderProxy | 4G | 1000 | 10240 | 1000 | 0 | 991.78 | 1006.07 | 62.69 | 1007 | 99.77 | 42.139 |
|  CBRTransportHeaderProxy | 4G | 1000 | 102400 | 0 | 0 | 3496.13 | 286.01 | 68.7 | 469 | 99.62 | 69.348 |
|  CBRTransportHeaderProxy | 4G | 1000 | 102400 | 30 | 0.11 | 1095.44 | 801.96 | 5076.76 | 7391 | 99.69 | 71.1 |
|  CBRTransportHeaderProxy | 4G | 1000 | 102400 | 100 | 0.13 | 657.83 | 1299.94 | 5892.64 | 14207 | 99.73 | 71.711 |
|  CBRTransportHeaderProxy | 4G | 1000 | 102400 | 500 | 0.04 | 669.81 | 1316.59 | 3407.24 | 7807 | 99.8 | 41.648 |
|  CBRTransportHeaderProxy | 4G | 1000 | 102400 | 1000 | 0 | 888.78 | 1114.46 | 434.49 | 2287 | 99.76 | 74.999 |
|  DirectProxy | 4G | 100 | 500 | 0 | 0 | 17588.2 | 5.63 | 13.41 | 85 | 99.32 | 76.095 |
|  DirectProxy | 4G | 100 | 500 | 30 | 0 | 3143.44 | 31.77 | 5.78 | 60 | 99.78 | 74.662 |
|  DirectProxy | 4G | 100 | 500 | 100 | 0 | 966.43 | 103.4 | 16 | 200 | 99.82 | 73.487 |
|  DirectProxy | 4G | 100 | 500 | 500 | 0 | 193.56 | 516.06 | 84.66 | 999 | 99.83 | 74.986 |
|  DirectProxy | 4G | 100 | 500 | 1000 | 0 | 97.6 | 1022.36 | 140.84 | 1999 | 99.86 | 43.441 |
|  DirectProxy | 4G | 100 | 1024 | 0 | 0 | 16667.76 | 5.93 | 13.28 | 85 | 99.35 | 71.504 |
|  DirectProxy | 4G | 100 | 1024 | 30 | 0 | 3161.28 | 31.57 | 5.4 | 60 | 99.77 | 67.035 |
|  DirectProxy | 4G | 100 | 1024 | 100 | 0 | 960.09 | 104.08 | 18.02 | 200 | 99.82 | 71.693 |
|  DirectProxy | 4G | 100 | 1024 | 500 | 0 | 196.01 | 509.59 | 64.01 | 999 | 99.84 | 72.434 |
|  DirectProxy | 4G | 100 | 1024 | 1000 | 0 | 97.43 | 1024.28 | 147.26 | 2007 | 99.87 | 70.425 |
|  DirectProxy | 4G | 100 | 10240 | 0 | 0 | 13173.19 | 7.5 | 45 | 92 | 99.47 | 75.828 |
|  DirectProxy | 4G | 100 | 10240 | 30 | 0 | 3184.3 | 31.36 | 4.27 | 60 | 99.77 | 70.283 |
|  DirectProxy | 4G | 100 | 10240 | 100 | 0 | 957.63 | 104.28 | 18.34 | 200 | 99.86 | 42.649 |
|  DirectProxy | 4G | 100 | 10240 | 500 | 0 | 195.89 | 510.08 | 65.56 | 999 | 99.85 | 66.134 |
|  DirectProxy | 4G | 100 | 10240 | 1000 | 0 | 99.28 | 1006.38 | 65.66 | 1003 | 99.84 | 41.166 |
|  DirectProxy | 4G | 100 | 102400 | 0 | 0 | 4269.14 | 23.07 | 7.53 | 47 | 99.74 | 71.818 |
|  DirectProxy | 4G | 100 | 102400 | 30 | 0 | 755.13 | 132.24 | 93.99 | 461 | 99.81 | 70.431 |
|  DirectProxy | 4G | 100 | 102400 | 100 | 0 | 769.56 | 129.76 | 35.71 | 343 | 99.82 | 70.119 |
|  DirectProxy | 4G | 100 | 102400 | 500 | 0 | 197.1 | 507.24 | 49.76 | 999 | 99.84 | 68.37 |
|  DirectProxy | 4G | 100 | 102400 | 1000 | 0 | 99.66 | 1002.08 | 0.88 | 1007 | 99.87 | 42.787 |
|  DirectProxy | 4G | 200 | 500 | 0 | 0 | 19509.07 | 10.17 | 14.82 | 95 | 99.18 | 75.698 |
|  DirectProxy | 4G | 200 | 500 | 30 | 0 | 6300.93 | 31.7 | 5.17 | 60 | 99.68 | 63.883 |
|  DirectProxy | 4G | 200 | 500 | 100 | 0 | 1947.8 | 102.58 | 12.29 | 199 | 99.79 | 67.778 |
|  DirectProxy | 4G | 200 | 500 | 500 | 0 | 391.82 | 509.75 | 63.88 | 999 | 99.81 | 66.784 |
|  DirectProxy | 4G | 200 | 500 | 1000 | 0 | 198.19 | 1007.06 | 70.75 | 1003 | 99.84 | 70.974 |
|  DirectProxy | 4G | 200 | 1024 | 0 | 0 | 18175.66 | 10.87 | 16.19 | 100 | 99.24 | 65.698 |
|  DirectProxy | 4G | 200 | 1024 | 30 | 0 | 6352.07 | 31.44 | 4.41 | 60 | 99.67 | 76.556 |
|  DirectProxy | 4G | 200 | 1024 | 100 | 0 | 1938.9 | 102.98 | 14.07 | 200 | 99.79 | 69.847 |
|  DirectProxy | 4G | 200 | 1024 | 500 | 0 | 390.66 | 511.41 | 70.31 | 999 | 99.83 | 65.672 |
|  DirectProxy | 4G | 200 | 1024 | 1000 | 0 | 199.03 | 1003.79 | 41.88 | 1003 | 99.85 | 46.919 |
|  DirectProxy | 4G | 200 | 10240 | 0 | 0 | 13937.52 | 14.22 | 16.61 | 100 | 99.45 | 41.469 |
|  DirectProxy | 4G | 200 | 10240 | 30 | 0 | 6308.75 | 31.65 | 4.21 | 60 | 99.66 | 74.902 |
|  DirectProxy | 4G | 200 | 10240 | 100 | 0 | 1953.57 | 102.3 | 11.31 | 199 | 99.79 | 71.275 |
|  DirectProxy | 4G | 200 | 10240 | 500 | 0 | 390.56 | 511.57 | 70.39 | 999 | 99.82 | 67.383 |
|  DirectProxy | 4G | 200 | 10240 | 1000 | 0 | 197.2 | 1012.09 | 99.54 | 1999 | 99.87 | 42.009 |
|  DirectProxy | 4G | 200 | 102400 | 0 | 0 | 4120.19 | 48.04 | 14.89 | 97 | 99.73 | 68.656 |
|  DirectProxy | 4G | 200 | 102400 | 30 | 0 | 757.23 | 264.04 | 140.9 | 627 | 99.8 | 67.652 |
|  DirectProxy | 4G | 200 | 102400 | 100 | 0 | 756.67 | 264.19 | 86.17 | 579 | 99.81 | 68.634 |
|  DirectProxy | 4G | 200 | 102400 | 500 | 0 | 395.92 | 504.96 | 35.21 | 509 | 99.83 | 68.852 |
|  DirectProxy | 4G | 200 | 102400 | 1000 | 0 | 198.03 | 1007.19 | 70.48 | 1011 | 99.86 | 42.201 |
|  DirectProxy | 4G | 500 | 500 | 0 | 0 | 19940.62 | 24.92 | 20.38 | 107 | 98.95 | 80.643 |
|  DirectProxy | 4G | 500 | 500 | 30 | 0 | 13705.48 | 36.4 | 7.11 | 68 | 99.26 | 75.747 |
|  DirectProxy | 4G | 500 | 500 | 100 | 0 | 4895.74 | 102.07 | 9.25 | 138 | 99.64 | 63.042 |
|  DirectProxy | 4G | 500 | 500 | 500 | 0 | 988.16 | 505.51 | 44.54 | 531 | 99.79 | 67.722 |
|  DirectProxy | 4G | 500 | 500 | 1000 | 0 | 495.02 | 1007.82 | 75.35 | 1007 | 99.8 | 71.507 |
|  DirectProxy | 4G | 500 | 1024 | 0 | 0 | 18235.69 | 27.23 | 21.57 | 112 | 99.02 | 70.332 |
|  DirectProxy | 4G | 500 | 1024 | 30 | 0 | 13309.43 | 37.46 | 7.61 | 70 | 99.3 | 72.75 |
|  DirectProxy | 4G | 500 | 1024 | 100 | 0 | 4887.79 | 102.22 | 9.39 | 142 | 99.67 | 42.563 |
|  DirectProxy | 4G | 500 | 1024 | 500 | 0 | 991.6 | 503.76 | 34.41 | 507 | 99.79 | 71.35 |
|  DirectProxy | 4G | 500 | 1024 | 1000 | 0 | 496.25 | 1005.76 | 60.42 | 1003 | 99.81 | 66.165 |
|  DirectProxy | 4G | 500 | 10240 | 0 | 0 | 13434.7 | 37.1 | 22.74 | 117 | 99.25 | 69.378 |
|  DirectProxy | 4G | 500 | 10240 | 30 | 0 | 11435.12 | 43.65 | 11 | 86 | 99.35 | 71.911 |
|  DirectProxy | 4G | 500 | 10240 | 100 | 0 | 4855.25 | 102.91 | 12.01 | 199 | 99.66 | 41.673 |
|  DirectProxy | 4G | 500 | 10240 | 500 | 0 | 992.25 | 503.42 | 31.53 | 509 | 99.8 | 70.18 |
|  DirectProxy | 4G | 500 | 10240 | 1000 | 0 | 495.11 | 1008.11 | 77.06 | 1007 | 99.8 | 71.674 |
|  DirectProxy | 4G | 500 | 102400 | 0 | 0 | 3611.01 | 137.46 | 41.14 | 249 | 99.7 | 41.427 |
|  DirectProxy | 4G | 500 | 102400 | 30 | 0.02 | 1002.15 | 435.15 | 2362.42 | 3695 | 99.75 | 71.517 |
|  DirectProxy | 4G | 500 | 102400 | 100 | 0.02 | 655.18 | 660.53 | 2101.02 | 4415 | 99.78 | 70.668 |
|  DirectProxy | 4G | 500 | 102400 | 500 | 0 | 882.48 | 566.36 | 148.33 | 1271 | 99.79 | 68.866 |
|  DirectProxy | 4G | 500 | 102400 | 1000 | 0 | 496.35 | 1004.39 | 44.65 | 1015 | 99.81 | 41.805 |
|  DirectProxy | 4G | 1000 | 500 | 0 | 0 | 19764.01 | 50.5 | 32.94 | 164 | 98.55 | 76.657 |
|  DirectProxy | 4G | 1000 | 500 | 30 | 0 | 18388.71 | 54.31 | 18.25 | 123 | 98.7 | 75.062 |
|  DirectProxy | 4G | 1000 | 500 | 100 | 0 | 9686.05 | 103.15 | 9.3 | 139 | 99.32 | 68.074 |
|  DirectProxy | 4G | 1000 | 500 | 500 | 0 | 1983.14 | 503.82 | 34.83 | 507 | 99.73 | 41.83 |
|  DirectProxy | 4G | 1000 | 500 | 1000 | 0 | 993.56 | 1004.16 | 44.97 | 1007 | 99.78 | 73.024 |
|  DirectProxy | 4G | 1000 | 1024 | 0 | 0 | 18255.44 | 54.69 | 33.75 | 171 | 98.69 | 48.599 |
|  DirectProxy | 4G | 1000 | 1024 | 30 | 0 | 17134.97 | 58.25 | 21.12 | 138 | 98.79 | 63.589 |
|  DirectProxy | 4G | 1000 | 1024 | 100 | 0 | 9622.34 | 103.83 | 10.88 | 187 | 99.33 | 75.45 |
|  DirectProxy | 4G | 1000 | 1024 | 500 | 0 | 1984.81 | 503.39 | 31.62 | 507 | 99.72 | 68.866 |
|  DirectProxy | 4G | 1000 | 1024 | 1000 | 0 | 991.96 | 1006.12 | 63 | 1007 | 99.77 | 70.444 |
|  DirectProxy | 4G | 1000 | 10240 | 0 | 0 | 13203.39 | 75.63 | 34 | 179 | 98.99 | 67.601 |
|  DirectProxy | 4G | 1000 | 10240 | 30 | 0 | 12857.09 | 77.69 | 28.49 | 171 | 99.04 | 69.669 |
|  DirectProxy | 4G | 1000 | 10240 | 100 | 0 | 9391.78 | 106.38 | 9.63 | 144 | 99.32 | 67.953 |
|  DirectProxy | 4G | 1000 | 10240 | 500 | 0 | 1985.81 | 503.25 | 29.99 | 509 | 99.73 | 70.195 |
|  DirectProxy | 4G | 1000 | 10240 | 1000 | 0 | 993.13 | 1005.09 | 54.54 | 1007 | 99.78 | 71.126 |
|  DirectProxy | 4G | 1000 | 102400 | 0 | 0 | 3409.22 | 293.37 | 55.7 | 441 | 99.62 | 70.9 |
|  DirectProxy | 4G | 1000 | 102400 | 30 | 0.1 | 1274.84 | 691.46 | 4364.97 | 7007 | 99.68 | 73.703 |
|  DirectProxy | 4G | 1000 | 102400 | 100 | 0.15 | 656.83 | 1302.9 | 6452.14 | 14399 | 99.74 | 73.007 |
|  DirectProxy | 4G | 1000 | 102400 | 500 | 0.06 | 660.7 | 1313.16 | 3815.2 | 7903 | 99.75 | 67.968 |
|  DirectProxy | 4G | 1000 | 102400 | 1000 | 0 | 822.9 | 1101.34 | 429.8 | 2383 | 99.77 | 42.545 |
|  SecureProxy | 4G | 100 | 500 | 0 | 0 | 527.31 | 189.56 | 136.87 | 611 | 99.23 | 79.255 |
|  SecureProxy | 4G | 100 | 500 | 30 | 0 | 528.96 | 189.06 | 101.86 | 503 | 99.25 | 76.185 |
|  SecureProxy | 4G | 100 | 500 | 100 | 0 | 511.14 | 195.61 | 61.2 | 387 | 99.33 | 56.527 |
|  SecureProxy | 4G | 100 | 500 | 500 | 0 | 197.3 | 506.83 | 1.71 | 511 | 99.68 | 78.165 |
|  SecureProxy | 4G | 100 | 500 | 1000 | 0 | 99.21 | 1006.82 | 1.93 | 1015 | 99.76 | 79.628 |
|  SecureProxy | 4G | 100 | 1024 | 0 | 0 | 506.25 | 197.55 | 142.44 | 639 | 99.2 | 56.795 |
|  SecureProxy | 4G | 100 | 1024 | 30 | 0 | 506.22 | 197.56 | 107.52 | 527 | 99.18 | 80.183 |
|  SecureProxy | 4G | 100 | 1024 | 100 | 0 | 492.32 | 203.11 | 65.3 | 405 | 99.28 | 81.56 |
|  SecureProxy | 4G | 100 | 1024 | 500 | 0 | 197.15 | 507.28 | 1.97 | 515 | 99.67 | 80.212 |
|  SecureProxy | 4G | 100 | 1024 | 1000 | 0 | 99.16 | 1006.82 | 1.84 | 1011 | 99.75 | 78.39 |
|  SecureProxy | 4G | 100 | 10240 | 0 | 0 | 280.78 | 356.32 | 138.46 | 735 | 98.33 | 76.538 |
|  SecureProxy | 4G | 100 | 10240 | 30 | 0 | 277.31 | 360.76 | 129.77 | 715 | 98.03 | 82.118 |
|  SecureProxy | 4G | 100 | 10240 | 100 | 0 | 274.64 | 364.24 | 109.04 | 667 | 98.17 | 79.389 |
|  SecureProxy | 4G | 100 | 10240 | 500 | 0 | 186.87 | 535.06 | 28.99 | 639 | 98.85 | 58.29 |
|  SecureProxy | 4G | 100 | 10240 | 1000 | 0 | 98.65 | 1012.55 | 5.02 | 1039 | 99.35 | 84.671 |
|  SecureProxy | 4G | 100 | 102400 | 0 | 0 | 34.16 | 2917.17 | 683.16 | 4767 | 75.31 | 529.665 |
|  SecureProxy | 4G | 100 | 102400 | 30 | 0 | 34.01 | 2933.18 | 690.24 | 4767 | 74.93 | 548.385 |
|  SecureProxy | 4G | 100 | 102400 | 100 | 0 | 34.14 | 2919.5 | 685.95 | 4767 | 74.71 | 541.218 |
|  SecureProxy | 4G | 100 | 102400 | 500 | 0 | 33.42 | 2983.49 | 707.94 | 4799 | 74.62 | 552.562 |
|  SecureProxy | 4G | 100 | 102400 | 1000 | 0 | 32.26 | 3090.9 | 820.67 | 5119 | 71.86 | 645.36 |
|  SecureProxy | 4G | 200 | 500 | 0 | 0 | 526.59 | 379.69 | 269.85 | 1207 | 98.86 | 78.314 |
|  SecureProxy | 4G | 200 | 500 | 30 | 0 | 524.17 | 381.64 | 235.82 | 1111 | 98.92 | 78.962 |
|  SecureProxy | 4G | 200 | 500 | 100 | 0 | 522.47 | 382.62 | 180.14 | 935 | 98.93 | 80.926 |
|  SecureProxy | 4G | 200 | 500 | 500 | 0 | 389.96 | 512.94 | 10.62 | 559 | 99.39 | 78.34 |
|  SecureProxy | 4G | 200 | 500 | 1000 | 0 | 198.29 | 1007.33 | 2.64 | 1019 | 99.61 | 73.382 |
|  SecureProxy | 4G | 200 | 1024 | 0 | 0 | 504.59 | 396.34 | 288.47 | 1271 | 98.84 | 56.743 |
|  SecureProxy | 4G | 200 | 1024 | 30 | 0 | 502.46 | 398.06 | 251.48 | 1159 | 98.74 | 77.42 |
|  SecureProxy | 4G | 200 | 1024 | 100 | 0 | 504.46 | 396.23 | 198.57 | 995 | 98.82 | 75.042 |
|  SecureProxy | 4G | 200 | 1024 | 500 | 0 | 385.71 | 518.62 | 20.17 | 607 | 99.28 | 75.154 |
|  SecureProxy | 4G | 200 | 1024 | 1000 | 0 | 198.17 | 1007.85 | 3.44 | 1023 | 99.57 | 78.162 |
|  SecureProxy | 4G | 200 | 10240 | 0 | 0 | 279.55 | 715.2 | 216.19 | 1311 | 97.49 | 73.294 |
|  SecureProxy | 4G | 200 | 10240 | 30 | 0 | 274.4 | 728.47 | 218.99 | 1319 | 96.55 | 79.539 |
|  SecureProxy | 4G | 200 | 10240 | 100 | 0 | 273.3 | 731.78 | 220.76 | 1319 | 96.59 | 83.617 |
|  SecureProxy | 4G | 200 | 10240 | 500 | 0 | 265.79 | 751.94 | 112.94 | 1079 | 96.82 | 58.847 |
|  SecureProxy | 4G | 200 | 10240 | 1000 | 0 | 178.12 | 1121.42 | 108.13 | 1447 | 97.83 | 77.669 |
|  SecureProxy | 4G | 200 | 102400 | 0 | 0 | 28.29 | 7029.78 | 1406.07 | 9663 | 65.55 | 898.012 |
|  SecureProxy | 4G | 200 | 102400 | 30 | 0 | 28.65 | 6939.29 | 1404.59 | 9663 | 64.85 | 900.687 |
|  SecureProxy | 4G | 200 | 102400 | 100 | 0 | 28.62 | 6931.39 | 1430.03 | 9727 | 65.39 | 888.535 |
|  SecureProxy | 4G | 200 | 102400 | 500 | 0 | 28.63 | 6945.24 | 1371.02 | 9535 | 64.74 | 897.237 |
|  SecureProxy | 4G | 200 | 102400 | 1000 | 0 | 28.42 | 6989.01 | 1452.78 | 9663 | 63.95 | 920.483 |
|  SecureProxy | 4G | 500 | 500 | 0 | 0 | 511.23 | 977.12 | 595.13 | 2767 | 98.36 | 86.38 |
|  SecureProxy | 4G | 500 | 500 | 30 | 0 | 508.23 | 982.5 | 579.83 | 2735 | 97.38 | 78.49 |
|  SecureProxy | 4G | 500 | 500 | 100 | 0 | 512.54 | 974.52 | 540.01 | 2575 | 98.05 | 78.87 |
|  SecureProxy | 4G | 500 | 500 | 500 | 0 | 508.98 | 981.29 | 322.93 | 1975 | 98.2 | 83.046 |
|  SecureProxy | 4G | 500 | 500 | 1000 | 0 | 434.69 | 1148.32 | 148.52 | 1711 | 98.71 | 80.45 |
|  SecureProxy | 4G | 500 | 1024 | 0 | 0 | 491.45 | 1016.17 | 603.13 | 2815 | 97.72 | 80.762 |
|  SecureProxy | 4G | 500 | 1024 | 30 | 0 | 493.48 | 1011.76 | 589.52 | 2783 | 98.1 | 79.076 |
|  SecureProxy | 4G | 500 | 1024 | 100 | 0 | 495.05 | 1009.17 | 570.08 | 2719 | 97.97 | 57.051 |
|  SecureProxy | 4G | 500 | 1024 | 500 | 0 | 491.85 | 1015.36 | 346.62 | 2063 | 97.79 | 58.523 |
|  SecureProxy | 4G | 500 | 1024 | 1000 | 0 | 430.39 | 1159.76 | 150.17 | 1727 | 98.45 | 79.147 |
|  SecureProxy | 4G | 500 | 10240 | 0 | 0 | 257.2 | 1940.51 | 476.61 | 3215 | 93.57 | 229.821 |
|  SecureProxy | 4G | 500 | 10240 | 30 | 0 | 255.65 | 1952.54 | 483.5 | 3311 | 93.2 | 221.796 |
|  SecureProxy | 4G | 500 | 10240 | 100 | 0 | 256.93 | 1942.83 | 466.47 | 3167 | 93 | 274.328 |
|  SecureProxy | 4G | 500 | 10240 | 500 | 0 | 250.78 | 1989.15 | 482.4 | 3295 | 91.14 | 323.145 |
|  SecureProxy | 4G | 500 | 10240 | 1000 | 0 | 243.94 | 2043.65 | 446.11 | 3407 | 88.96 | 421.967 |
|  SecureProxy | 4G | 500 | 102400 | 0 | 0 | 14.72 | 32950.24 | 4855.22 | 44031 | 39.3 | 1954.443 |
|  SecureProxy | 4G | 500 | 102400 | 30 | 0 | 13.83 | 34995.89 | 6516.56 | 55039 | 38.32 | 1954.133 |
|  SecureProxy | 4G | 500 | 102400 | 100 | 0 | 14.6 | 33315.32 | 4579.05 | 43007 | 39.26 | 1951.286 |
|  SecureProxy | 4G | 500 | 102400 | 500 | 0 | 13.63 | 35633.28 | 5311.35 | 49663 | 37.56 | 1984.342 |
|  SecureProxy | 4G | 500 | 102400 | 1000 | 0 | 13.67 | 35639.77 | 5518.18 | 46591 | 37.64 | 1997.772 |
|  SecureProxy | 4G | 1000 | 500 | 0 | 0 | 510.19 | 1955.96 | 664.01 | 3887 | 97.44 | 130.348 |
|  SecureProxy | 4G | 1000 | 500 | 30 | 0 | 505.96 | 1971.84 | 662.35 | 3919 | 97.53 | 119.611 |
|  SecureProxy | 4G | 1000 | 500 | 100 | 0 | 508.73 | 1961.69 | 661.74 | 3903 | 97.31 | 122.635 |
|  SecureProxy | 4G | 1000 | 500 | 500 | 0 | 506.38 | 1969.19 | 654.6 | 3903 | 97.01 | 75.957 |
|  SecureProxy | 4G | 1000 | 500 | 1000 | 0 | 505.24 | 1973.56 | 571.86 | 3695 | 96.74 | 76.415 |
|  SecureProxy | 4G | 1000 | 1024 | 0 | 0 | 482.99 | 2065.56 | 689.57 | 4079 | 96.97 | 161.599 |
|  SecureProxy | 4G | 1000 | 1024 | 30 | 0 | 481.64 | 2071.49 | 685.16 | 4079 | 96.44 | 199.289 |
|  SecureProxy | 4G | 1000 | 1024 | 100 | 0 | 482.28 | 2067.47 | 687.72 | 4031 | 96.49 | 139.857 |
|  SecureProxy | 4G | 1000 | 1024 | 500 | 0 | 484.52 | 2058.41 | 671.59 | 4031 | 96.72 | 79.183 |
|  SecureProxy | 4G | 1000 | 1024 | 1000 | 0 | 480.06 | 2076.25 | 613.34 | 3919 | 96.03 | 60.812 |
|  SecureProxy | 4G | 1000 | 10240 | 0 | 0 | 220.88 | 4508.53 | 856.26 | 6687 | 83.82 | 521.351 |
|  SecureProxy | 4G | 1000 | 10240 | 30 | 0 | 222.47 | 4471.48 | 854.58 | 6751 | 83.77 | 524.097 |
|  SecureProxy | 4G | 1000 | 10240 | 100 | 0 | 220.98 | 4495.79 | 824.38 | 6527 | 83.64 | 532.525 |
|  SecureProxy | 4G | 1000 | 10240 | 500 | 0 | 224.3 | 4432.06 | 863.25 | 6623 | 82.55 | 553.213 |
|  SecureProxy | 4G | 1000 | 10240 | 1000 | 0 | 219.24 | 4536.01 | 911.95 | 6911 | 81.6 | 587.007 |
|  SecureProxy | 4G | 1000 | 102400 | 0 | 100 | 7 | 121528.23 | 18330.53 | 185343 | N/A | N/A |
|  XSLTEnhancedProxy | 4G | 100 | 500 | 0 | 0 | 8874.01 | 11.22 | 17.18 | 91 | 99.1 | 81.997 |
|  XSLTEnhancedProxy | 4G | 100 | 500 | 30 | 0 | 3119.78 | 32.02 | 5.59 | 60 | 99.62 | 77.57 |
|  XSLTEnhancedProxy | 4G | 100 | 500 | 100 | 0 | 957.6 | 104.34 | 18.2 | 199 | 99.79 | 81.02 |
|  XSLTEnhancedProxy | 4G | 100 | 500 | 500 | 0 | 195.8 | 510.34 | 65.67 | 999 | 99.84 | 80.475 |
|  XSLTEnhancedProxy | 4G | 100 | 500 | 1000 | 0 | 98.17 | 1017.17 | 121.81 | 1999 | 99.84 | 78.628 |
|  XSLTEnhancedProxy | 4G | 100 | 1024 | 0 | 0 | 7267.4 | 13.71 | 16.98 | 43 | 99.07 | 65.34 |
|  XSLTEnhancedProxy | 4G | 100 | 1024 | 30 | 0 | 3087.31 | 32.35 | 5.85 | 59 | 99.59 | 79.268 |
|  XSLTEnhancedProxy | 4G | 100 | 1024 | 100 | 0 | 941.32 | 106.17 | 22.04 | 200 | 99.78 | 83.08 |
|  XSLTEnhancedProxy | 4G | 100 | 1024 | 500 | 0 | 193.43 | 516.64 | 85.49 | 999 | 99.83 | 75.967 |
|  XSLTEnhancedProxy | 4G | 100 | 1024 | 1000 | 0 | 96.63 | 1032.82 | 172.19 | 1999 | 99.85 | 78.114 |
|  XSLTEnhancedProxy | 4G | 100 | 10240 | 0 | 0 | 1198.14 | 83.22 | 319.19 | 206 | 99.2 | 74.575 |
|  XSLTEnhancedProxy | 4G | 100 | 10240 | 30 | 0 | 1136.74 | 87.88 | 147.77 | 167 | 99.33 | 60.053 |
|  XSLTEnhancedProxy | 4G | 100 | 10240 | 100 | 0 | 877.08 | 113.84 | 15.98 | 198 | 99.44 | 80.033 |
|  XSLTEnhancedProxy | 4G | 100 | 10240 | 500 | 0 | 196.87 | 507.93 | 46.67 | 519 | 99.78 | 62.292 |
|  XSLTEnhancedProxy | 4G | 100 | 10240 | 1000 | 0 | 98.37 | 1013.03 | 99.5 | 1999 | 99.81 | 78.908 |
|  XSLTEnhancedProxy | 4G | 100 | 102400 | 0 | 0 | 166.59 | 600.05 | 170.62 | 1023 | 98.69 | 75.166 |
|  XSLTEnhancedProxy | 4G | 100 | 102400 | 30 | 0 | 164.45 | 607.87 | 159.31 | 1011 | 98.68 | 75.88 |
|  XSLTEnhancedProxy | 4G | 100 | 102400 | 100 | 0 | 163.45 | 611.65 | 152.36 | 1011 | 98.65 | 77.97 |
|  XSLTEnhancedProxy | 4G | 100 | 102400 | 500 | 0 | 141.56 | 705.65 | 90.01 | 1003 | 99.06 | 76.307 |
|  XSLTEnhancedProxy | 4G | 100 | 102400 | 1000 | 0 | 93.69 | 1066.18 | 50.27 | 1231 | 99.43 | 44.688 |
|  XSLTEnhancedProxy | 4G | 200 | 500 | 0 | 0 | 9186.8 | 21.66 | 19.77 | 87 | 98.79 | 79.942 |
|  XSLTEnhancedProxy | 4G | 200 | 500 | 30 | 0 | 5694.75 | 35.07 | 5.17 | 60 | 99.31 | 80.374 |
|  XSLTEnhancedProxy | 4G | 200 | 500 | 100 | 0 | 1949.63 | 102.52 | 12.16 | 199 | 99.68 | 79.046 |
|  XSLTEnhancedProxy | 4G | 200 | 500 | 500 | 0 | 394.61 | 506.4 | 48.27 | 531 | 99.81 | 76.406 |
|  XSLTEnhancedProxy | 4G | 200 | 500 | 1000 | 0 | 195.16 | 1022.37 | 140.59 | 1999 | 99.81 | 63.14 |
|  XSLTEnhancedProxy | 4G | 200 | 1024 | 0 | 0 | 7740.41 | 25.74 | 21.91 | 101 | 98.84 | 78.89 |
|  XSLTEnhancedProxy | 4G | 200 | 1024 | 30 | 0 | 5343.76 | 37.37 | 6.36 | 62 | 99.19 | 59.136 |
|  XSLTEnhancedProxy | 4G | 200 | 1024 | 100 | 0 | 1939.61 | 103.02 | 13.44 | 199 | 99.64 | 82.48 |
|  XSLTEnhancedProxy | 4G | 200 | 1024 | 500 | 0 | 392.39 | 509.22 | 60.89 | 999 | 99.83 | 61.7 |
|  XSLTEnhancedProxy | 4G | 200 | 1024 | 1000 | 0 | 197.84 | 1008.54 | 79.67 | 1011 | 99.83 | 81.447 |
|  XSLTEnhancedProxy | 4G | 200 | 10240 | 0 | 0 | 1279.28 | 156.26 | 74.44 | 371 | 98.98 | 75.853 |
|  XSLTEnhancedProxy | 4G | 200 | 10240 | 30 | 0 | 1242.8 | 160.73 | 57.69 | 329 | 99.01 | 81.326 |
|  XSLTEnhancedProxy | 4G | 200 | 10240 | 100 | 0 | 1141.2 | 175.13 | 38.34 | 289 | 99.11 | 81.59 |
|  XSLTEnhancedProxy | 4G | 200 | 10240 | 500 | 0 | 393.3 | 508.31 | 49.58 | 991 | 99.65 | 55.896 |
|  XSLTEnhancedProxy | 4G | 200 | 10240 | 1000 | 0 | 197.8 | 1007.98 | 70.41 | 1015 | 99.74 | 57.077 |
|  XSLTEnhancedProxy | 4G | 200 | 102400 | 0 | 0 | 165.25 | 1208.79 | 233.88 | 1799 | 97.79 | 100.412 |
|  XSLTEnhancedProxy | 4G | 200 | 102400 | 30 | 0 | 162.63 | 1228.24 | 246.54 | 1839 | 97.66 | 127.34 |
|  XSLTEnhancedProxy | 4G | 200 | 102400 | 100 | 0 | 164.43 | 1214.88 | 239.71 | 1823 | 97.74 | 105.251 |
|  XSLTEnhancedProxy | 4G | 200 | 102400 | 500 | 0 | 159.09 | 1255.52 | 230.7 | 1895 | 98.02 | 57.259 |
|  XSLTEnhancedProxy | 4G | 200 | 102400 | 1000 | 0 | 151.14 | 1320.8 | 124.81 | 1695 | 98.53 | 79.517 |
|  XSLTEnhancedProxy | 4G | 500 | 500 | 0 | 0 | 8806.37 | 56.66 | 39.52 | 207 | 97.97 | 75.537 |
|  XSLTEnhancedProxy | 4G | 500 | 500 | 30 | 0 | 8344.07 | 59.82 | 20.44 | 146 | 98.25 | 90.458 |
|  XSLTEnhancedProxy | 4G | 500 | 500 | 100 | 0 | 4729.08 | 105.67 | 9.02 | 134 | 99.11 | 78.586 |
|  XSLTEnhancedProxy | 4G | 500 | 500 | 500 | 0 | 989.67 | 504.76 | 38.38 | 523 | 99.66 | 71.033 |
|  XSLTEnhancedProxy | 4G | 500 | 500 | 1000 | 0 | 495.01 | 1008.21 | 77.51 | 1011 | 99.76 | 42.701 |
|  XSLTEnhancedProxy | 4G | 500 | 1024 | 0 | 0 | 7142.94 | 69.88 | 61.37 | 289 | 98.14 | 42.185 |
|  XSLTEnhancedProxy | 4G | 500 | 1024 | 30 | 0 | 7254.9 | 68.79 | 25.42 | 164 | 98.3 | 61.993 |
|  XSLTEnhancedProxy | 4G | 500 | 1024 | 100 | 0 | 4638.54 | 107.71 | 10 | 143 | 98.98 | 79.532 |
|  XSLTEnhancedProxy | 4G | 500 | 1024 | 500 | 0 | 989.8 | 504.67 | 38.56 | 515 | 99.68 | 78.397 |
|  XSLTEnhancedProxy | 4G | 500 | 1024 | 1000 | 0 | 495.56 | 1007.06 | 69.32 | 1011 | 99.75 | 83.42 |
|  XSLTEnhancedProxy | 4G | 500 | 10240 | 0 | 0 | 1322.67 | 378.19 | 198.24 | 771 | 97.91 | 77.652 |
|  XSLTEnhancedProxy | 4G | 500 | 10240 | 30 | 0 | 1294.29 | 386.3 | 135.19 | 751 | 98.06 | 77.407 |
|  XSLTEnhancedProxy | 4G | 500 | 10240 | 100 | 0 | 1278.49 | 391.25 | 115.87 | 715 | 98.16 | 42.804 |
|  XSLTEnhancedProxy | 4G | 500 | 10240 | 500 | 0 | 921.8 | 542.11 | 45.19 | 671 | 98.89 | 43.776 |
|  XSLTEnhancedProxy | 4G | 500 | 10240 | 1000 | 0 | 495.61 | 1005.8 | 44.7 | 1023 | 99.38 | 81.304 |
|  XSLTEnhancedProxy | 4G | 500 | 102400 | 0 | 0 | 156.2 | 3189.75 | 387.63 | 4159 | 95.81 | 317.553 |
|  XSLTEnhancedProxy | 4G | 500 | 102400 | 30 | 0 | 155.57 | 3200.22 | 401.66 | 4223 | 95.66 | 311.01 |
|  XSLTEnhancedProxy | 4G | 500 | 102400 | 100 | 0 | 155 | 3213.16 | 399.33 | 4223 | 95.58 | 306.911 |
|  XSLTEnhancedProxy | 4G | 500 | 102400 | 500 | 0 | 157.86 | 3154.33 | 383.71 | 4159 | 95.66 | 301.105 |
|  XSLTEnhancedProxy | 4G | 500 | 102400 | 1000 | 0 | 157.72 | 3156.16 | 384.04 | 4159 | 96.08 | 291.616 |
|  XSLTProxy | 4G | 100 | 500 | 0 | 0 | 5589.76 | 17.82 | 16.64 | 69 | 96.32 | 58.098 |
|  XSLTProxy | 4G | 100 | 500 | 30 | 0 | 2881.33 | 34.67 | 25.2 | 64 | 98.13 | 42.536 |
|  XSLTProxy | 4G | 100 | 500 | 100 | 0 | 956.67 | 104.48 | 17.24 | 199 | 99.27 | 79.114 |
|  XSLTProxy | 4G | 100 | 500 | 500 | 0 | 193.46 | 516.23 | 83.81 | 999 | 99.73 | 82.2 |
|  XSLTProxy | 4G | 100 | 500 | 1000 | 0 | 97.57 | 1021.92 | 138.62 | 1999 | 99.79 | 79.457 |
|  XSLTProxy | 4G | 100 | 1024 | 0 | 0 | 4033.55 | 24.72 | 25.68 | 153 | 97.22 | 80.541 |
|  XSLTProxy | 4G | 100 | 1024 | 30 | 0 | 2722.87 | 36.64 | 7.52 | 67 | 98.13 | 78.443 |
|  XSLTProxy | 4G | 100 | 1024 | 100 | 0 | 958.69 | 104.24 | 15.5 | 199 | 99.26 | 70.542 |
|  XSLTProxy | 4G | 100 | 1024 | 500 | 0 | 193.19 | 517.32 | 85.97 | 999 | 99.74 | 82.093 |
|  XSLTProxy | 4G | 100 | 1024 | 1000 | 0 | 97.81 | 1019.64 | 130.16 | 1999 | 99.82 | 41.972 |
|  XSLTProxy | 4G | 100 | 10240 | 0 | 0 | 629.69 | 158.73 | 105.32 | 471 | 98.24 | 75.147 |
|  XSLTProxy | 4G | 100 | 10240 | 30 | 0 | 634.68 | 157.5 | 75.73 | 391 | 98.33 | 42.202 |
|  XSLTProxy | 4G | 100 | 10240 | 100 | 0 | 618.2 | 161.68 | 39.98 | 295 | 98.42 | 82.615 |
|  XSLTProxy | 4G | 100 | 10240 | 500 | 0 | 195.53 | 510.92 | 49.64 | 995 | 99.43 | 85.161 |
|  XSLTProxy | 4G | 100 | 10240 | 1000 | 0 | 99.33 | 1006.03 | 2.37 | 1015 | 99.64 | 77.512 |
|  XSLTProxy | 4G | 100 | 102400 | 0 | 0 | 59.12 | 1688.66 | 280.45 | 2399 | 95.54 | 191.322 |
|  XSLTProxy | 4G | 100 | 102400 | 30 | 0 | 59.48 | 1678.49 | 269.13 | 2351 | 96.3 | 74.102 |
|  XSLTProxy | 4G | 100 | 102400 | 100 | 0 | 56.38 | 1770.65 | 267.43 | 2431 | 96.55 | 83.508 |
|  XSLTProxy | 4G | 100 | 102400 | 500 | 0 | 57.82 | 1725.46 | 255.25 | 2383 | 95.72 | 187.613 |
|  XSLTProxy | 4G | 100 | 102400 | 1000 | 0 | 55.45 | 1798.75 | 214.6 | 2463 | 96.6 | 79.878 |
|  XSLTProxy | 4G | 200 | 500 | 0 | 0 | 5804.45 | 34.29 | 22.15 | 120 | 95.82 | 78.652 |
|  XSLTProxy | 4G | 200 | 500 | 30 | 0 | 4600.79 | 43.41 | 10.98 | 89 | 96.81 | 80.287 |
|  XSLTProxy | 4G | 200 | 500 | 100 | 0 | 1916.17 | 104.29 | 14.05 | 199 | 98.62 | 78.269 |
|  XSLTProxy | 4G | 200 | 500 | 500 | 0 | 390.39 | 511.82 | 69.08 | 999 | 99.6 | 82.236 |
|  XSLTProxy | 4G | 200 | 500 | 1000 | 0 | 195.63 | 1019.91 | 131.59 | 1999 | 99.73 | 78.625 |
|  XSLTProxy | 4G | 200 | 1024 | 0 | 0 | 4112.69 | 48.53 | 32.22 | 169 | 96.86 | 76.588 |
|  XSLTProxy | 4G | 200 | 1024 | 30 | 0 | 3761.49 | 53.09 | 16.92 | 118 | 97.24 | 42.006 |
|  XSLTProxy | 4G | 200 | 1024 | 100 | 0 | 1896.06 | 105.41 | 12.93 | 198 | 98.58 | 78.987 |
|  XSLTProxy | 4G | 200 | 1024 | 500 | 0 | 392.66 | 509.03 | 55.38 | 999 | 99.59 | 78.945 |
|  XSLTProxy | 4G | 200 | 1024 | 1000 | 0 | 195.99 | 1017.44 | 121.83 | 1999 | 99.71 | 77.724 |
|  XSLTProxy | 4G | 200 | 10240 | 0 | 0 | 638.38 | 313.25 | 192.19 | 863 | 97.72 | 77.514 |
|  XSLTProxy | 4G | 200 | 10240 | 30 | 0 | 629.27 | 317.9 | 158.69 | 783 | 97.8 | 77.435 |
|  XSLTProxy | 4G | 200 | 10240 | 100 | 0 | 631.03 | 316.95 | 117.66 | 667 | 97.91 | 79.315 |
|  XSLTProxy | 4G | 200 | 10240 | 500 | 0 | 392.53 | 509.21 | 34.87 | 539 | 98.83 | 61.728 |
|  XSLTProxy | 4G | 200 | 10240 | 1000 | 0 | 197.31 | 1011.7 | 70.53 | 1047 | 99.34 | 83.113 |
|  XSLTProxy | 4G | 200 | 102400 | 0 | 0 | 52.52 | 3794.32 | 651.32 | 5471 | 87.94 | 420.626 |
|  XSLTProxy | 4G | 200 | 102400 | 30 | 0 | 53.48 | 3724.03 | 654.6 | 5439 | 86.66 | 445.371 |
|  XSLTProxy | 4G | 200 | 102400 | 100 | 0 | 54.29 | 3670.8 | 651.84 | 5407 | 86.32 | 463.473 |
|  XSLTProxy | 4G | 200 | 102400 | 500 | 0 | 54.49 | 3653.49 | 625.96 | 5279 | 87.07 | 429.71 |
|  XSLTProxy | 4G | 200 | 102400 | 1000 | 0 | 53.66 | 3708.23 | 573.84 | 5311 | 87.75 | 419.81 |
|  XSLTProxy | 4G | 500 | 500 | 0 | 0 | 5385.62 | 92.75 | 45.96 | 240 | 94.97 | 80.548 |
|  XSLTProxy | 4G | 500 | 500 | 30 | 0 | 5292.73 | 94.37 | 38.95 | 219 | 94.9 | 446.369 |
|  XSLTProxy | 4G | 500 | 500 | 100 | 0 | 4090.28 | 122.16 | 20.38 | 201 | 96.48 | 80.734 |
|  XSLTProxy | 4G | 500 | 500 | 500 | 0 | 987.84 | 505.75 | 38.69 | 547 | 99.08 | 82.571 |
|  XSLTProxy | 4G | 500 | 500 | 1000 | 0 | 494.83 | 1008.06 | 73.75 | 1039 | 99.46 | 65.913 |
|  XSLTProxy | 4G | 500 | 1024 | 0 | 0 | 3895.41 | 128.2 | 64.83 | 331 | 96.07 | 82.072 |
|  XSLTProxy | 4G | 500 | 1024 | 30 | 0 | 3862.47 | 129.36 | 52.9 | 303 | 96.25 | 57.153 |
|  XSLTProxy | 4G | 500 | 1024 | 100 | 0 | 3472.06 | 143.92 | 27.06 | 234 | 96.75 | 49.801 |
|  XSLTProxy | 4G | 500 | 1024 | 500 | 0 | 984.98 | 507.34 | 38.95 | 551 | 99.02 | 83.308 |
|  XSLTProxy | 4G | 500 | 1024 | 1000 | 0 | 494.98 | 1007.59 | 69.64 | 1039 | 99.42 | 79.242 |
|  XSLTProxy | 4G | 500 | 10240 | 0 | 0 | 572.94 | 872 | 468.89 | 2207 | 96.2 | 91.964 |
|  XSLTProxy | 4G | 500 | 10240 | 30 | 0 | 577.67 | 865.22 | 420.56 | 2079 | 96.01 | 81.566 |
|  XSLTProxy | 4G | 500 | 10240 | 100 | 0 | 576.27 | 866.5 | 373.18 | 1903 | 96.22 | 77.368 |
|  XSLTProxy | 4G | 500 | 10240 | 500 | 0 | 558.3 | 894.35 | 214.15 | 1551 | 96.9 | 80.844 |
|  XSLTProxy | 4G | 500 | 10240 | 1000 | 0 | 461.56 | 1081.67 | 85.47 | 1407 | 97.82 | 81.232 |
|  XSLTProxy | 4G | 500 | 102400 | 0 | 0 | 41.57 | 11846.55 | 1698.93 | 16127 | 76.49 | 804.734 |
|  XSLTProxy | 4G | 500 | 102400 | 30 | 0 | 41.91 | 11773.45 | 1704.72 | 16191 | 73.81 | 891.396 |
|  XSLTProxy | 4G | 500 | 102400 | 100 | 0 | 39.79 | 12424.63 | 1861.9 | 17279 | 71.54 | 942.67 |
|  XSLTProxy | 4G | 500 | 102400 | 500 | 0 | 43.3 | 11427.31 | 1630.39 | 15615 | 75.03 | 834.322 |
|  XSLTProxy | 4G | 500 | 102400 | 1000 | 0 | 42.79 | 11516.26 | 1728.7 | 16063 | 75.75 | 839.687 |
|  XSLTProxy | 4G | 1000 | 500 | 0 | 0 | 5326.2 | 187.69 | 81.11 | 415 | 93.45 | 701.373 |
|  XSLTProxy | 4G | 1000 | 500 | 30 | 0 | 5312.41 | 188.19 | 68.7 | 389 | 93.32 | 686.537 |
|  XSLTProxy | 4G | 1000 | 500 | 100 | 0 | 5166.26 | 193.47 | 49.51 | 333 | 93.9 | 594.9 |
|  XSLTProxy | 4G | 1000 | 500 | 500 | 0 | 1981.58 | 504.15 | 26.22 | 543 | 97.99 | 77.247 |
|  XSLTProxy | 4G | 1000 | 500 | 1000 | 0 | 991.11 | 1006.71 | 63.01 | 1047 | 98.91 | 82.461 |
|  XSLTProxy | 4G | 1000 | 1024 | 0 | 0 | 3822.64 | 261.68 | 115.35 | 599 | 94.55 | 615.095 |
|  XSLTProxy | 4G | 1000 | 1024 | 30 | 0 | 3817.31 | 262.05 | 106.11 | 579 | 94.43 | 625.139 |
|  XSLTProxy | 4G | 1000 | 1024 | 100 | 0 | 3755.43 | 266.33 | 80.18 | 505 | 94.96 | 526.714 |
|  XSLTProxy | 4G | 1000 | 1024 | 500 | 0 | 1932.63 | 517.2 | 32.72 | 591 | 97.82 | 83.086 |
|  XSLTProxy | 4G | 1000 | 1024 | 1000 | 0 | 991.34 | 1006.34 | 54.79 | 1047 | 98.82 | 84.938 |
|  XSLTProxy | 4G | 1000 | 10240 | 0 | 0 | 514.51 | 1940.36 | 801.52 | 4159 | 89.55 | 691.023 |
|  XSLTProxy | 4G | 1000 | 10240 | 30 | 0 | 542.04 | 1841.78 | 741.58 | 3983 | 90.83 | 684.985 |
|  XSLTProxy | 4G | 1000 | 10240 | 100 | 0 | 534.7 | 1866.21 | 733.95 | 3967 | 90.13 | 670.123 |
|  XSLTProxy | 4G | 1000 | 10240 | 500 | 0 | 529.57 | 1880.97 | 638.09 | 3759 | 91.25 | 658.341 |
|  XSLTProxy | 4G | 1000 | 10240 | 1000 | 0 | 538.3 | 1852.3 | 449.8 | 3215 | 92.56 | 661.964 |
|  XSLTProxy | 4G | 1000 | 102400 | 0 | 0 | 35.85 | 26905.53 | 2187.23 | 31743 | 69.43 | 1172.853 |
|  XSLTProxy | 4G | 1000 | 102400 | 30 | 0 | 36.1 | 26857.64 | 2167.5 | 32127 | 66.92 | 1232.942 |
|  XSLTProxy | 4G | 1000 | 102400 | 100 | 0 | 36.33 | 26718.28 | 2193.08 | 32383 | 66.14 | 1217.68 |
|  XSLTProxy | 4G | 1000 | 102400 | 500 | 0 | 36.34 | 26558.83 | 2262.27 | 32255 | 67.86 | 1207.227 |
|  XSLTProxy | 4G | 1000 | 102400 | 1000 | 0 | 38.13 | 25512.57 | 2158.27 | 30847 | 66.91 | 1197.509 |
