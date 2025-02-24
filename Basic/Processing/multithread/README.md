# Multi-thread Parallel Processing

Library support parallel processing with multi-thread.

## Overview
This library enables efficient parallel processing by utilizing multiple worker threads. The key parameters for tuning performance are:

### 1. `max_workers` (Number of Workers)
Workers are execution units that process tasks concurrently. They can be threads or processes operating in parallel to enhance efficiency and reduce latency.

- **Definition:** Specifies the total number of workers executing tasks concurrently.
- **Example Usage:** A cloud-based AI service using multiple workers to process user queries simultaneously.
- **Worker Functionality:** Each worker fetches a task from the queue, processes it, and returns the result.

### 2. `batch_size` (Workload per Worker)
Batch size determines the number of tasks assigned to a worker in a single execution cycle.

- **Definition:** The number of data points or tasks processed together in each batch.

## Example Usage
Below is an example demonstrating how to calculate the sum of the squares of the first billion natural numbers using this library.



```python
from multithread_processing.base_job import BaseJob


class SumSquaresJob(BaseJob):
    def __init__(self, batch_size=1000, max_workers=4):
        self.n = 10 ** 9
        work_iterable = range(self.n)
        super().__init__(work_iterable, batch_size, max_workers)

    def _start(self):
        self.sum = 0

    def _execute(self):
        self.batch_executor.execute(
            self.work_iterable,
            self._execute_batch,
            total_items=self.n
        )

    def _execute_batch(self, works):
        _sum = 0
        for i in works:
            _sum += i * i
        self.sum += _sum

    def _end(self):
        print(f"Sum of the squares of the first {self.n} natural numbers: {self.sum}")
        self.batch_executor.shutdown()


if __name__ == "__main__":
    job = SumSquaresJob(
        batch_size=10000,
        max_workers=10
    )
    job.run()
```

## Key Features

Batch size determines the number of tasks assigned to a worker in a single execution cycle.

- Simple and efficient parallel processing with multi-threading.

- Customizable number of workers and batch sizes for performance tuning.
- Suitable for computationally intensive tasks such as data processing and machine learning.

## Reference

Refering [This](https://hanwenzhang123.medium.com/process-v-s-thread-and-background-processing-with-worker-25dd763fb88a) for more process, thread background understanding