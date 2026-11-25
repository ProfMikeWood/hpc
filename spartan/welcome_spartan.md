# Welcome to Spartan

Spartan is the name of the computing cluster at San José State University hosted in the College of Science. 

```{code}
:caption: View of the Spartan introduction text
################################################################################
                        _               ___ _____
   ___ _ __   __ _ _ __| |_ __ _ _ __  / _ \___ /
  / __| '_ \ / _` | '__| __/ _` | '_ \| | | ||_ \
  \__ \ |_) | (_| | |  | || (_| | | | | |_| |__) |
  |___/ .__/ \__,_|_|   \__\__,_|_| |_|\___/____/.sjsu.edu
      |_|

################################################################################
```

Spartan is a humble cluster sized to fit the needs of a small but productive group of SJSU faculty and students that require computational resources for their researching and teaching.

Spartan is made up of the following hardware:
- 72 compute nodes on the `nodes` parition (each with 2 broadwell processers that have 14 CPUs)
- 2 high memory nodes on the `himem` parition (each with 2 broadwell processors that have 6 CPUs each)
- 4 GPU notes on the `gpu` partition (each with 2 broadwell processors that have 14 GPUs each)
- a storage system with several hundred TB of shared storage

As a user, a way to think about Spartan is outlined in the following diagram:


```{figure} ../images/spartan/spartan_schematic.png
---
width=100%
---
Schematic depiction of Spartan.
```

When a user logs into Spartan, they interact with the machine through the head node. They access the head node by providing their credentials and they must be on the SJSU network for access. If the user is off site, they can use the SJSU VPN for access. From the head node, the user has access to their storage parition on the shared scratch storage system and they have the ability to submit jobs to any of the three paritions (`nodes`, `highmem` and `gpu`) through the head node. 

The next pages in this resource describe how to get credentials, access Spartan, and run jobs for your research.