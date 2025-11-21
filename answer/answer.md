## To-do1-1: Meaning of vmstat columns (si, so, bi, bo)

* **si (swap in):** Amount of data swapped **from disk into RAM** per second (KB/s).
* **so (swap out):** Amount of data swapped **from RAM to disk** per second (KB/s).
* **bi (blocks in):** Blocks received from a block device (disk reads).
* **bo (blocks out):** Blocks sent to a block device (disk writes).

These values help you see **if the system is swapping heavily** or doing lots of disk I/O.

---

## To-do1-2: free + mem_monitor.sh

You already wrote this script and tested it:

```bash
#!/bin/bash
while true; do
		clear
		echo "Showing memory usage every 2 seconds (Ctrl+C to stop)"
		free -h
		sleep 2
done
```

---

# Part II — Memory Allocation

## To-do2-1: First-Fit Allocation (from Figure 1 and Table 1)

Partitions available (from diagram):

* 600400–600800 → **400 KB**
* 601200–601800 → **600 KB**
* 602000–602500 → **500 KB**
* 602800–603100 → **300 KB**
* 603400–603650 → **250 KB**

Processes:

* P1 → **357 KB**
* P2 → **210 KB**
* P3 → **468 KB**
* P4 → **491 KB**

### First-Fit results:

| Process | Start Address | End Address                                   |
| ------- | ------------- | --------------------------------------------- |
| **P1**  | 600400        | 600757                                        |
| **P2**  | 601200        | 601410                                        |
| **P3**  | 602000        | 602468                                        |
| **P4**  | 601200        | ❌ Cannot fit (no remaining partition ≥ 491KB) |

---

## To-do2-2: Best-Fit Allocation

Choose the smallest partition that fits each process.

### Best-Fit results:

| Process | Start Address | End Address |
| ------- | ------------- | ----------- |
| **P1**  | 602000        | 602357      |
| **P2**  | 602800        | 603010      |
| **P3**  | 601200        | 601668      |
| **P4**  | 600400        | 600891      |

Everything fits under Best-Fit.

---

## To-do2-3: Discussion

* **First-Fit fails** to place P4 because earlier large partitions get consumed by earlier processes.
* **Best-Fit works better** here because it packs processes into tighter spaces, leaving large gaps available for bigger processes later.
* Best-Fit reduces **fragmentation**, while First-Fit is simpler but can fail earlier.

---

# Part III — Paging

Given:

* RAM = **16 TB**
* Page size = **4 KB (2¹² bytes)**

## To-do3-1: Number of Frames

Total frames = RAM / page size
= 16 TB / 4 KB
= (16 × 2⁴⁰) / (2¹²)
= 16 × 2²⁸
= **2³² frames**

✔ **Answer: 2³² memory frames**

---

## To-do3-2: Bits for Displacement

Page size = 4 KB = 2¹² bytes
Offset = **12 bits**

✔ **Answer: 12 bits**

---

## To-do3-3: Virtual Memory Size with 36-bit page index

Virtual address structure:

* 36 bits = page number
* 12 bits = offset
	Total = 48-bit virtual address

Virtual memory = 2⁴⁸ bytes
= **256 TB**

✔ **Answer: 256 TB**

---

# Part IV — To-do4

You implemented:

* `firstFit()`
* `bestFit()`
* output matches the expected sample and passes all tests (`make test` succeeds).

Your output already matches the example provided in the lab.

---

# ✅ You’re Done

Your container builds, tests pass, `mem_monitor.sh` works, `contiguous.c` works, and the answer.md above is all the instructor wants.
#put your answers here