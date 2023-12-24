# ------ Basics of Hardware Components  ------ 

Welcome to Hardware Modules of our "Computer Systems" course! In these modules, we'll dive deep into the exciting world of computer hardware and microprocessors. Ever wondered what's inside your computer and how it makes everything work? Well, that's exactly what we're going to explore. 

![Figure 1.11 Image depicting the components of a computer system, including the CPU, motherboard, memory modules, storage devices, and various input/output ports](https://github.com/muneebmh/SIT111.github.io/assets/149995551/64a33dad-ce29-44cb-b9a4-870809f1b986)
*Figure 1.11: Image depicting the components of a computer system, including the CPU, motherboard, memory modules, storage devices, and various input/output ports (Source: Dall-E)*

# Overview of Computer Hardware Components

In the world of computing, understanding the fundamental hardware components is essential. This section provides an in-depth exploration of the various components that constitute a computer system. By the end of this section, you will have a comprehensive grasp of the intricate interplay between these components and their pivotal roles in computer functionality.

## Central Processing Unit (CPU)

The **Central Processing Unit (CPU)**, often referred to as the "brain" of the computer, is the nucleus of computing operations. It is responsible for executing instructions, performing calculations, and managing data within the system. The CPU's architecture, performance, and capabilities vary across different computing devices and generations.

### CPU Architecture

Modern CPUs are designed based on a microarchitecture that dictates their internal organization and operation. Key aspects of CPU architecture include:

+ Instruction Fetch and Decode: The CPU retrieves and interprets instructions from memory.
+ Execution Units: These units perform arithmetic and logic operations, handling tasks like addition, subtraction, multiplication, and division.
+ Registers: High-speed storage locations within the CPU used for temporary data storage and efficient data manipulation.

### CPU Performance Metrics

Understanding CPU performance is crucial for optimizing computer systems. Key performance metrics include:

+ Clock Speed: Measured in Hertz (Hz), clock speed determines how many instructions the CPU can execute per second. Higher clock speeds generally lead to faster processing.
+ Cores: CPUs may have multiple cores, each capable of executing instructions independently. Multicore processors can handle parallel tasks more efficiently.
+ Cache Memory: CPU cache stores frequently accessed data and instructions, reducing the need to fetch them from slower main memory.

![Figure 1 12](https://github.com/muneebmh/SIT111.github.io/assets/149995551/ffb6d50f-77c3-4145-a17e-5cb56b8be26a)

  *Types of RAM in Computer Systems (Source: https://quicklearncomputer.com/types-of-ram)*

## Memory (RAM)

**Random Access Memory (RAM)** serves as the computer's temporary workspace, providing high-speed data storage for currently running programs and data. RAM offers fast data access but is volatile, meaning its contents are lost when the computer is powered off.

### RAM Types

Different types of RAM exist, including:

+ **Static RAM (SRAM):** SRAM stores data using a six-transistor memory cell and is primarily used as cache memory for the CPU. It is faster but more expensive and consumes more power than DRAM, and has lower storage capacity for the same physical size​​​​.

+ **Dynamic RAM (DRAM):** DRAM stores each bit of data in a separate capacitor within an integrated circuit, making it the standard memory in modern desktop computers. It is less expensive, has a larger storage capacity, and uses less power but requires regular voltage refresh to maintain data​​​​.

+ **Synchronous Dynamic RAM (SDRAM):** Developed for higher speeds, SDRAM synchronizes with the system bus, allowing for quicker data access. It was an advancement over asynchronous memory, which operated independently of the processor​​​​.

+ **Double Data Rate RAM (DDR):** Introduced in 2000, DDR RAM transfers data on both the rising and falling edges of the clock signal, providing faster speeds and greater energy efficiency than SDRAM. It has undergone several generational improvements, including DDR2, DDR3, DDR4, and the latest DDR5​​​​.

+ **Fast Page Mode DRAM (FPM DRAM):** FPM DRAM waits through the entire process of locating and reading a data bit before proceeding to the next. It is an older type of RAM with a maximum transfer rate of around 176 Mbps​​.

+ **Extended Data Out RAM (EDO RAM):** EDO RAM improves upon FPM DRAM by beginning to locate the next bit as soon as the address of the first bit is identified, reducing the wait time between reads​

### RAM Capacity
RAM capacity significantly impacts a computer's performance. Operating systems and software demand varying amounts of RAM, so it's essential to choose an appropriate amount for specific tasks.


## Storage Devices

**Storage devices** are integral to computing as they provide a means for permanent data storage, retaining information even when the computer is powered off. In this context, we will explore two primary types of storage devices: Hard Disk Drives (HDDs) and Solid-State Drives (SSDs).

### Hard Disk Drives (HDDs)

**Hard Disk Drives**, commonly referred to as HDDs, are traditional storage devices that have been a foundational component of computing for decades. They operate on the principle of spinning disks or platters to read and write data. Key characteristics of HDDs include:

+ Storage Capacity: HDDs are known for their generous storage capacity, making them an economical choice for applications that require large storage volumes, such as media files and archives.

+ Mechanical Components: HDDs contain mechanical parts, including spinning platters and an actuator arm responsible for positioning read/write heads over data tracks. While this mechanical design has advantages in terms of capacity, it can result in slightly slower data access times compared to SSDs.

+ Cost Efficiency: One of the notable advantages of HDDs is their cost per gigabyte, which tends to be lower than that of SSDs. This makes them a preferred choice for applications with high storage demands where speed is not the primary concern.

### Solid-State Drives (SSDs)

**Solid-State Drives**, or SSDs, represent a newer generation of storage devices that have gained popularity due to their distinctive features:

+ **Flash Memory:** SSDs employ NAND flash memory for data storage, devoid of any moving parts. This design eliminates the need for spinning disks, contributing to their notable speed and durability.

+ **Speed and Performance:** SSDs offer significantly faster data access times compared to HDDs. This translates to quicker system boot times, rapid application loading, and overall improved system responsiveness.

+ **Energy Efficiency:** SSDs are known for their lower power consumption, making them an energy-efficient choice for laptops and mobile devices. This energy efficiency extends battery life for portable computing.

+ **Durability:** The absence of moving parts in SSDs makes them highly durable and resistant to physical shocks and vibrations. This quality is especially valuable for mobile devices prone to rough handling.

This comprehensive overview sets the stage for a deeper dive into each component. In subsequent sections, we will explore these hardware elements in greater detail, providing students with a solid foundation in computer hardware fundamentals.




```
Activity:
Take a moment to inspect your own laptop or computer to identify and list its major hardware components, such as the CPU, RAM, and storage type (HDD/SSD)
```








[^note]:
    The content presented in this "Computer Systems" course is the intellectual property of Deakin University. Unauthorized use, reproduction, or distribution of this material is strictly prohibited and may be subject to disciplinary and legal action in accordance with university policies. Permission for any use beyond the scope of this course must be obtained from Deakin University - School of Information Technology.
