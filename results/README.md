
# Robotics Middleware Benchmarking Data

## Folder Overview

This folder contains raw CSV data from communication benchmarks conducted on **ROS** and **ROS 2**. The experiments measure how data size and message frequency impact system performance.

### File Naming Convention

Files are named using the following structure:
`[middleware]_[config]_[metric].csv`

* **`middleware`**:
* `ros`: Robot Operating System (ROS).
* `ros2_dds1`: ROS 2 using the **Fast DDS** middleware implementation.
* `ros2_dds2`: ROS 2 using the **Cyclone DDS** middleware implementation.


* **`config`** (Communication Type):
* `intra`: **Intra-board** (or intra-process) communication, where nodes run on the same computer or process.
* `inter`: **Inter-board** (or inter-process) communication, where nodes communicate over a network link between separate hardware units.


* **`metric`**:
* `latency`: The time delay (usually in milliseconds) for a message to travel from the publisher to the subscriber.
* `throughput`: The rate or percentage of successfully delivered messages.
* `bandwidth`: The data transfer rate (e.g., kb/sec or Mbps) achieved during transmission.



---

### Data Format

Each `.csv` file contains three columns representing the following parameters:

| Column | Name | Description |
| --- | --- | --- |
| **1** | **Data Size** | The size of the message payload (e.g., in KB). |
| **2** | **Frequency** | The rate at which messages were published (in Hz). |
| **3** | **Result** | The value for the specific metric (Latency, Throughput, or Bandwidth). |

**Example Entry (`ros_inter_latency.csv`):**
`50, 10, 2.5`

* *Interpretation*: For a **50 KB** data size sent at **10 Hz**, the resulting **latency** for **inter-board ROS** communication was **2.5** units.

---

### Notes on ROS 2 DDS Implementations

ROS 2 is built on the **Data Distribution Service (DDS)** standard. This dataset compares the two most common implementations:

1. **Fast DDS (dds1)**: Often optimized for high-throughput and feature-rich environments.
2. **Cyclone DDS (dds2)**: Focuses on simplicity and low-latency efficiency.