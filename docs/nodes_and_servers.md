# Nodes and Servers Planning

## Nodes

| Node              | Total Memory (MiB) | Memory Overallocate (%) | Disk Space (MiB) | Disk Overallocate (%) |
|-------------------|--------------------|-------------------------|------------------|-----------------------|
| Node-1            | 24576              | 120                     | 768000           | 120                   |
| Node-2 (optional) | 24576              | 120                     | 768000           | 120                   |

- *Adjust values according to your hardware. 24576 MiB ≈ 24 GB RAM, 768000 MiB ≈ 750 GB disk.*
- *Node-2 (optional) is for planning a second dedicated server or VPS, separate from Node-1. Add more rows as you scale to additional physical or virtual machines.*

---

### Node 1 (100% resources)
| Server        | CPU Limit (%) | Memory (MiB) | Disk Space (MiB) |
|---------------|---------------|--------------|------------------|
| Velocity Java | 30            | 512          | 512              |
| Lobby 1       | 40            | 1024         | 1024             |
| Plot Creative | 120           | 5120         | 24576            |
| Skywars       | 60            | 2560         | 12288            |
| **Total**     | **250**       | **9216**     | **38300**        |
| **Node Max**  | **400**       | **24576**    | **768000**       |

### Node 2 (70% resources)
| Server           | CPU Limit (%) | Memory (MiB) | Disk Space (MiB) |
|------------------|---------------|--------------|------------------|
| Velocity Bedrock | 30            | 512          | 512              |
| Auth             | 40            | 512          | 512              |
| Lobby 2          | 40            | 1024         | 1024             |
| Survival         | 100           | 5120         | 24576            |
| Arena PvP        | 60            | 2560         | 12288            |
| **Total**        | **270**       | **9728**     | **38912**        |
| **Node Max**     | **280**       | **24576**    | **768000**       |

**Resource Field Recommendations:**
- **CPU Pinning:** Leave blank for all servers. This allows Docker and the OS to schedule CPU dynamically for best performance. Only set if you need strict isolation.
- **Swap (MiB):** Set to 0 for all servers. Disabling swap prevents lag spikes due to swapping. If a server runs out of RAM, the OOM Killer will safely restart it.
- **Block IO Weight:** Use 500 for all servers (Docker default). Only change if you have a server that needs disk priority (rare for Minecraft).
- **OOM Killer:** Set to "Yes" for all servers. This ensures that if a server exceeds its memory allocation, it will be killed and restarted, protecting the rest of the node.

*These defaults are safe and effective for most Minecraft network setups. Adjust only if you have special requirements.*

#### Node Resource Limits
- Node 1: 4 cores (400%), 32 GB RAM (32768 MiB), 921600 MiB Disk
- Node 2: 2.8 cores (280%), 22.4 GB RAM (22938 MiB), 645120 MiB Disk (70% usable)

*All values are within safe limits for each node. Adjust as needed for future growth.*

---

## World Seeds

This section lists the Minecraft world seeds for each server. Add or update seeds as needed for your environment.

| Server        | World Seed           |
|---------------|----------------------|
| Plot Creative |                      |
| Survival      | 7822881847993768055  |
| Arena PvP     |                      |
| Skywars       |                      |

---

*This file helps you plan the nodes and servers to create, with recommended configuration for each.*

---

## Example: Server Distribution Across Two Nodes

If you have two dedicated servers, a simple and effective way to distribute the load is to split them evenly, for example:

**Node 1:**
- Velocity Java
- Lobby 1
- Survival
- Skywars

**Node 2:**
- Velocity Bedrock
- Auth
- Lobby 2
- Plot Creative
- Arena PvP

This approach helps balance memory, CPU, and disk usage. Adjust the distribution as needed based on real usage and server performance.
