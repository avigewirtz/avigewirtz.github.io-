# Call Graph

The call graph provides a detailed breakdown of each function's relationships with its callers and callees. This section helps identify how functions contribute to the overall execution time and which function calls might be responsible for performance bottlenecks. Each function entry in the call graph contains the following information:

1. **Function Index**: A unique index number assigned to each function in the call graph.
2. **Function Name**: The name of the function.
3. **Function Attributes**: The attributes of the function, such as its address in the binary and the source file and line number where it is defined.
4. **Called/Total Parents**: The number of times the function was called by each parent function (caller), along with the total number of calls made by the parent function.
5. **Called/Total Children**: The number of times the function called each child function (callee), along with the total number of calls made to the child function.

| index   | % time   | self    | children   | called    | name                               |
| ------- | -------- | ------- | ---------- | --------- | ---------------------------------- |
|         |          |         |            |           |                                    |
| \[1]    | 100.0    | 0.00    | 0.06       |           | start \[1]                         |
|         |          | 0.00    | 0.06       | 1/1       | main \[10]                         |
|         |          | 0.00    | 0.00       | 1/2       | time \[6]                          |
|         |          | 0.00    | 0.00       | 1/1       | fopen \[1]                         |
| ------- | -------- | ------- | ---------- | --------- | ---------------------------------- |
|         |          | 0.00    | 0.06       | 1/1       | start \[1]                         |
| \[2]    | 100.0    | 0.00    | 0.06       | 1         | main \[10]                         |
|         |          | 0.00    | 0.06       | 1/1       | strstr \[2]                        |
| ------- | -------- | ------- | ---------- | --------- | ---------------------------------- |
|         |          | 0.00    | 0.06       | 1/1       | main \[10]                         |
| \[3]    | 100.0    | 0.00    | 0.06       | 1         | strstr \[2]                        |
|         |          | 0.01    | 0.02       | 6800/8    | fopen \[1]                         |
|         |          | 0.01    | 0.01       | 10/10     | memcpy \[3]                        |
|         |          | 0.01    | 0.00       | 9/9       | write \[4]                         |
|         |          | 0.00    | 0.00       | 220/260   | time \[6]                          |
|         |          | 0.00    | 0.00       | 200/200   | tolower \[7]                       |
|         |          | 0.00    | 0.00       | 50/50     | strlen \[8]                        |
|         |          | 0.00    | 0.00       | 40/40     | strchr \[9]                        |
|         |          | 0.00    | 0.00       | 1/1       | memset \[11]                       |
|         |          | 0.00    | 0.00       | 1/1       | printf \[12]                       |
|         |          | 0.00    | 0.00       | 1/1       | fprintf \[13]                      |
| ------- | -------- | ------- | ---------- | --------- | ---------------------------------- |
| \[4]    | 59.8     | 0.01    | 0.02       | 8+472     | \<cycle 2 as a whole> \[4]         |
|         |          | 0.01    | 0.02       | 6800+260  | fopen \<cycle 2> \[1]              |
|         |          |         |            |           |                                    |
