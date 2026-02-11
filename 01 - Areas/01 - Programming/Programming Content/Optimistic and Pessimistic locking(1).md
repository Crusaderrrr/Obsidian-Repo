---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - programming
note type: Informational Note
---
In brief:

- **Optimistic locking**: *no lock during editing*, conflict checked at commit and rolled back if error occurred, good for low-conflict, read-heavy scenarios.
    
- **Pessimistic locking**: *locks data during editing*, prevents conflicts by waiting, good for high-conflict, write-heavy scenarios. If the transaction is executed, the data that is being used is locked and no more transactions can use it before the main transaction ends.