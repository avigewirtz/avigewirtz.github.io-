# Flat Profile

The flat profile offers an overview of the program's performance, providing a summary of the execution time and call count for each function. The report is sorted by the total execution time in descending order. Here are the columns you will find in the flat profile:

| % time | cumulative seconds | self seconds | calls | ms/call | ms/call | name    |
| ------ | ------------------ | ------------ | ----- | ------- | ------- | ------- |
| 40.00  | 0.02               | 0.02         | 6800  | 0.00    | 0.00    | fopen   |
| 30.00  | 0.03               | 0.01         | 260   | 0.04    | 0.15    | strstr  |
| 15.00  | 0.04               | 0.01         | 10    | 1.50    | 1.50    | memcpy  |
| 10.00  | 0.05               | 0.01         | 9     | 1.11    | 1.11    | write   |
| 5.00   | 0.06               | 0.01         |       |         |         | mcount  |
| 0.00   | 0.06               | 0.00         | 220   | 0.00    | 0.00    | time    |
| 0.00   | 0.06               | 0.00         | 200   | 0.00    | 0.00    | tolower |
| 0.00   | 0.06               | 0.00         | 50    | 0.00    | 0.00    | strlen  |
| 0.00   | 0.06               | 0.00         | 40    | 0.00    | 0.00    | strchr  |
| 0.00   | 0.06               | 0.00         | 2     | 0.00    | 60.00   | main    |
| 0.00   | 0.06               | 0.00         | 1     | 0.00    | 0.00    | memset  |
| 0.00   | 0.06               | 0.00         | 1     | 0.00    | 20.20   | printf  |
| 0.00   | 0.06               | 0.00         | 1     | 0.00    | 60.00   | fprintf |

* **% Time**: The percentage of the total execution time spent in the given function.
* **Cumulative Seconds**: The cumulative time spent in the function and all preceding functions in the sorted list.
* **Self Seconds**: The time spent in the given function, excluding time spent in calls to other functions.
* **Calls**: The total number of calls made to the function.
* **Self ms/call**: The average time (in milliseconds) spent in the function per call, excluding time spent in calls to other functions.
* **Total ms/call**: The average time (in milliseconds) spent in the function per call, including time spent in calls to other functions.
* **Function Name**: The name of the function.

Let's go over each column for every function:

1. `fopen`:
   * `% time`: `fopen` accounted for 40% of the total execution time.
   * `cumulative seconds`: By the end of `fopen`'s execution, 0.02 seconds had passed.
   * `self seconds`: `fopen` itself took 0.02 seconds to run.
   * `calls`: `fopen` was called 6800 times.
   * `ms/call` (self and total): The average time spent per call in `fopen` was too small to measure accurately.
2. `strstr`:
   * `% time`: `strstr` accounted for 30% of the total execution time.
   * `cumulative seconds`: By the end of `strstr`'s execution, 0.03 seconds had passed.
   * `self seconds`: `strstr` itself took 0.01 seconds to run.
   * `calls`: `strstr` was called 260 times.
   * `ms/call` (self): On average, `strstr` took 0.04 ms per call.
   * `ms/call` (total): Including time in its descendant functions, `strstr` took 0.15 ms per call.
3. `memcpy`:
   * `% time`: `memcpy` accounted for 15% of the total execution time.
   * `cumulative seconds`: By the end of `memcpy`'s execution, 0.04 seconds had passed.
   * `self seconds`: `memcpy` itself took 0.01 seconds to run.
   * `calls`: `memcpy` was called 10 times.
   * `ms/call` (self and total): On average, `memcpy` took 1.50 ms per call.
4. `write`:
   * `% time`: `write` accounted for 10% of the total execution time.
   * `cumulative seconds`: By the end of `write`'s execution, 0.05 seconds had passed.
   * `self seconds`: `write` itself took 0.01 seconds to run.
   * `calls`: `write` was called 9 times.
   * `ms/call` (self and total): On average, `write` took 1.11 ms per call.
5. `mcount`:
   * `% time`: `mcount` accounted for 5% of the total execution time.
   * `cumulative seconds`: By the end of `mcount`'s execution, 0.06 seconds had passed.
   * `self seconds`: `mcount` itself took 0.01 seconds to run.
   * `calls`: The table does not provide how many times `mcount` was called.
   * `ms/call`: The table does not provide how much time was spent per call in `mcount`.
6. The rest (`time`, `tolower`, `strlen`, `strchr`, `main`, `memset`, `printf`, and `fprintf`):
   * `% time`: Each of these functions accounted for 0% of the total execution time, meaning they had negligible impact on the total time.
   * `cumulative seconds`: By the end of each function's execution, 0.06 seconds had passed cumulatively for all functions.
   * `self seconds`: Each of these functions took 0.00 seconds to run.
   * `calls`: The number of times each function was called varies.
   * `ms/call`: The time spent per call in these functions is either not provided or too small to measure accurately.
