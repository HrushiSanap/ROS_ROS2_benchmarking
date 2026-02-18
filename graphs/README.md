# Data Visualizations (Benchmarking Graphs)

## Folder Structure & Comparison Logic

The **`graphs`** folder is organized into sub-folders based on the specific architectural or framework comparison being performed. Each sub-folder contains three distinct categories: **Latency**, **Bandwidth**, and **Throughput**.

### 1. **ROS inter vs intra**

This folder compares the performance of legacy **ROS** in two different network environments:

* **Intra-board**: Communication between nodes running on a single Raspberry Pi 3B+.
* **Inter-board**: Wireless communication between two separate Raspberry Pi devices.
* **Files**: e.g., `50kb bw.png` shows how a 50KB message size impacts bandwidth when moving from local to wireless communication.

### 2. **ROS vs ROS2 DDS1 vs ROS2 DDS2**

A primary research objective: a three-way comparison between legacy ROS and two distinct ROS 2 implementations:

* **ROS**: Legacy performance baseline.
* **ROS2 DDS1**: ROS 2 utilizing **Fast DDS** (asynchronous by default).
* **ROS2 DDS2**: ROS 2 utilizing **Cyclone DDS** (synchronous by default).
* **Purpose**: Demonstrates the "abrupt performance drop" of ROS beyond specific frequency thresholds (e.g., 30Hz) compared to the "graceful degradation" of ROS 2 DDS variants.

### 3. **ROS2 DDS1 inter vs intra**

Evaluates the scalability of **Fast DDS** (DDS1):

* Compares how the decentralized DDS architecture handles the transition from local process memory to a wireless network stack.

### 4. **ROS2 DDS2 inter vs intra**

Evaluates the scalability of **Cyclone DDS** (DDS2):

* Similar to the DDS1 folder, but specifically profiles the efficiency of the Cyclone DDS implementation under wireless constraints.

### 5. **ROS2 DDS1 vs ROS2 DDS2**

A direct "head-to-head" comparison between the two primary ROS 2 middleware options:

* **Key Finding**: Highlights that **Fast DDS** often exhibits lower latency than Cyclone DDS, particularly in intra-board scenarios where Cyclone may require significantly more duration for message transmission.

---

## Visualized Parameters

Inside each sub-folder (e.g., `bandwidth`), you will find five files corresponding to the message sizes sweeped in the experiment:

* **`10kb [metric].png`**
* **`50kb [metric].png`** (Primary data point highlighted in the dissertation)
* **`100kb [metric].png`**
* **`150kb [metric].png`**
* **`200kb [metric].png`**

**X-Axis**: Represents the message frequency sweep (from **10Hz to 200Hz**).
**Y-Axis**: Represents the specific metric value (Latency in ms, Throughput in %, or Bandwidth in kb/sec).
