
# Benchmarking Robotic Middleware: A Comparative Analysis of ROS and ROS 2


## Project Overview

This research addresses the critical systems integration challenges in modern robotics by systematically benchmarking the two industry-leading middlewares: **ROS (Noetic)** and **ROS 2 (Foxy)**. As ROS approaches its end-of-life, this study serves as a technical guide for researchers and engineers transitioning to ROS 2, focusing on the performance implications of the move to a **Data Distribution Service (DDS)** architecture.

---

## Chapter 1: Introduction

* **Legacy Challenges**: Before standardized middleware, robotic development required tight, proprietary integration of hardware and software, making component reusability low and system upgrades time-consuming.


* **The Middleware Solution**: Middleware acts as an intermediary layer that abstracts hardware complexities through standardized interfaces and protocols.


* **The Paradigm Shift**: While ROS pioneered open-source hardware abstraction, it suffers from a centralized "Master Node" architecture, which represents a single point of failure. ROS 2 modernizes this with decentralized, real-time capable, and secure communication.



---

## Chapter 2: Literature and Technology Review

### Architectural Frameworks

* **ROS (Centralized)**: Utilizes the **ROS Master** for node registration and topic name resolution. Communication is primarily conducted via **TCPROS** (reliable) and **UDPROS** (lightweight/less reliable).


* **ROS 2 (Decentralized)**: Replaces the custom ROS messaging framework with the **DDS standard**. This allows for peer-to-peer networking and introduces a **Quality-of-Service (QoS)** framework to control reliability, durability, and deadlines.



### Benchmarking Metrics

The study evaluates performance through three fundamental metrics:

1. **Latency**: The time delay for a message to travel from sender to receiver.
2. **Throughput**: The rate at which messages are successfully transmitted or processed.
3. **Bandwidth**: The data transfer rate, calculated as the product of throughput and message size.



---

## Chapter 3: Benchmark Design and Methodology

The research utilizes an embedded computing platform to simulate real-world constraints.

### Hardware & Software Stack

* **Device**: Raspberry Pi 3 Model B+ (64-bit quad-core @ 1.4GHz, 1GB RAM).
* **OS**: Ubuntu Server 20.04 (Focal Fossa) with a lightweight Lubuntu desktop to conserve RAM.
* **Middleware**: ROS Noetic and ROS 2 Foxy.
* **DDS Implementations**: Fast DDS and Cyclone DDS were tested for ROS 2 to evaluate the impact of different middleware vendors.



### Testing Methodology

* **Message sweep**: Payload sizes ranging from **10kb to 200kb** in 10kb increments.
* **Frequency sweep**: Communication rates from **10Hz to 200Hz** in 10Hz increments.
* **Statistical Integrity**: Every test run published **1,500 messages** to generate a large sample set. **Median latency** was used to minimize the impact of outliers.
* **Cool-down Protocols**: A 30-second cool-down period was enforced between tests to ensure hardware reset and prevent data carry-over.



---

## Chapter 4: Results and Observations

The study highlights critical performance thresholds, particularly at the **50kb message size**.

### Intra-Board Results (Internal Communication)

* **Latency Dominance**: ROS 2 significantly outperformed ROS. At 90Hz, ROS latency was **28.83 times higher** than ROS 2 with Fast DDS.


* **Throughput Thresholds**: ROS maintained a perfect **100% throughput up to 30Hz**. Beyond this, ROS throughput plummeted by 55.33% at 90Hz, whereas ROS 2 (Fast DDS) only dropped by 15.89%.



### Inter-Board Results (Wireless Communication)

* **Wireless Overhead**: Inter-board communication consistently required **1.4x to 1.9x** more duration than intra-board for both systems.


* **Scalability**: ROS throughput lead up to 20Hz but deteriorated rapidly thereafter. ROS 2 showed **graceful degradation**, making it superior for high-frequency wireless tasks.



### DDS Implementation Impact

* **Fast DDS vs. Cyclone DDS**: Fast DDS was consistently faster (lower latency) than Cyclone DDS. In intra-board tests, Cyclone DDS exhibited **70% to 200% higher latency** compared to Fast DDS.



---
## Chapter 5: Conclusion and Future Scope

### Research Summary

The study concludes that **ROS 2** is the preferred platform for high-frequency, real-time robotics due to its decentralized DDS architecture, which provides superior latency and more stable throughput under load. Legacy ROS remains a strong contender only for applications requiring maximum throughput at **low frequencies (under 20-30Hz)**.

### Technical Limitations & Future Directions

* **Hardware Throttling**: The 1GB RAM of the Pi 3B+ was identified as a potential bottleneck for ROS 2's memory-intensive DDS.


* **Future Scope**: Recommended future research includes re-running these benchmarks on **Raspberry Pi 4 (4GB RAM)** to isolate hardware constraints and profiling **CPU/Memory tradeoffs**.


* **Security Benchmarking**: Investigating the performance impact of ROS 2’s encryption and authentication mechanisms.



---

> _this reposotory represents the research presented in the M.Sc. dissertation, **"Comparing ROS and ROS 2 For Robot Communication"**, authored by Hrushikesh Sanap at the University of Glasgow._

