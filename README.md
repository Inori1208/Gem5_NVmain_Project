# Gem5_NVmain_Project

2025 Final project for Computer Organization

![image](https://cdn.discordapp.com/emojis/1346556552945078404.webp?size=96)

## Objective

- Q1: Gem5 + NVmain build up
- Q2: Enable L3 cache
- Q3: Config last level cache to 2-way and full-way associative, and test the performance
- Q4: Modify last level cache policy based on frequency based replacement policy
- Q5: Test the performance of write back and write through policy based on 4-way associative cache with isscc_pcm
> Bonus: I gave up

## Solution

### Q1(Setup)

> Environment: Ubuntu 18.04.6 running in Oracle VirtualBox
- Just follow along with the PPT.

### Q2(Enable L3)

Multiple files needs to be changed:
- gem5/configs/common/Caches.py
- gem5/configs/common/CacheConfig.py
- gem5/configs/common/Options.py
- gem5/src/cpu/BaseCPU.py
- gem5/src/mem/XBar.py

### Q3(2-way and full-way assoc)

Add ' --l3_assoc= *number of ways associative* ' in the command line.
> Note: TA asked us to give l3 cache 1MB size, but the l3 miss rate on my computer is completly the same in different associative while running quicksort. So I changed the size to 256kB, and this did make some different in l3 miss rate.

> Note2: Full-way associative setting is kind of controvertial, some says that l3_assoc should changed to 1 to imply full-way associative, and provide links to gem5 documentary, which can't be access nowadays.

>        There's also multple people just change l3_assoc to 16384<sub>for 1MB size</sub>, and it makes me confused, so I decided to put both of them. In my case, I change l3\_assoc to 4096 since the size is 262144, and the default block size is 64.

### Q4(Frequency baced policy)

- In gem5/configs/common/Caches.py\
In where you add L3 cache class:\
add the replacement policy\
you can see whether it is worked in config.ini

### Q5(Write back & Write through)

- In gem5/src/mem/cache/bace.cc\
Important: 'BaseCache::writecleanBlk()'\
Make the cache write back everytime when write hit.\
