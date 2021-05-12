---
layout: post
title: "Cache: Write Polices"
date: 2020-12-01 13:01:20 +0300
description: Write Policies for cache consistencies. # Add post description (optional)
img:  system-components.png # Add image post (optional)(optional)
categories: [system-components]
icon: blogging.png
---
 
 **To mitigate** inconsistent cache results we **use cache write policies** to make sure we are always in consistent state when data is being changed by some external component/system.

- #### Write-through: 
When data is updated, it is written to both the cache and the back-end storage. This mode is easy for operation but is slow in data writing because data has to be written to both the cache and the storage.
    - **Advantage**: Ensures fast retrieval while making sure the data is in the backing store and is not lost in case the cache is disrupted.
    - **Disadvantage**: Writing data will experience latency as you have to write to two places every time.
    - Good for applications that write and then re-read data frequently. This will result in slightly higher write latency but low read latency. So, it’s ok to spend a bit longer writing once, but then benefit from reading frequently with low latency.

- #### Write-back: 
When data is updated, it is written only to the cache. The modified data is written to the back-end storage only when data is removed from the cache. This mode has fast data write speed but data will be lost if a power failure occurs before the updated data is written to the storage.
    - **Advantage**: Low latency and high throughput for write-intensive applications.
    - **Disadvantage**: There is data availability risk because the cache could fail (and so suffer from data loss) before the data is persisted to the backing store. This result in the data being lost.
    - This policy is the best performer for mixed workloads as both read and write I/O have similar response time levels. In reality, you can add resiliency (e.g. by duplicating writes) to reduce the likelihood of data loss.

- #### Write-around:
Data is written only to the backing store without writing to the cache.
    - **Advantage**: Good for not flooding the cache with data that may not subsequently be re-read.
    - **Disadvantage**: Reading recently written data will result in a cache miss (and so a higher latency) because the data can only be read from the slower backing store.
    - Good for applications that don’t frequently re-read recently written data. This will result in lower write latency but higher read latency which is a acceptable trade-off for these scenarios.

<br/>

#### Simple Stub of the concept
```python
def write_through(cache, persistent_datastore, datum):
    cache.write(datum)
    persistent_datastore.write(datum)

def write_around(persistent_datastore, datum):
    persistent_datastore.write(datum)

def write_back(cache, datum):
    cache.write(datum)
    # Possibly do an async write to the persistent_datastore

class PersistentDataStore: ## could be database 
    def __init__(self):
        self.data = []

    def write(self, datum):
        print('Started writing to backing store.')
        time.sleep(2)  # Writing to disk is slow
        self.data.append(datum)
        print('Finished writing to backing store.')

    def read(self, index):
        print('Started reading from backing store.')
        time.sleep(2)  # Reading from disk is slow
        print('Finished reading from backing store.')
        return self.data[index]

class Cache:
    def __init__(self):
        self.data = []

    def write(self, datum):
        print('Started writing to cache.')
        self.data.append(datum)
        print('Finished writing to cache.')

    def read(self, index):
        print('Started reading from backing store.')
        print('Finished reading from backing store.')
        return self.data[index]
```