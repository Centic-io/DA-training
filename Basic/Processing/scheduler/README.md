# Multi-thread Parallel Processing

Library support parallel processing with scheduling job.

## Overview
This library enables efficient parallel processing by utilizing multiple worker threads. The key parameters for tuning performance are:

### 1. `run_now`: bool
A signal for the process to run now or not 

### 2. `interval`: int
Waiting time to run process after the excution

### 3. `delay`: int
Delay time that the process actually run after the command.

## Example Usage
Below is an example demonstrating how to schedule the process calculate  sum of the squares of the first billion natural numbers using this library.




```python
from cli_scheduler.scheduler_job import SchedulerJob
from ETL.mutithread import SumSquaresJob


class SumSquaresScheduler(SchedulerJob):
    def __init__(
        self,
        run_now,
        interval,
        delay,
    ):
        scheduler = f"^{run_now}@{interval}/{delay}#true"
        super().__init__(scheduler)
        self.updated_collection = updated_collection
\
    def _execute(self, *args, **kwargs):
        job = SumSquaresJob(
        batch_size=10000,
        max_workers=10
        )
        job.run()


if __name__ == "__main__":
    job = SumSquaresScheduler(
        run_now=True,
        interval=300,
        delay=0
    )
    job.run()
```
