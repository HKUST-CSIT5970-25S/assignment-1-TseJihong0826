[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/IAASVEAZ)
# CSIT5970 Assignment-1: EC2 Measurement (2 questions, 4 marks)

### Deadline: 11:59PM, Feb, 28, Friday

---

### Name: XIE, Zikang
### Student Id: 21086447
### Email: zxiebh@connect.ust.hk

---

## Question 1: Measure the EC2 CPU and Memory performance

1. (1 mark) Report the name of measurement tool used in your measurements (you are free to choose *any* open source measurement software as long as it can measure CPU and memory performance). Please describe your configuration of the measurement tool, and explain why you set such a value for each parameter. Explain what the values obtained from measurement results represent (e.g., the value of your measurement result can be the execution time for a scientific computing task, a score given by the measurement tools or something else).

    > Measurement tool: `Phoronix Test Suite`<br>
    > CPU test Configuration: `none`<br>
    > `The average item in compression rate represents the average of three test results of how many million instruction executed per second. It is similar for decompression rate test result.`<br>
    > Memory Test Configuration: `1: COPY; 1: Integer.(Because i just want to test the performance of integer copy on this machine)`<br>
    > `The average item of the memory performance test result represent the average copy rate of 3 independent tests.`

2. (1 mark) Run your measurement tool on general purpose `t2.micro`, `t2.medium`, and `c5d.large` Linux instances, respectively, and find the performance differences among these instances. Launch all the instances in the **US East (N. Virginia)** region. Does the performance of EC2 instances increase commensurate with the increase of the number of vCPUs and memory resource?

    In order to answer this question, you need to complete the following table by filling out blanks with the measurement results corresponding to each instance type.

    | Size        | CPU performance                                  | Memory performance |
    | ----------- | ------------------------------------------------ | ------------------ |
    | `t2.micro`  | 3996 MIPS(compression); 3143 MIPS(decompression) | 11174.40 MB/s      |
    | `t2.medium` | 9993 MIPS(compression); 5812 MIPS(decompression) | 19518.38 MB/s      |
    | `c5d.large` | 7271 MIPS(compression); 4861 MIPS(decompression) | 13943.07 MB/s      |

    `no, the performance of EC2 instances don't increase commensurate with the increase of the number of vCPUs and memory resource`
    <br>

    > Region: US East (N. Virginia). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI.

## Question 2: Measure the EC2 Network performance

1. (1 mark) The metrics of network performance include **TCP bandwidth** and **round-trip time (RTT)**. Within the same region, what network performance is experienced between instances of the same type and different types? In order to answer this question, you need to complete the following table.

    | Type                      | TCP b/w (Mbps) | RTT (ms) |
    | ------------------------- | -------------- | -------- |
    | `t3.medium` - `t3.medium` | 1020           | 0.711    |
    | `m5.large` - `m5.large`   | 4960           | 0.214    |
    | `c5n.large` - `c5n.large` | 4960           | 0.172    |
    | `t3.medium` - `c5n.large` | 1020           | 0.473    |
    | `m5.large` - `c5n.large`  | 3940           | 0.432    |
    | `m5.large` - `t3.medium`  | 1020           | 0.723    |

    > Region: US East (N. Virginia). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI. Note: Use private IP address when using iPerf within the same region. You'll need iPerf for measuring TCP bandwidth and Ping for measuring Round-Trip time.

2. (1 mark) What about the network performance for instances deployed in different regions? In order to answer this question, you need to complete the following table.

    | Connection                | TCP b/w (Mbps) | RTT (ms) |
    | ------------------------- | -------------- | -------- |
    | N. Virginia - Oregon      | 28.3           | 85.8     |
    | N. Virginia - N. Virginia | 4560           | 0.329    |
    | Oregon - Oregon           | 4630           | 0.322    |
 
    > Region: US East (N. Virginia), US West (Oregon). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI. All instances are `c5.large`. Note: Use public IP address when using iPerf within the same region.
