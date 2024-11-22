### Operating System Lab Note

---

### 1. **Linux File Commands**
- **`ls`**: List files and directories (`-l` for detailed, `-a` for hidden files).  
- **`cd`**: Change directory (`cd ..` to go back).  
- **`pwd`**: Print current working directory.  
- **`touch`**: Create a new file (`touch file.txt`).  
- **`mkdir`**: Create a new directory (`mkdir folder`).  
- **`rm`**: Remove files/directories (`-r` for recursive).  
- **`cp`**: Copy files (`cp source dest`).  
- **`mv`**: Move/rename files (`mv oldname newname`).  
- **`cat`**: View file content (`cat file.txt`).  
- **`head`/`tail`**: Display the first/last lines of a file.

#### **Piping Commands**  
- **Input Redirection (`<`)**: Redirect a file as input for a command.  
  ```bash
  cat < file.txt  # Read from file.txt and display
  ```
- **Output Redirection (`>` and `>>`)**: Redirect output to a file.  
  ```bash
  ls > files.txt  # Overwrites content of files.txt
  ls >> files.txt  # Appends to files.txt
  ```
- **Piping (`|`)**: Pass output of one command as input to another.  
  ```bash
  ls | grep "text"  # List files and filter names containing "text"
  ```

---

### 2. **Linux Process Management Commands**  
- **`ps`**: Show running processes (`ps aux` for all).  
- **`top`**: Interactive process viewer.  
- **`kill`**: Terminate a process by PID (`kill -9 PID`).  
- **`jobs`**: List background jobs.  
- **`fg`**: Bring a job to the foreground.  
- **`bg`**: Resume a stopped job in the background.  
- **`nice`/`renice`**: Set/adjust process priority.

---

### 3. **Linux File Permission Commands** (Detailed)  
- **`chmod` Syntax**: `chmod [who][operation][permissions] file`  
  - **Who**: `u` (user), `g` (group), `o` (others), `a` (all).  
  - **Operation**: `+` (add), `-` (remove), `=` (set exact).  
  - **Permissions**: `r` (read), `w` (write), `x` (execute).
  - 7 = rwx, 5 = r-x, 4 = r--

#### Examples:
```bash
chmod u+x file.sh    # Add execute permission for user
chmod g-w file.txt   # Remove write permission for group
chmod o=r file.txt   # Set others to read-only
chmod 755 file.txt   # Set rwxr-xr-x (user full, group and others read+execute)
```

---

### 4. **Linux System Information Commands**  
- **`uname -a`**: Kernel and OS information.  
- **`hostname`**: Display or set the system hostname.  
- **`uptime`**: Show system uptime.  
- **`df -h`**: Disk usage in human-readable format.  
- **`free -h`**: Memory usage.  

---

### 5. **Searching Commands**  
- **`grep`**: Search text in files (`grep "pattern" file.txt`).  
- **`find`**: Locate files (`find /path -name "*.txt"`).  
- **`locate`**: Quickly find files (`locate filename`).  
- **`which`**: Find executable path (`which python`).  

---

### 6. **Shell Scripting** (Detailed)  
Here’s a more detailed revision of the requested topics:

---

### **Shell Scripting (Expanded)**  

#### **1. Variables**  
- **Definition**: Variables store data values.  
- **Examples**:  
```bash
#!/bin/bash
# Assigning variables
name="Alice"
age=25
echo "Name: $name, Age: $age"
```

#### **2. Input and Output**  
- **Taking Input**:  
```bash
#!/bin/bash
# Prompt for user input
read -p "Enter your name: " user_name
echo "Hello, $user_name!"
```
- **Output Redirection**:  
```bash
echo "This is a log message" >> logfile.txt  # Append output to a file
```

#### **3. Conditional Statements**  
- **Syntax**:  
```bash
if [ condition ]; then
  # Commands if true
else
  # Commands if false
fi
```
- **Examples**:  
```bash
#!/bin/bash
file="test.txt"

if [ -f "$file" ]; then
  echo "File exists"
else
  echo "File not found"
fi
```

#### **4. Loops**  
- **For Loop**:  
```bash
#!/bin/bash
for i in {1..5}; do
  echo "Iteration $i"
done
```

- **While Loop**:  
```bash
#!/bin/bash
counter=1
while [ $counter -le 5 ]; do
  echo "Counter: $counter"
  ((counter++))
done
```

#### **5. Functions**  
- **Definition**: Functions group reusable code.  
```bash
#!/bin/bash
greet() {
  echo "Hello, $1!"
}

greet "World"  # Call function
```

#### **6. Arrays**  
- **Definition**: Arrays store multiple values.  
- **Example**:  
```bash
#!/bin/bash
fruits=("Apple" "Banana" "Cherry")

for fruit in "${fruits[@]}"; do
  echo "$fruit"
done
```

#### **7. Practical Example: Script for System Monitoring**  
```bash
#!/bin/bash
echo "System Monitoring Script"
echo "-------------------------"
echo "Current Users Logged In:"
who

echo "Disk Usage:"
df -h

echo "Memory Usage:"
free -h
```

---

### 7. **Scheduling Algorithms**  
#### **FCFS (Non-Preemptive)**  
1. Sort processes by arrival time.  
2. Execute processes sequentially.  
3. Calculate waiting and turnaround times.  

#### **SJF (Non-Preemptive)**  
1. Select process with the shortest burst time.  
2. After completion, repeat with remaining processes.  

#### **Priority Scheduling (Non-Preemptive)**  
1. Sort processes by priority (lower number = higher priority).  
2. Execute in order of priority.  

#### **Round Robin**  
1. Assign a fixed time quantum.  
2. Execute processes for quantum or until completion.  
3. Rotate until all are finished.

#### **1. FCFS (First Come, First Serve)**  
```python
def fcfs(processes, burst_times):
    waiting_time = [0] * len(processes)
    turnaround_time = [0] * len(processes)

    for i in range(1, len(processes)):
        waiting_time[i] = waiting_time[i-1] + burst_times[i-1]

    for i in range(len(processes)):
        turnaround_time[i] = waiting_time[i] + burst_times[i]

    print("Process\tBT\tWT\tTAT")
    for i in range(len(processes)):
        print(f"{processes[i]}\t{burst_times[i]}\t{waiting_time[i]}\t{turnaround_time[i]}")
```

#### **2. SJF (Shortest Job First, Non-Preemptive)**  
```python
def sjf(processes, burst_times):
    n = len(processes)
    waiting_time = [0] * n
    turnaround_time = [0] * n

    # Sort by burst time
    processes = [x for _, x in sorted(zip(burst_times, processes))]
    burst_times.sort()

    for i in range(1, n):
        waiting_time[i] = waiting_time[i-1] + burst_times[i-1]

    for i in range(n):
        turnaround_time[i] = waiting_time[i] + burst_times[i]

    print("Process\tBT\tWT\tTAT")
    for i in range(n):
        print(f"{processes[i]}\t{burst_times[i]}\t{waiting_time[i]}\t{turnaround_time[i]}")
```

---

### 8. **Deadlock Detection and Avoidance**  
- **Deadlock Detection**: Use resource allocation graphs or algorithms to check for circular dependencies.  
- **Deadlock Avoidance**: Prevent allocation if it leads to unsafe states.

#### **Banker’s Algorithm**  
1. Calculate the **Need**: `Need = Max - Allocation`.  
2. Check if a process can complete based on current resources.  
3. Allocate resources temporarily to simulate completion.  
4. Repeat until all processes are finished or a deadlock is detected.

#### Example:  
| Process | Max | Allocation | Need | Available |  
|---------|-----|------------|------|-----------|  
| P1      | 7   | 2          | 5    | 3         |  
| P2      | 4   | 1          | 3    |           |  

- Check if `Need <= Available`.  
- Allocate resources temporarily.  
- Mark process as finished and release its allocation.

---

### **Deadlock Detection and Avoidance**

#### **1. Detection**  
- Use a **Resource Allocation Graph (RAG)**.  
- Detect cycles in the graph:  
  - If cycles exist → Possible deadlock.  

#### **2. Avoidance (Banker’s Algorithm)**  
- Determine **safe state**:  
  - A system is in a safe state if all processes can complete in some order.  

##### **Steps**:  
1. **Calculate Need**: `Need = Max - Allocation`.  
2. **Check Feasibility**:  
   - Ensure `Need <= Available`.  
3. **Simulate Allocation**:  
   - If feasible, allocate temporarily and move to the next process.  
4. **Repeat**: If all processes complete, the state is safe.  

##### **Example Table**  

| Process | Max | Allocation | Need | Available |  
|---------|-----|------------|------|-----------|  
| P1      | 7   | 3          | 4    | 3         |  
| P2      | 4   | 1          | 3    |           |  

1. Check P1: `Need (4) <= Available (3)` → False.  
2. Check P2: `Need (3) <= Available (3)` → True → Allocate.  
3. Add allocation of P2 to `Available`.

---

### 9. **Page Replacement Algorithms**  
### **Page Replacement Algorithms**  

#### **1. Overview**  
- **Page Replacement**: Determines which page to replace in memory when new pages are needed.  
- **Key Terms**:  
  - **Page Fault**: Occurs when the required page is not in memory.  
  - **Frame**: A fixed-size block in memory for storing pages.  

---

#### **2. FIFO (First In First Out)**  
- **Principle**: Replace the page that has been in memory the longest.  
- **Steps**:  
  1. Maintain a queue of pages.  
  2. When a page fault occurs, evict the front of the queue.  
  3. Add the new page to the back of the queue.  

##### **Example**  
Pages: [1, 2, 3, 4, 2, 5]  
Frames: 3  

| Step | Frames | Action       | Page Fault? |
|------|--------|--------------|-------------|
| 1    | 1      | Load page 1  | Yes         |
| 2    | 1, 2   | Load page 2  | Yes         |
| 3    | 1, 2, 3| Load page 3  | Yes         |
| 4    | 2, 3, 4| Replace 1    | Yes         |
| 5    | 2, 3, 4| No change    | No          |
| 6    | 3, 4, 5| Replace 2    | Yes         |

---

#### **3. LRU (Least Recently Used)**  
- **Principle**: Replace the page that has been unused for the longest time.  
- **Steps**:  
  1. Maintain a list of recently used pages.  
  2. When a page fault occurs, evict the least recently used page.  

##### **Example**  
Pages: [1, 2, 3, 1, 4, 2]  
Frames: 3  

| Step | Frames  | Action           | Page Fault? |
|------|---------|------------------|-------------|
| 1    | 1       | Load page 1      | Yes         |
| 2    | 1, 2    | Load page 2      | Yes         |
| 3    | 1, 2, 3 | Load page 3      | Yes         |
| 4    | 1, 2, 3 | Refresh page 1   | No          |
| 5    | 2, 3, 4 | Replace page 1   | Yes         |
| 6    | 3, 4, 2 | Replace page 2   | Yes         |


