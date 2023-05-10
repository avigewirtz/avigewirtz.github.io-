# Interpreting Gprof Output

The Gprof report consists of two main sections: the flat profile and the call graph. The flat profile provides an overview of the program's performance, listing each function's total execution time, number of calls, and average time per call. The call graph, on the other hand, displays a more detailed breakdown of each function's callers and callees, offering insights into the relationships between functions and their contributions to the overall execution time.

## Flat Profile

The flat profile offers an overview of the program's performance, providing a summary of the execution time and call count for each function. The report is sorted by the total execution time in descending order. Here are the columns you will find in the flat profile:

1. **% Time**: The percentage of the total execution time spent in the given function.
2. **Cumulative Seconds**: The cumulative time spent in the function and all preceding functions in the sorted list.
3. **Self Seconds**: The time spent in the given function, excluding time spent in calls to other functions.
4. **Calls**: The total number of calls made to the function.
5. **Self ms/call**: The average time (in milliseconds) spent in the function per call, excluding time spent in calls to other functions.
6. **Total ms/call**: The average time (in milliseconds) spent in the function per call, including time spent in calls to other functions.
7. **Function Name**: The name of the function.

## Call Graph

The call graph provides a detailed breakdown of each function's relationships with its callers and callees. This section helps identify how functions contribute to the overall execution time and which function calls might be responsible for performance bottlenecks. Each function entry in the call graph contains the following information:

1. **Function Index**: A unique index number assigned to each function in the call graph.
2. **Function Name**: The name of the function.
3. **Function Attributes**: The attributes of the function, such as its address in the binary and the source file and line number where it is defined.
4. **Called/Total Parents**: The number of times the function was called by each parent function (caller), along with the total number of calls made by the parent function.
5. **Called/Total Children**: The number of times the function called each child function (callee), along with the total number of calls made to the child function.

\
