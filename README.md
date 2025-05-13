# InterPlanetary File System (IPFS) Simulator

![IPFS System Logo](https://upload.wikimedia.org/wikipedia/commons/1/18/Ipfs-logo-1024-ice-text.png)

## Introduction

The InterPlanetary File System (IPFS) Simulator is a distributed hash table implementation that simulates a peer-to-peer network for storing and retrieving files. This project demonstrates the core concepts of distributed systems using chord protocol, B-Trees for efficient data storage, and SHA-1 hashing for content addressing.

## Table of Contents

1. [Project Overview](#project-overview)
2. [System Architecture](#system-architecture)
3. [Key Features](#key-features)
4. [Data Structures](#data-structures)
5. [Algorithms](#algorithms)
6. [Usage Guide](#usage-guide)
7. [Technical Implementation](#technical-implementation)
8. [Advanced Features](#advanced-features)

## Project Overview

The IPFS Simulator creates a ring-based distributed network of virtual machines that can store and retrieve file data. Each machine in the network is assigned a unique identifier using SHA-1 hashing. The system implements the following key functionalities:

- Insertion of files into the distributed system
- Searching for files by path or content
- Deletion of files from the system
- Dynamic addition and removal of machines (nodes) in the network
- Automatic adjustment of routing tables when network topology changes
- Persistence of system state

## System Architecture

### Chord Protocol Implementation

The system implements a variant of the Chord protocol for distributed hash tables. The architecture consists of:

1. **Ring Structure**: Machines are arranged in a circular ring based on their hashed identifiers.
2. **Routing Tables**: Each machine maintains a routing table to efficiently locate other machines.
3. **Content Addressing**: Files are hashed using SHA-1 and mapped to the appropriate machine.

### Component Hierarchy

- **RingDistributedHashTable**: The main server class that manages the entire network
- **Machine**: Individual nodes in the network that store data and routing tables
- **BTree**: Each machine uses a B-Tree to efficiently store and retrieve file data
- **FileData**: Represents file information, including path and content hash
- **PathList**: A linked list to store multiple paths for the same content
- **RoutingTable**: Maintains connections between machines for efficient lookup

## Key Features

1. **Content-Addressed Storage**: Files are identified by the hash of their content, allowing for deduplication.
2. **Efficient Data Retrieval**: B-Tree indexing ensures O(log n) search time complexity.
3. **Fault Tolerance**: The system can handle the addition and removal of machines without data loss.
4. **Multiple Path Support**: The same file content can be associated with multiple file paths.
5. **Server State Persistence**: The system can save and restore its state between sessions.
6. **User-Friendly Interface**: An interactive console interface to perform operations.

## Data Structures

### BTree
B-Tree is used for efficient storage and retrieval of file data within each machine. The implementation includes:
- Dynamic node splitting and merging
- Balancing algorithms
- Search, insert, and delete operations

### Distributed Hash Table (DHT)
The DHT is implemented using the Chord protocol:
- Finger tables for efficient routing
- Consistent hashing for load balancing
- Successor/predecessor pointers for ring navigation

### PathList
A linked list implementation to store multiple file paths that might contain the same content:
- Insert, remove, and print operations
- Ability to retrieve file data from paths

## Algorithms

### File Insertion
1. Read the file content
2. Generate SHA-1 hash of the content
3. Map the hash to the appropriate machine using consistent hashing
4. Store the file data in the machine's B-Tree

### File Search
1. For path search:
   - Hash the path
   - Find the responsible machine
   - Search in the machine's B-Tree
2. For content search:
   - Hash the content
   - Route the request to the responsible machine
   - Retrieve the file data

### Machine Management
1. For adding a machine:
   - Generate a unique machine ID
   - Find the correct position in the ring
   - Update routing tables of affected machines
   - Redistribute data if necessary
2. For removing a machine:
   - Identify the machine to remove
   - Transfer its data to successor machines
   - Update routing tables of affected machines

## Usage Guide

### Main Menu Options

1. **Insert File by giving Directory**: Add a file to the distributed system
2. **Search by giving Directory/Path**: Find a file using its path
3. **Delete File by giving Key**: Remove a file from the system
4. **Print Routing Table of Any Machine**: View the routing information
5. **Print B-Tree of Any Machine**: Visualize the data structure of a specific machine
6. **ADD Machine**: Insert a new machine into the network
7. **DELETE Machine**: Remove a machine from the network
8. **Exit Menu**: Close the application

### Example Operations

#### Adding a File
1. Select option 1 from the main menu
2. Enter the file path
3. The system will:
   - Read the file
   - Hash its content
   - Store it on the appropriate machine

#### Searching for a File
1. Select option 2 from the main menu
2. Enter the file path
3. The system will:
   - Route the request through the network
   - Return the file content if found

## Technical Implementation

### Hashing Mechanism
The project uses SHA-1 hashing for:
- Generating machine IDs
- Creating content-addressed storage
- Ensuring consistent data distribution

### Server Initialization
On startup, the system:
1. Defines the identifier space (in bits)
2. Creates the initial set of machines
3. Establishes routing tables
4. Either generates random machine IDs or accepts manual input

### Persistence
The system can save its state to disk files:
- `ServerPreviousData.txt`: Stores machine configuration
- `Paths_Files.txt`: Records file paths and their mappings

## Advanced Features

### Dynamic Network Topology
- Machines can be added or removed at runtime
- The system automatically adjusts routing tables
- Data is redistributed as needed

### B-Tree Visualization
- The system can display the B-Tree structure of any machine
- Shows the hierarchical organization of keys and values

### Multiple Path Support
- The same content can be referenced by multiple file paths
- The system maintains these relationships efficiently

---

## Requirements

- C++ compiler (supporting C++11 or later)
- Windows operating system (for console display features)

## Build Instructions

The project can be built using Visual Studio or any C++ compiler:

```
g++ -std=c++11 Source.cpp -o ipfs_simulator
```

---

*This project was developed as part of the Data Structures course.* 