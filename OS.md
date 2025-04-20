### Q1) Write a program to implement FCFS (with arrival time=0 for all) Calculate waiting time, turnaround time for each process. Calculate avg. waiting time, avg turnaround time.

```java
import java.util.Scanner;

public class FCFS {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        System.out.print("Enter number of processes: ");
        int n = sc.nextInt();

        int[] bt = new int[n];  // burst time
        int[] wt = new int[n];  // waiting time
        int[] tat = new int[n]; // turnaround time

        for (int i = 0; i < n; i++) {
            System.out.print("Enter burst time for process " + (i + 1) + ": ");
            bt[i] = sc.nextInt();
        }

        // FCFS scheduling logic (arrival time = 0 for all)
        wt[0] = 0;
        for (int i = 1; i < n; i++) {
            wt[i] = wt[i - 1] + bt[i - 1];
        }

        for (int i = 0; i < n; i++) {
            tat[i] = wt[i] + bt[i];
        }

        double totalWt = 0, totalTat = 0;
        System.out.println("\nProcess\tBurst Time\tWaiting Time\tTurnaround Time");
        for (int i = 0; i < n; i++) {
            totalWt += wt[i];
            totalTat += tat[i];
            System.out.println((i + 1) + "\t\t\t\t" + bt[i] + "\t\t\t\t" + wt[i] + "\t\t\t\t" + tat[i]);
        }

        System.out.printf("\nAverage Waiting Time: %.2f\n", totalWt / n);
        System.out.printf("Average Turnaround Time: %.2f\n", totalTat / n);
    }
}

```

### Q2) Write a program to implement SJF (with arrival time=0 for all) Calculate waiting time, turnaround time for each process. Calculate avg. waiting time, avg turnaround time

```java
import java.util.Scanner;
import java.util.Arrays;

public class SJF {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        System.out.print("Enter number of processes: ");
        int n = sc.nextInt();

        int[] bt = new int[n]; // burst time
        int[] wt = new int[n]; // waiting time
        int[] tat = new int[n]; // turnaround time
        int[] pid = new int[n]; // process ID

        for (int i = 0; i < n; i++) {
            System.out.print("Enter burst time for process " + (i + 1) + ": ");
            bt[i] = sc.nextInt();
            pid[i] = i + 1;
        }

        // Sort processes by burst time
        for (int i = 0; i < n - 1; i++) {
            for (int j = i + 1; j < n; j++) {
                if (bt[i] > bt[j]) {
                    int temp = bt[i];
                    bt[i] = bt[j];
                    bt[j] = temp;

                    temp = pid[i];
                    pid[i] = pid[j];
                    pid[j] = temp;
                }
            }
        }

        wt[0] = 0;
        for (int i = 1; i < n; i++) {
            wt[i] = wt[i - 1] + bt[i - 1];
        }

        for (int i = 0; i < n; i++) {
            tat[i] = wt[i] + bt[i];
        }

        double totalWt = 0, totalTat = 0;
        System.out.println("\nProcess\tBurst Time\tWaiting Time\tTurnaround Time");
        for (int i = 0; i < n; i++) {
            totalWt += wt[i];
            totalTat += tat[i];
            System.out.println(pid[i] + "\t\t" + bt[i] + "\t\t" + wt[i] + "\t\t" + tat[i]);
        }

        System.out.printf("\nAverage Waiting Time: %.2f\n", totalWt / n);
        System.out.printf("Average Turnaround Time: %.2f\n", totalTat / n);
    }
}

```

### Q3)  Write a program to implement Non preemptive Priority scheduling. Calculate waiting time, turnaround time for each process. Calculate avg. waiting time, avg. turnaround time

```java
import java.util.*;

public class PriorityScheduling {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        System.out.print("Enter number of processes: ");
        int n = sc.nextInt();

        int[] bt = new int[n];     // burst times
        int[] priority = new int[n]; // priority values (lower number = higher priority)
        int[] wt = new int[n];     // waiting times
        int[] tat = new int[n];    // turnaround times
        Integer[] pid = new Integer[n];

        for (int i = 0; i < n; i++) {
            System.out.print("Enter burst time for process " + (i + 1) + ": ");
            bt[i] = sc.nextInt();
            System.out.print("Enter priority for process " + (i + 1) + " (lower = higher priority): ");
            priority[i] = sc.nextInt();
            pid[i] = i;
        }

        // Sort by priority
        Arrays.sort(pid, Comparator.comparingInt(i -> priority[i]));

        wt[pid[0]] = 0;
        for (int i = 1; i < n; i++) {
            wt[pid[i]] = wt[pid[i - 1]] + bt[pid[i - 1]];
        }

        for (int i = 0; i < n; i++) {
            tat[i] = wt[i] + bt[i];
        }

        double totalWt = 0, totalTat = 0;
        System.out.println("\nProcess\tBT\tPriority\tWT\tTAT");
        for (int i = 0; i < n; i++) {
            totalWt += wt[i];
            totalTat += tat[i];
            System.out.println((i + 1) + "\t" + bt[i] + "\t" + priority[i] + "\t\t" + wt[i] + "\t" + tat[i]);
        }

        System.out.printf("\nAverage Waiting Time: %.2f\n", totalWt / n);
        System.out.printf("Average Turnaround Time: %.2f\n", totalTat / n);
    }
}

```

### Q4) Write a program to implement Round Robin. Calculate waiting time, turnaround time for each process. Calculate avg. waiting time, avg turnaround time

```java
import java.util.*;

public class RoundRobin {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        System.out.print("Enter number of processes: ");
        int n = sc.nextInt();
        int[] bt = new int[n]; // burst times
        int[] rt = new int[n]; // remaining times
        int[] wt = new int[n]; // waiting times
        int[] tat = new int[n]; // turnaround times

        for (int i = 0; i < n; i++) {
            System.out.print("Enter burst time for process " + (i + 1) + ": ");
            bt[i] = sc.nextInt();
            rt[i] = bt[i];
        }

        System.out.print("Enter time quantum: ");
        int quantum = sc.nextInt();

        int time = 0;
        boolean done;

        do {
            done = true;
            for (int i = 0; i < n; i++) {
                if (rt[i] > 0) {
                    done = false;
                    if (rt[i] > quantum) {
                        time += quantum;
                        rt[i] -= quantum;
                    } else {
                        time += rt[i];
                        wt[i] = time - bt[i];
                        rt[i] = 0;
                    }
                }
            }
        } while (!done);

        for (int i = 0; i < n; i++) {
            tat[i] = bt[i] + wt[i];
        }

        double totalWt = 0, totalTat = 0;
        System.out.println("\nProcess\tBT\tWT\tTAT");
        for (int i = 0; i < n; i++) {
            totalWt += wt[i];
            totalTat += tat[i];
            System.out.println((i + 1) + "\t" + bt[i] + "\t" + wt[i] + "\t" + tat[i]);
        }

        System.out.printf("\nAverage Waiting Time: %.2f\n", totalWt / n);
        System.out.printf("Average Turnaround Time: %.2f\n", totalTat / n);
    }
}

```

### Q5) Write a program to simulate the First Fit Memory Allocation Technique

```java
import java.util.Scanner;

public class FirstFit {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        System.out.print("Enter number of memory blocks: ");
        int m = sc.nextInt();
        int[] blockSize = new int[m];

        for (int i = 0; i < m; i++) {
            System.out.print("Enter size of block " + (i + 1) + ": ");
            blockSize[i] = sc.nextInt();
        }

        System.out.print("\nEnter number of processes: ");
        int n = sc.nextInt();
        int[] processSize = new int[n];
        int[] allocation = new int[n];

        for (int i = 0; i < n; i++) {
            System.out.print("Enter size of process " + (i + 1) + ": ");
            processSize[i] = sc.nextInt();
            allocation[i] = -1;
        }

        // First Fit Allocation
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {
                if (blockSize[j] >= processSize[i]) {
                    allocation[i] = j;
                    blockSize[j] -= processSize[i];
                    break;
                }
            }
        }

        System.out.println("\nProcess No.\tProcess Size\tBlock Allocated");
        for (int i = 0; i < n; i++) {
            System.out.print((i + 1) + "\t\t" + processSize[i] + "\t\t");
            if (allocation[i] != -1)
                System.out.println(allocation[i] + 1);
            else
                System.out.println("Not Allocated");
        }
    }
}

```

### Q6) Write programs to simulate the Best Fit Memory Allocation Technique

```java
import java.util.Scanner;

public class BestFit {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        System.out.print("Enter number of memory blocks: ");
        int m = sc.nextInt();
        int[] blockSize = new int[m];

        for (int i = 0; i < m; i++) {
            System.out.print("Enter size of block " + (i + 1) + ": ");
            blockSize[i] = sc.nextInt();
        }

        System.out.print("\nEnter number of processes: ");
        int n = sc.nextInt();
        int[] processSize = new int[n];
        int[] allocation = new int[n];

        for (int i = 0; i < n; i++) {
            System.out.print("Enter size of process " + (i + 1) + ": ");
            processSize[i] = sc.nextInt();
            allocation[i] = -1;
        }

        for (int i = 0; i < n; i++) {
            int bestIdx = -1;
            for (int j = 0; j < m; j++) {
                if (blockSize[j] >= processSize[i]) {
                    if (bestIdx == -1 || blockSize[j] < blockSize[bestIdx]) {
                        bestIdx = j;
                    }
                }
            }

            if (bestIdx != -1) {
                allocation[i] = bestIdx;
                blockSize[bestIdx] -= processSize[i];
            }
        }

        System.out.println("\nProcess No.\tProcess Size\tBlock Allocated");
        for (int i = 0; i < n; i++) {
            System.out.print((i + 1) + "\t\t" + processSize[i] + "\t\t");
            if (allocation[i] != -1)
                System.out.println(allocation[i] + 1);
            else
                System.out.println("Not Allocated");
        }
    }
}

```

### Q7) Write programs to simulate the Worst Fit Memory Allocation Technique

```java
import java.util.Scanner;

public class WorstFit {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        System.out.print("Enter number of memory blocks: ");
        int m = sc.nextInt();
        int[] blockSize = new int[m];

        for (int i = 0; i < m; i++) {
            System.out.print("Enter size of block " + (i + 1) + ": ");
            blockSize[i] = sc.nextInt();
        }

        System.out.print("\nEnter number of processes: ");
        int n = sc.nextInt();
        int[] processSize = new int[n];
        int[] allocation = new int[n];

        for (int i = 0; i < n; i++) {
            System.out.print("Enter size of process " + (i + 1) + ": ");
            processSize[i] = sc.nextInt();
            allocation[i] = -1;
        }

        for (int i = 0; i < n; i++) {
            int worstIdx = -1;
            for (int j = 0; j < m; j++) {
                if (blockSize[j] >= processSize[i]) {
                    if (worstIdx == -1 || blockSize[j] > blockSize[worstIdx]) {
                        worstIdx = j;
                    }
                }
            }

            if (worstIdx != -1) {
                allocation[i] = worstIdx;
                blockSize[worstIdx] -= processSize[i];
            }
        }

        System.out.println("\nProcess No.\tProcess Size\tBlock Allocated");
        for (int i = 0; i < n; i++) {
            System.out.print((i + 1) + "\t\t" + processSize[i] + "\t\t");
            if (allocation[i] != -1)
                System.out.println(allocation[i] + 1);
            else
                System.out.println("Not Allocated");
        }
    }
}

```

### Q8) Write a program to implement FIFO policy and calculate Hit ratio and Miss ratio

```java
import java.util.*;

public class FIFOPageReplacement {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        System.out.print("Enter number of frames: ");
        int frames = sc.nextInt();

        System.out.print("Enter number of pages: ");
        int n = sc.nextInt();
        int[] pages = new int[n];

        System.out.println("Enter the page reference string:");
        for (int i = 0; i < n; i++) {
            pages[i] = sc.nextInt();
        }

        Set<Integer> set = new HashSet<>();
        Queue<Integer> queue = new LinkedList<>();
        int hits = 0, misses = 0;

        for (int page : pages) {
            if (set.contains(page)) {
                hits++;
            } else {
                misses++;
                if (set.size() == frames) {
                    int removed = queue.poll();
                    set.remove(removed);
                }
                queue.add(page);
                set.add(page);
            }
        }

        System.out.println("\nHits: " + hits);
        System.out.println("Misses: " + misses);
        System.out.printf("Hit Ratio: %.2f\n", (double) hits / n);
        System.out.printf("Miss Ratio: %.2f\n", (double) misses / n);
    }
}

```

### Q9) Write a program to implement LRU policy and calculate Hit ratio and Miss ratio

```java
import java.util.Scanner;

public class LRUPageReplacement {
    static int n_frames, n_pages, p = 0, n_hits = 0, fr_num = 0;
    static int[] frames = new int[20];
    static int[] pg_ref_str = new int[20];
    static int[] priority = new int[20];

    public static int check_rep(int x) {
        for (int i = 0; i < n_frames; i++) {
            if (frames[i] == x) {
                return i;
            }
        }
        return -1;
    }

    public static int isEmpty() {
        for (int i = 0; i < n_frames; i++) {
            if (frames[i] == -1) {
                return i;
            }
        }
        return -1;
    }

    public static int LRU() {
        int min = priority[0], min_index = 0;
        for (int i = 1; i < n_frames; i++) {
            if (priority[i] < min) {
                min = priority[i];
                min_index = i;
            }
        }
        return min_index;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        System.out.print("Enter the number of frames: ");
        n_frames = sc.nextInt();

        System.out.print("Enter the number of pages: ");
        n_pages = sc.nextInt();

        System.out.print("Enter the page reference string: ");
        for (int i = 0; i < n_pages; i++) {
            pg_ref_str[i] = sc.nextInt();
        }

        System.out.println("\nReference String:");
        for (int i = 0; i < n_pages; i++) {
            System.out.printf("%3d", pg_ref_str[i]);
        }
        System.out.println();

        for (int i = 0; i < n_frames; i++) {
            frames[i] = -1;
            priority[i] = 100;
        }

        for (int i = 0; i < n_pages; i++) {
            int emptyIndex = isEmpty();
            int repIndex = check_rep(pg_ref_str[i]);

            if (emptyIndex != -1) {
                frames[emptyIndex] = pg_ref_str[i];
                priority[emptyIndex] = p++;
                System.out.printf("%3s", "F");
            } else if (repIndex != -1) {
                n_hits++;
                priority[repIndex] = p++;
                System.out.printf("%3s", "H");
            } else {
                fr_num = LRU();
                frames[fr_num] = pg_ref_str[i];
                priority[fr_num] = p++;
                System.out.printf("%3s", "F");
            }
        }

        System.out.println("\nPage Hit: " + n_hits);
        System.out.println("Page Fault: " + (n_pages - n_hits));
        System.out.printf("Hit Ratio: %.2f\n", n_hits / (float) n_pages);

        sc.close();
    }
}

```

### Q10) Write a program to implement Optimal policy and calculate Hit ratio and Miss ratio

```java
import java.util.*;

public class OptimalPageReplacement {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        System.out.print("Enter number of frames: ");
        int frames = sc.nextInt();

        System.out.print("Enter number of pages: ");
        int n = sc.nextInt();
        int[] pages = new int[n];

        System.out.println("Enter the page reference string:");
        for (int i = 0; i < n; i++) {
            pages[i] = sc.nextInt();
        }

        Set<Integer> set = new HashSet<>();
        int hits = 0, misses = 0;

        for (int i = 0; i < n; i++) {
            int page = pages[i];
            if (set.contains(page)) {
                hits++;
            } else {
                misses++;
                if (set.size() == frames) {
                    int pageToRemove = -1, farthest = i + 1;

                    for (int p : set) {
                        int j;
                        for (j = i + 1; j < n; j++) {
                            if (pages[j] == p) break;
                        }
                        if (j > farthest) {
                            farthest = j;
                            pageToRemove = p;
                        }
                    }

                    if (pageToRemove == -1) {
                        pageToRemove = set.iterator().next(); // fallback
                    }
                    set.remove(pageToRemove);
                }
                set.add(page);
            }
        }

        System.out.println("\nHits: " + hits);
        System.out.println("Misses: " + misses);
        System.out.printf("Hit Ratio: %.2f\n", (double) hits / n);
        System.out.printf("Miss Ratio: %.2f\n", (double) misses / n);
    }
}

```

### Q11) Write a program to simulate MVT

```java
import java.util.*;

public class MVT {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        System.out.print("Enter total memory size: ");
        int totalMemory = sc.nextInt();
        int memoryAvailable = totalMemory;

        System.out.print("Enter number of processes: ");
        int n = sc.nextInt();

        int[] memoryRequired = new int[n];
        boolean[] allocated = new boolean[n];

        for (int i = 0; i < n; i++) {
            System.out.print("Enter memory required for process " + (i + 1) + ": ");
            memoryRequired[i] = sc.nextInt();

            if (memoryRequired[i] <= memoryAvailable) {
                allocated[i] = true;
                memoryAvailable -= memoryRequired[i];
            } else {
                allocated[i] = false;
            }
        }

        System.out.println("\nProcess\tMemory Required\tStatus");
        for (int i = 0; i < n; i++) {
            System.out.println((i + 1) + "\t" + memoryRequired[i] + "\t\t" + (allocated[i] ? "Allocated" : "Not Allocated"));
        }

        System.out.println("\nTotal Memory: " + totalMemory);
        System.out.println("Memory Left: " + memoryAvailable);
    }
}

```

### Q12) Write a program to simulateMFT

```java
import java.util.*;

public class MFT {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        System.out.print("Enter total memory size: ");
        int totalMemory = sc.nextInt();

        System.out.print("Enter block size: ");
        int blockSize = sc.nextInt();

        int numberOfBlocks = totalMemory / blockSize;

        System.out.print("Enter number of processes: ");
        int n = sc.nextInt();

        int[] processSize = new int[n];
        boolean[] allocated = new boolean[n];
        int internalFragmentation = 0;
        int memoryUsed = 0;
        int processCount = 0;

        for (int i = 0; i < n && processCount < numberOfBlocks; i++) {
            System.out.print("Enter size of process " + (i + 1) + ": ");
            processSize[i] = sc.nextInt();

            if (processSize[i] <= blockSize) {
                allocated[i] = true;
                internalFragmentation += (blockSize - processSize[i]);
                memoryUsed += blockSize;
                processCount++;
            } else {
                allocated[i] = false;
            }
        }

        System.out.println("\nProcess\tProcess Size\tStatus");
        for (int i = 0; i < n; i++) {
            System.out.println((i + 1) + "\t" + processSize[i] + "\t\t" + (allocated[i] ? "Allocated" : "Not Allocated"));
        }

        System.out.println("\nTotal Memory: " + totalMemory);
        System.out.println("Used Memory: " + memoryUsed);
        System.out.println("Internal Fragmentation: " + internalFragmentation);
        System.out.println("External Fragmentation: " + (totalMemory - memoryUsed));
    }
}

```

### Q13) Write a program to simulate Paging technique

```java
import java.util.Scanner;

public class PagingSimulation {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        long processSize, pageSize, pmemSize;
        int nFrames, nEntries, paBits, laBits, offsetBits, pageBits, n, p = 0;
        int[] pgNo = new int[300];
        int[] fNo = new int[300];
        int[] valid = new int[300];
        String la;

        System.out.print("Enter the process size(in KB): ");
        processSize = sc.nextLong();

        System.out.print("Enter the page size(in bytes): ");
        pageSize = sc.nextLong();

        System.out.print("Enter the size of physical memory(in MB): ");
        pmemSize = sc.nextLong();

        // Converting to bytes
        processSize *= 1024;
        pmemSize *= 1024 * 1024;

        nFrames = (int)(pmemSize / pageSize);
        nEntries = (int)(processSize / pageSize);
        paBits = (int)(Math.log(pmemSize) / Math.log(2));
        laBits = (int)(Math.log(processSize) / Math.log(2));
        offsetBits = (int)(Math.log(pageSize) / Math.log(2));
        pageBits = laBits - offsetBits;

        System.out.println("\n-Total no. of frames in memory: " + nFrames + " bytes");
        System.out.println("-Number of entries in page table: " + nEntries + " bytes");
        System.out.println("-No. of bits in physical address: " + paBits + " bits");
        System.out.println("-No. of bits in logical address along with its distribution: " + laBits + " bits");
        System.out.println("Distribution - Page No. Field = " + pageBits + " bits\tOffset = " + offsetBits + " bits");

        System.out.print("\nEnter the number of entries: ");
        n = sc.nextInt();

        for (int i = 0; i < n; i++) {
            System.out.print("Enter the Page number, Frame Number and Valid bit: ");
            pgNo[i] = sc.nextInt();
            fNo[i] = sc.nextInt();
            valid[i] = sc.nextInt();
        }

        System.out.println("\nPage Table\n");
        System.out.println("Page No\t\tFrame No\tValid");
        for (int i = 0; i < n; i++) {
            System.out.println(pgNo[i] + "\t\t" + fNo[i] + "\t\t" + valid[i]);
        }

        System.out.print("\nEnter Logical address (" + laBits + " bits): ");
        la = sc.next();

        for (int i = 0; i < pageBits; i++) {
            p = p * 2 + (la.charAt(i) - '0');
        }

        if (p >= n || valid[p] != 1) {
            System.out.println("Page Fault");
        } else {
            System.out.println("Page Hit");
        }

        sc.close();
    }
}

```

### Q14) Write a program to simulate Banker’s algorithm

```java
import java.util.Scanner;

public class BankersAlgorithm {
    static class Bankers {
        int[] allocated = new int[20];
        int[] max = new int[20];
        int[] need = new int[20];
    }

    static Bankers[] b = new Bankers[20];
    static int[] available = new int[20];
    static int n, r;

    public static void PrintB() {
        System.out.println("\n\nProcess\t\tAllocated\t\tMax Need\t\tNeed");
        for (int i = 0; i < n; i++) {
            System.out.print("P" + i + "\t\t");
            for (int j = 0; j < r; j++)
                System.out.printf("%3d ", b[i].allocated[j]);
            System.out.print("\t\t");
            for (int j = 0; j < r; j++)
                System.out.printf("%3d ", b[i].max[j]);
            System.out.print("\t\t");
            for (int j = 0; j < r; j++)
                System.out.printf("%3d ", b[i].need[j]);
            System.out.println();
        }

        System.out.print("\nAvailable resources: ");
        for (int i = 0; i < r; i++)
            System.out.print(available[i] + " ");
        System.out.println();
    }

    public static void BankersAlgo() {
        int[] finish = new int[20];
        int count = 0;

        // Calculate need = max - allocated
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < r; j++) {
                b[i].need[j] = b[i].max[j] - b[i].allocated[j];
            }
        }

        PrintB();

        while (count < n) {
            boolean found = false;
            for (int i = 0; i < n; i++) {
                if (finish[i] == 0) {
                    int j;
                    for (j = 0; j < r; j++) {
                        if (b[i].need[j] > available[j])
                            break;
                    }

                    if (j == r) {
                        for (int k = 0; k < r; k++) {
                            available[k] += b[i].allocated[k];
                        }

                        finish[i] = 1;
                        found = true;
                        count++;
                        System.out.print("P" + i + " ");
                    }
                }
            }

            if (!found)
                break;
        }

        if (count == n)
            System.out.println("\nSafe state");
        else
            System.out.println("\nUnsafe state");
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        System.out.print("Enter r: ");
        r = sc.nextInt();

        System.out.print("Enter number of processes: ");
        n = sc.nextInt();

        // Initialize each process object
        for (int i = 0; i < n; i++) {
            b[i] = new Bankers();
        }

        System.out.println("Enter the allocated resources: ");
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < r; j++) {
                b[i].allocated[j] = sc.nextInt();
            }
        }

        System.out.println("Enter the max need: ");
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < r; j++) {
                b[i].max[j] = sc.nextInt();
            }
        }

        System.out.println("Enter the available resources: ");
        for (int i = 0; i < r; i++) {
            available[i] = sc.nextInt();
        }

        BankersAlgo();
        sc.close();
    }
}

```

### Q15) Write a program to implement the FCFS Disk Scheduling Policy

```java
import java.util.Scanner;

public class DiskFCFS {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        System.out.print("Enter number of disk requests: ");
        int n = sc.nextInt();

        int[] request = new int[n];
        System.out.println("Enter disk request sequence:");
        for (int i = 0; i < n; i++) {
            request[i] = sc.nextInt();
        }

        System.out.print("Enter initial head position: ");
        int head = sc.nextInt();

        int totalMovement = 0;
        for (int i = 0; i < n; i++) {
            totalMovement += Math.abs(request[i] - head);
            head = request[i];
        }

        System.out.println("Total Head Movement: " + totalMovement);
    }
}

```

### Q16) Write a program to implement the following SSTF Disk Scheduling Policy

```java
import java.util.*;

public class DiskSSTF {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        System.out.print("Enter number of disk requests: ");
        int n = sc.nextInt();
        int[] request = new int[n];
        boolean[] visited = new boolean[n];

        System.out.println("Enter disk request sequence:");
        for (int i = 0; i < n; i++) {
            request[i] = sc.nextInt();
        }

        System.out.print("Enter initial head position: ");
        int head = sc.nextInt();

        int totalMovement = 0;
        for (int i = 0; i < n; i++) {
            int minDist = Integer.MAX_VALUE, index = -1;
            for (int j = 0; j < n; j++) {
                if (!visited[j] && Math.abs(request[j] - head) < minDist) {
                    minDist = Math.abs(request[j] - head);
                    index = j;
                }
            }
            visited[index] = true;
            totalMovement += Math.abs(request[index] - head);
            head = request[index];
        }

        System.out.println("Total Head Movement: " + totalMovement);
    }
}

```

### Q17) Write a program to implement the following SCAN Disk Scheduling Policy

```java
import java.util.*;

public class DiskSCAN {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        System.out.print("Enter number of requests: ");
        int n = sc.nextInt();
        int[] request = new int[n];

        System.out.println("Enter request sequence:");
        for (int i = 0; i < n; i++) {
            request[i] = sc.nextInt();
        }

        System.out.print("Enter initial head position: ");
        int head = sc.nextInt();

        System.out.print("Enter disk size: ");
        int diskSize = sc.nextInt();

        System.out.print("Enter direction (left/right): ");
        String direction = sc.next();

        Arrays.sort(request);
        int totalMovement = 0;
        int pos = 0;

        for (int i = 0; i < n; i++) {
            if (request[i] >= head) {
                pos = i;
                break;
            }
        }

        if (direction.equalsIgnoreCase("right")) {
            for (int i = pos; i < n; i++) {
                totalMovement += Math.abs(head - request[i]);
                head = request[i];
            }
            totalMovement += Math.abs(head - (diskSize - 1));
            head = diskSize - 1;
            for (int i = pos - 1; i >= 0; i--) {
                totalMovement += Math.abs(head - request[i]);
                head = request[i];
            }
        } else {
            for (int i = pos - 1; i >= 0; i--) {
                totalMovement += Math.abs(head - request[i]);
                head = request[i];
            }
            totalMovement += head;
            head = 0;
            for (int i = pos; i < n; i++) {
                totalMovement += Math.abs(head - request[i]);
                head = request[i];
            }
        }

        System.out.println("Total Head Movement: " + totalMovement);
    }
}

```

### Q18) Write a program to implement the following LOOK Disk Scheduling Policy

```java
import java.util.*;

public class DiskLOOK {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        System.out.print("Enter number of requests: ");
        int n = sc.nextInt();
        int[] request = new int[n];

        System.out.println("Enter request sequence:");
        for (int i = 0; i < n; i++) {
            request[i] = sc.nextInt();
        }

        System.out.print("Enter initial head position: ");
        int head = sc.nextInt();

        System.out.print("Enter direction (left/right): ");
        String direction = sc.next();

        Arrays.sort(request);
        int totalMovement = 0;
        int pos = 0;

        for (int i = 0; i < n; i++) {
            if (request[i] >= head) {
                pos = i;
                break;
            }
        }

        if (direction.equalsIgnoreCase("right")) {
            for (int i = pos; i < n; i++) {
                totalMovement += Math.abs(head - request[i]);
                head = request[i];
            }
            for (int i = pos - 1; i >= 0; i--) {
                totalMovement += Math.abs(head - request[i]);
                head = request[i];
            }
        } else {
            for (int i = pos - 1; i >= 0; i--) {
                totalMovement += Math.abs(head - request[i]);
                head = request[i];
            }
            for (int i = pos; i < n; i++) {
                totalMovement += Math.abs(head - request[i]);
                head = request[i];
            }
        }

        System.out.println("Total Head Movement: " + totalMovement);
    }
}

```

### Q19) Write a program to implement the following CSCAN Disk Scheduling Policy

```java
import java.util.*;

public class DiskCSCAN {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        System.out.print("Enter number of requests: ");
        int n = sc.nextInt();
        int[] request = new int[n];

        System.out.println("Enter request sequence:");
        for (int i = 0; i < n; i++) {
            request[i] = sc.nextInt();
        }

        System.out.print("Enter initial head position: ");
        int head = sc.nextInt();

        System.out.print("Enter disk size: ");
        int diskSize = sc.nextInt();

        Arrays.sort(request);
        int totalMovement = 0;
        int pos = 0;

        for (int i = 0; i < n; i++) {
            if (request[i] >= head) {
                pos = i;
                break;
            }
        }

        for (int i = pos; i < n; i++) {
            totalMovement += Math.abs(head - request[i]);
            head = request[i];
        }

        totalMovement += Math.abs(head - (diskSize - 1));
        totalMovement += (diskSize - 1); // move to start (0)
        head = 0;

        for (int i = 0; i < pos; i++) {
            totalMovement += Math.abs(head - request[i]);
            head = request[i];
        }

        System.out.println("Total Head Movement: " + totalMovement);
    }
}

```

### Q20) Write a program to implement the following CLOOK Disk Scheduling Policy

```cpp
import java.util.*;

public class DiskCLOOK {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        System.out.print("Enter number of requests: ");
        int n = sc.nextInt();
        int[] request = new int[n];

        System.out.println("Enter request sequence:");
        for (int i = 0; i < n; i++) {
            request[i] = sc.nextInt();
        }

        System.out.print("Enter initial head position: ");
        int head = sc.nextInt();

        Arrays.sort(request);
        int totalMovement = 0;
        int pos = 0;

        for (int i = 0; i < n; i++) {
            if (request[i] >= head) {
                pos = i;
                break;
            }
        }

        for (int i = pos; i < n; i++) {
            totalMovement += Math.abs(head - request[i]);
            head = request[i];
        }

        totalMovement += Math.abs(head - request[0]);
        head = request[0];

        for (int i = 1; i < pos; i++) {
            totalMovement += Math.abs(head - request[i]);
            head = request[i];
        }

        System.out.println("Total Head Movement: " + totalMovement);
    }
}

```

## Q21 ) SHELL PROGRAMMING

**1) Write a command to create two input files containing five names each and perform the
following operations on the command prompt:**

a. Concatenate two files.
b. Arrange the names of the friends in ascending order.
c. Arrange the names of the friends in descending order.
d. Remove the contents of the files.
e. Repeat the entire work via a shell program

```bash
#!/bin/bash

# Part 1: Create two input files with five names each
echo "Creating two input files with five names each..."

# Create the first file
cat > friends1.txt << EOF
Alice
Bob
Charlie
David
Eva
EOF

# Create the second file
cat > friends2.txt << EOF
Frank
Grace
Hannah
Ian
Jack
EOF

echo "Files created successfully!"

# Part 2: Perform the operations
echo -e "\nPerforming operations on the files:"

# a. Concatenate two files
echo -e "\na. Concatenating the two files:"
cat friends1.txt friends2.txt > combined.txt
cat combined.txt

# b. Arrange names in ascending order
echo -e "\nb. Arranging names in ascending order:"
sort combined.txt > sorted_asc.txt
cat sorted_asc.txt

# c. Arrange names in descending order
echo -e "\nc. Arranging names in descending order:"
sort -r combined.txt > sorted_desc.txt
cat sorted_desc.txt

# d. Remove the contents of the files
echo -e "\nd. Removing the contents of the files..."
> friends1.txt
> friends2.txt
> combined.txt
> sorted_asc.txt
> sorted_desc.txt
echo "Contents removed successfully!"

# e. Repeat the entire work (already being done as this is the shell script)
echo -e "\ne. The entire work has been performed via this shell script."

echo -e "\nScript execution completed."
```

**2) Write a shell program to determine whether the entered 3-digit no is Armstrong or not**

```bash
#!/bin/bash

# Function to check if a number is Armstrong
check_armstrong() {
    number=$1
    
    # Verify it's a 3-digit number
    if [[ $number -lt 100 || $number -gt 999 ]]; then
        echo "$number is not a 3-digit number."
        return 1
    fi
    
    # Extract individual digits
    hundreds=$((number / 100))
    tens=$(((number % 100) / 10))
    units=$((number % 10))
    
    # Calculate sum of cubes
    sum=$((hundreds**3 + tens**3 + units**3))
    
    # Check if it's an Armstrong number
    if [ $sum -eq $number ]; then
        echo "$number is an Armstrong number!"
    else
        echo "$number is not an Armstrong number."
        echo "Sum of cubes = $sum (${hundreds}^3 + ${tens}^3 + ${units}^3 = $((hundreds**3)) + $((tens**3)) + $((units**3)))"
    fi
}

# Main program
echo "Armstrong Number Checker"
echo "------------------------"

# Check if number was provided as command line argument
if [ $# -eq 1 ]; then
    check_armstrong $1
else
    # If not provided as argument, ask for input
    echo "Enter a 3-digit number: "
    read number
    check_armstrong $number
fi
```

**3) Write a shell program to compute the Fibonacci series using a while loop.**

```bash
#!/bin/bash

# Shell program to compute the Fibonacci series using a while loop

echo "Fibonacci Series Calculator"
echo "--------------------------"

# Ask user for the number of terms
echo -n "Enter the number of Fibonacci terms to generate: "
read n

# Validate input
if ! [[ "$n" =~ ^[0-9]+$ ]]; then
    echo "Error: Please enter a valid positive integer"
    exit 1
fi

# Handle special cases
if [ $n -eq 0 ]; then
    echo "No terms to display"
    exit 0
elif [ $n -eq 1 ]; then
    echo "Fibonacci series (1 term): 0"
    exit 0
fi

# Initialize variables
a=0
b=1
count=1

echo -n "Fibonacci series ($n terms): $a"

# Generate Fibonacci series using while loop
while [ $count -lt $n ]
do
    echo -n ", $b"
    
    # Calculate next Fibonacci number
    next=$((a + b))
    a=$b
    b=$next
    
    ((count++))
done

echo ""  # Print newline at the end
```

**4) Write a shell program to Determine whether a person is eligible to vote.**

```bash
#!/bin/bash

# Shell program to determine whether a person is eligible to vote

echo "===== Voting Eligibility Checker ====="

# Define voting age requirement
VOTING_AGE=18

# Check if age was provided as a command line argument
if [ $# -eq 1 ]; then
    age=$1
else
    # Prompt user to enter their age
    echo -n "Please enter your age: "
    read age
fi

# Validate that the input is a number
if ! [[ "$age" =~ ^[0-9]+$ ]]; then
    echo "Error: Please enter a valid age (a positive number)"
    exit 1
fi

# Determine eligibility based on age
if [ $age -lt $VOTING_AGE ]; then
    years_left=$((VOTING_AGE - age))
    echo "Sorry, you are not eligible to vote yet."
    
    if [ $years_left -eq 1 ]; then
        echo "You need to wait 1 more year to be eligible."
    else
        echo "You need to wait $years_left more years to be eligible."
    fi
else
    echo "Congratulations! You are eligible to vote."
fi

echo "====================================="
```

**5)  Write a shell program to do the following:**

1. Display the top 10 processes in descending order.
2. Display the process with the highest memory usage.
3. Display the current user logged in and login name.
4. Display the first 11 lines from a file.

```bash
#!/bin/bash

# Shell program to display system and process information

echo "====== System Information Display ======"

# 1. Display the top 10 processes in descending order (by CPU usage)
echo -e "\n1. TOP 10 PROCESSES (by CPU usage):"
echo "----------------------------------------"
ps aux --sort=-%cpu | head -11

# 2. Display the process with the highest memory usage
echo -e "\n2. PROCESS WITH HIGHEST MEMORY USAGE:"
echo "----------------------------------------"
ps aux --sort=-%mem | head -2

# 3. Display the current user logged in and login name
echo -e "\n3. CURRENT USER INFORMATION:"
echo "----------------------------------------"
echo "Current User: $(whoami)"
echo "Login Name: $(logname 2>/dev/null || echo "$(whoami)")"
echo "All logged-in users:"
who

# 4. Display the first 11 lines from a file
echo -e "\n4. FIRST 11 LINES OF A FILE:"
echo "----------------------------------------"
# Check if file name was provided as argument
if [ $# -eq 1 ] && [ -f "$1" ]; then
    echo "Displaying first 11 lines of file: $1"
    head -11 "$1"
else
    echo "To display first 11 lines of a file, run this script with a filename:"
    echo "Example: $0 /path/to/filename"
    
    # Alternative: Ask user for file input
    echo -e "\nWould you like to specify a file now? (y/n)"
    read answer
    if [[ "$answer" =~ ^[Yy] ]]; then
        echo "Enter the path to the file:"
        read filepath
        if [ -f "$filepath" ]; then
            echo "Displaying first 11 lines of file: $filepath"
            head -11 "$filepath"
        else
            echo "Error: File '$filepath' not found or not accessible."
        fi
    fi
fi

echo -e "\n====== End of System Information ======="
```

**6) Write a shell program to create two employee files, and each should store
the following information:**

1) Empid 2) Empname 3) Salary 4) Designation 
and perform the following operations:
a) Join two files in 3rd file and display two files (concatenate two files).
b) Search for any pattern in input files. (not taken in the lab still you can try man
command to try grep command use as $man grep)

c) Sort the input files.

```bash
#!/bin/bash

# Shell program to create employee files and perform various operations

# Function to create an employee file
create_employee_file() {
    filename=$1
    echo "Creating employee file: $filename"
    
    echo "Enter details for employees (Press Ctrl+D when finished):"
    echo "Format: EmpID EmpName Salary Designation"
    echo "Example: 101 John 50000 Manager"
    
    # Create the file with headers
    echo "EmpID EmpName Salary Designation" > $filename
    
    # Read employee data from user input
    while read -p "Employee details: " line
    do
        if [ ! -z "$line" ]; then
            echo "$line" >> $filename
        fi
    done
    
    echo "File '$filename' created successfully!"
    echo
}

# Function to display file contents
display_file() {
    filename=$1
    echo "Contents of '$filename':"
    echo "------------------------"
    cat $filename
    echo "------------------------"
    echo
}

# Function to search for a pattern in files
search_pattern() {
    pattern=$1
    file1=$2
    file2=$3
    
    echo "Searching for pattern '$pattern' in files:"
    echo "In $file1:"
    grep -i "$pattern" $file1
    echo
    echo "In $file2:"
    grep -i "$pattern" $file2
    echo
}

# Function to sort files based on a column
sort_files() {
    file1=$1
    file2=$2
    column=$3
    
    echo "Sorting $file1 by column $column:"
    echo "------------------------"
    # Save header
    head -1 $file1 > temp_header
    # Sort data (skip header)
    tail -n +2 $file1 | sort -k $column > temp_data
    # Combine header and sorted data
    cat temp_header temp_data > sorted_$file1
    cat sorted_$file1
    echo "------------------------"
    
    echo "Sorting $file2 by column $column:"
    echo "------------------------"
    # Save header
    head -1 $file2 > temp_header
    # Sort data (skip header)
    tail -n +2 $file2 | sort -k $column > temp_data
    # Combine header and sorted data
    cat temp_header temp_data > sorted_$file2
    cat sorted_$file2
    echo "------------------------"
    
    # Clean up temporary files
    rm temp_header temp_data
    echo
}

# Main script execution starts here
echo "==== Employee Files Management Program ===="
echo

# Create two employee files
emp_file1="employees1.txt"
emp_file2="employees2.txt"

# Option to create files or use examples
echo "Do you want to create employee files manually? (y/n)"
read create_manually

if [ "$create_manually" = "y" ]; then
    # Create files by user input
    create_employee_file $emp_file1
    create_employee_file $emp_file2
else
    # Create example files
    echo "Creating example employee files..."
    
    # Create first employee file with sample data
    cat > $emp_file1 << EOF
EmpID EmpName Salary Designation
101 John 50000 Manager
102 Alice 45000 Developer
103 Bob 55000 Engineer
104 Diana 60000 Architect
105 Edward 40000 Analyst
EOF
    
    # Create second employee file with sample data
    cat > $emp_file2 << EOF
EmpID EmpName Salary Designation
201 Sarah 48000 TeamLead
202 Michael 52000 Developer
203 Jennifer 43000 Designer
204 Robert 58000 Manager
205 Lisa 47000 Engineer
EOF
    
    echo "Example files created successfully!"
    echo
fi

# Display both files
display_file $emp_file1
display_file $emp_file2

# a) Join two files in 3rd file and display
echo "a) Concatenating files into a third file..."
cat $emp_file1 > combined_employees.txt
# Append second file (skip header)
tail -n +2 $emp_file2 >> combined_employees.txt
display_file combined_employees.txt

# b) Search for a pattern
echo "b) Search for a pattern in both files"
echo "Enter pattern to search: "
read pattern
search_pattern "$pattern" $emp_file1 $emp_file2

# c) Sort the input files
echo "c) Sort the input files"
echo "Enter column number to sort by (1=EmpID, 2=EmpName, 3=Salary, 4=Designation): "
read sort_column
sort_files $emp_file1 $emp_file2 $sort_column

echo "All operations completed successfully!"
echo "==== End of Employee Files Management Program ===="
```

**7) Write a shell program to create Customer files, and each should store** the following information:

1) custid, 2) username, 3) city, 4) balance, 

and perform the following operations. Search for any word in from the file grep (not taken in the lab still you can try man command to try grep command use as $man grep)

```bash
#!/bin/bash

# Shell program to create customer files and search for words

# Function to create a customer file
create_customer_file() {
    filename=$1
    echo "Creating customer file: $filename"
    
    # Create the file with headers
    echo "custid username city balance" > $filename
    
    echo "Enter details for customers (Press Ctrl+D when finished):"
    echo "Format: custid username city balance"
    echo "Example: 1001 john_doe NewYork 5000"
    
    # Read customer data from user input
    while read -p "Customer details: " line
    do
        if [ ! -z "$line" ]; then
            echo "$line" >> $filename
        fi
    done
    
    echo "File '$filename' created successfully!"
    echo
}

# Function to display file contents
display_file() {
    filename=$1
    echo "Contents of '$filename':"
    echo "------------------------"
    cat $filename
    echo "------------------------"
    echo
}

# Function to search for a word in file
search_word() {
    word=$1
    file=$2
    
    echo "Searching for word '$word' in file '$file':"
    echo "------------------------"
    grep -i "$word" $file
    
    # Check if word was found
    if [ $? -ne 0 ]; then
        echo "Word '$word' not found in the file."
    fi
    echo "------------------------"
    echo
    
    # Additional search options demonstration
    echo "Advanced search options with grep:"
    echo "1. Case-sensitive search:"
    grep "$word" $file || echo "No case-sensitive matches found."
    echo
    
    echo "2. Show line numbers for matches:"
    grep -n -i "$word" $file || echo "No matches found."
    echo
    
    echo "3. Show count of matches:"
    grep -c -i "$word" $file
    echo
}

# Main script execution starts here
echo "==== Customer Files Management Program ===="
echo

# Create customer file
customer_file="customers.txt"

# Option to create file or use example
echo "Do you want to create a customer file manually? (y/n)"
read create_manually

if [ "$create_manually" = "y" ]; then
    # Create file by user input
    create_customer_file $customer_file
else
    # Create example file
    echo "Creating example customer file..."
    
    # Create customer file with sample data
    cat > $customer_file << EOF
custid username city balance
1001 john_doe NewYork 5000
1002 alice_smith Chicago 3500
1003 robert_jones Boston 7200
1004 sarah_brown NewYork 4800
1005 michael_davis LosAngeles 6300
1006 emma_wilson Chicago 2900
1007 david_taylor Miami 8100
1008 lisa_miller Dallas 3700
1009 james_anderson SanFrancisco 5500
1010 olivia_thomas Seattle 4200
EOF
    
    echo "Example file created successfully!"
    echo
fi

# Display the file
display_file $customer_file

# Search for a word
echo "Enter a word to search in the customer file:"
read search_term

search_word "$search_term" $customer_file

# Ask if user wants to search for another word
while true; do
    echo "Do you want to search for another word? (y/n)"
    read continue_search
    
    if [ "$continue_search" != "y" ]; then
        break
    fi
    
    echo "Enter a word to search:"
    read search_term
    search_word "$search_term" $customer_file
done

echo "Thank you for using the Customer Files Management Program!"
echo "==== End of Customer Files Management Program ===="
```