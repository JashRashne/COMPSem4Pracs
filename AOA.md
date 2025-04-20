### Q1)  Implement **Insertion Sort** (show output after every pass)

```java
import java.util.Scanner;

public class InsertionSort {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        
        // Get array size from user
        System.out.print("Enter the number of elements: ");
        int n = scanner.nextInt();
        
        // Create array of specified size
        int[] arr = new int[n];
        
        // Get array elements from user
        System.out.println("Enter the elements:");
        for (int i = 0; i < n; i++) {
            arr[i] = scanner.nextInt();
        }
        
        System.out.println("\nOriginal array:");
        printArray(arr);
        
        insertionSort(arr);
        
        System.out.println("\nSorted array:");
        printArray(arr);
        
        scanner.close();
    }
    
    // Insertion sort implementation with pass-by-pass output
    static void insertionSort(int[] arr) {
        int n = arr.length;
        
        for (int i = 1; i < n; i++) {
            int key = arr[i];
            int j = i - 1;
            
            // Move elements of arr[0..i-1] that are greater than key
            // to one position ahead of their current position
            
            //check karta hai ki piche koi uthaye hue se bada hai ki nai , 
            //agar bada mila toh usko aage bhej dega and
            // agar koi bada nahi mila toh fir wo jaga
            //par uthaya hua swap kardega
            while (j >= 0 && arr[j] > key) {
                arr[j + 1] = arr[j];
                j = j - 1;
            }
            arr[j + 1] = key;
            
            // Display array after each pass
            System.out.println("\nAfter pass " + i + ":");
            printArray(arr);
        }
    }
    
    // Utility method to print an array
    static void printArray(int[] arr) {
        for (int value : arr) {
            System.out.print(value + " ");
        }
        System.out.println();
    }
}
```

### Q2)  Implement **Selection Sort** (show output after every pass)

```java
import java.util.Scanner;

public class SelectionSort {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        
        // Get array size from user
        System.out.print("Enter the number of elements: ");
        int n = scanner.nextInt();
        
        // Create array of specified size
        int[] arr = new int[n];
        
        // Get array elements from user
        System.out.println("Enter the elements:");
        for (int i = 0; i < n; i++) {
            arr[i] = scanner.nextInt();
        }
        
        System.out.println("\nOriginal array:");
        printArray(arr);
        
        selectionSort(arr);
        
        System.out.println("\nSorted array:");
        printArray(arr);
        
        scanner.close();
    }
    
    // Selection sort implementation with pass-by-pass output
    static void selectionSort(int[] arr) {
        int n = arr.length;
        
        // One by one move boundary of unsorted subarray
        for (int i = 0; i < n-1; i++) {
            // Find the minimum element in unsorted array
            int minIdx = i;
            for (int j = i+1; j < n; j++) {
                if (arr[j] < arr[minIdx]) {
                    minIdx = j;
                }
            }
            
            // Swap the found minimum element with the first element
            int temp = arr[minIdx];
            arr[minIdx] = arr[i];
            arr[i] = temp;
            
            // Display array after each pass
            System.out.println("\nAfter pass " + (i+1) + ":");
            printArray(arr);
        }
    }
    
    // Utility method to print an array
    static void printArray(int[] arr) {
        for (int value : arr) {
            System.out.print(value + " ");
        }
        System.out.println();
    }
}
```

### Q3) Implement Quick Sort (Print number of calls to quick sort procedure)

```java
import java.util.Scanner;

public class QuickSort {
    // Counter for the number of calls to quick sort procedure
    private static int callCount = 0;
    
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        
        // Get array size from user
        System.out.print("Enter the number of elements: ");
        int n = scanner.nextInt();
        
        // Create array of specified size
        int[] arr = new int[n];
        
        // Get array elements from user
        System.out.println("Enter the elements:");
        for (int i = 0; i < n; i++) {
            arr[i] = scanner.nextInt();
        }
        
        System.out.println("\nOriginal array:");
        printArray(arr);
        
        // Reset the call counter before sorting
        callCount = 0;
        
        // Perform quick sort
        quickSort(arr, 0, n - 1);
        
        System.out.println("\nSorted array:");
        printArray(arr);
        
        System.out.println("\nNumber of calls to quick sort procedure: " + callCount);
        
        scanner.close();
    }
    
    // Quick sort implementation
    static void quickSort(int[] arr, int low, int high) {
        // Increment call counter
        callCount++;
        
        if (low < high) {
            // Partition the array and get the pivot index
            int pi = partition(arr, low, high);
            
            // Recursively sort elements before and after partition
            quickSort(arr, low, pi - 1);
            quickSort(arr, pi + 1, high);
        }
    }
    
    // Partition function for quick sort
    static int partition(int[] arr, int low, int high) {
        // Select the rightmost element as pivot
        int pivot = arr[high];
        
        // Index of smaller element
        int i = (low - 1);
        
        for (int j = low; j < high; j++) {
            // If current element is smaller than or equal to pivot
            if (arr[j] <= pivot) {
                i++;
                
                // Swap arr[i] and arr[j]
                int temp = arr[i];
                arr[i] = arr[j];
                arr[j] = temp;
            }
        }
        
        // Swap arr[i+1] and arr[high] (or pivot)
        int temp = arr[i + 1];
        arr[i + 1] = arr[high];
        arr[high] = temp;
        
        return i + 1;
    }
    
    // Utility method to print an array
    static void printArray(int[] arr) {
        for (int value : arr) {
            System.out.print(value + " ");
        }
        System.out.println();
    }
}
```

### Q4) Implement Merge Sort (Print number of calls to merge sort procedure)

```java
import java.util.Scanner;

public class MergeSort {
    // Counter for the number of calls to merge sort procedure
    private static int callCount = 0;
    
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        
        // Get array size from user
        System.out.print("Enter the number of elements: ");
        int n = scanner.nextInt();
        
        // Create array of specified size
        int[] arr = new int[n];
        
        // Get array elements from user
        System.out.println("Enter the elements:");
        for (int i = 0; i < n; i++) {
            arr[i] = scanner.nextInt();
        }
        
        System.out.println("\nOriginal array:");
        printArray(arr);
        
        // Reset the call counter before sorting
        callCount = 0;
        
        // Perform merge sort
        mergeSort(arr, 0, n - 1);
        
        System.out.println("\nSorted array:");
        printArray(arr);
        
        System.out.println("\nNumber of calls to merge sort procedure: " + callCount);
        
        scanner.close();
    }
    
    // Merge sort implementation
    static void mergeSort(int[] arr, int left, int right) {
        // Increment call counter
        callCount++;
        
        if (left < right) {
            // Find the middle point
            int mid = left + (right - left) / 2;
            
            // Sort first and second halves
            mergeSort(arr, left, mid);
            mergeSort(arr, mid + 1, right);
            
            // Merge the sorted halves
            merge(arr, left, mid, right);
        }
    }
    
    // Merge two subarrays of arr[]
    static void merge(int[] arr, int left, int mid, int right) {
        // Find sizes of two subarrays to be merged
        int n1 = mid - left + 1;
        int n2 = right - mid;
        
        // Create temp arrays
        int[] L = new int[n1];
        int[] R = new int[n2];
        
        // Copy data to temp arrays
        for (int i = 0; i < n1; ++i)
            L[i] = arr[left + i];
        for (int j = 0; j < n2; ++j)
            R[j] = arr[mid + 1 + j];
        
        // Merge the temp arrays
        
        // Initial indexes of first and second subarrays
        int i = 0, j = 0;
        
        // Initial index of merged subarray
        int k = left;
        while (i < n1 && j < n2) {
            if (L[i] <= R[j]) {
                arr[k] = L[i];
                i++;
            } else {
                arr[k] = R[j];
                j++;
            }
            k++;
        }
        
        // Copy remaining elements of L[] if any
        while (i < n1) {
            arr[k] = L[i];
            i++;
            k++;
        }
        
        // Copy remaining elements of R[] if any
        while (j < n2) {
            arr[k] = R[j];
            j++;
            k++;
        }
    }
    
    // Utility method to print an array
    static void printArray(int[] arr) {
        for (int value : arr) {
            System.out.print(value + " ");
        }
        System.out.println();
    }
}
```

### Q5) Implement minimum spanning tree using Prim’s algorithm. (Print minimum cost and edges in MST)

```java
// A Java program for Prim's Minimum Spanning Tree (MST)
// algorithm. The program is for adjacency matrix
// representation of the graph

import java.io.*;
import java.lang.*;
import java.util.*;

class MST {

    // A utility function to find the vertex with minimum
    // key value, from the set of vertices not yet included
    // in MST
    int minKey(int key[], Boolean mstSet[])
    {
        // Initialize min value
        int min = Integer.MAX_VALUE, min_index = -1;

        for (int v = 0; v < mstSet.length; v++)
            if (mstSet[v] == false && key[v] < min) {
                min = key[v];
                min_index = v;
            }

        return min_index;
    }

    // A utility function to print the constructed MST
    // stored in parent[]
    void printMST(int parent[], int graph[][])
    {
        int sum = 0;
        System.out.println("Edge \tWeight");
        for (int i = 1; i < graph.length; i++){
            System.out.println(parent[i] + " - " + i + "\t"
                               + graph[parent[i]][i]);
            sum += graph[parent[i]][i];
        }
        
        System.out.println("\n\nTotal Cost is " + sum);
                               
        
    }

    // Function to construct and print MST for a graph
    // represented using adjacency matrix representation
    void primMST(int graph[][])
    {
        int V = graph.length;
        
        // Array to store constructed MST
        int parent[] = new int[V];

        // Key values used to pick minimum weight edge in
        // cut
        int key[] = new int[V];

        // To represent set of vertices included in MST
        Boolean mstSet[] = new Boolean[V];

        // Initialize all keys as INFINITE
        for (int i = 0; i < V; i++) {
            key[i] = Integer.MAX_VALUE;
            mstSet[i] = false;
        }

        // Always include first 1st vertex in MST.
        // Make key 0 so that this vertex is
        // picked as first vertex
        key[0] = 0;
      
        // First node is always root of MST
        parent[0] = -1;

        // The MST will have V vertices
        for (int count = 0; count < V - 1; count++) {
            
            // Pick the minimum key vertex from the set of
            // vertices not yet included in MST
            int u = minKey(key, mstSet);

            // Add the picked vertex to the MST Set
            mstSet[u] = true;

            // Update key value and parent index of the
            // adjacent vertices of the picked vertex.
            // Consider only those vertices which are not
            // yet included in MST
            for (int v = 0; v < V; v++)

                // graph[u][v] is non zero only for adjacent
                // vertices of m mstSet[v] is false for
                // vertices not yet included in MST Update
                // the key only if graph[u][v] is smaller
                // than key[v]
                if (graph[u][v] != 0 && mstSet[v] == false
                    && graph[u][v] < key[v]) {
                    parent[v] = u;
                    key[v] = graph[u][v];
                }
        }

        // Print the constructed MST
        printMST(parent, graph);
    }

    public static void main(String[] args)
    {
        MST t = new MST();
        int graph[][] = new int[][] { { 0, 2, 0, 6, 0 },
                                      { 2, 0, 3, 8, 5 },
                                      { 0, 3, 0, 0, 7 },
                                      { 6, 8, 0, 0, 9 },
                                      { 0, 5, 7, 9, 0 } };

        // Print the solution
        t.primMST(graph);
    }
}

```

### Q6) Implement minimum spanning tree using Kruskals algorithm. (Print minimum cost and edges in MST)

```java
import java.util.*;

public class SimpleKruskalMST {
    // Simple Edge class
    static class Edge implements Comparable<Edge> {
        int src, dest, weight;
        
        public Edge(int src, int dest, int weight) {
            this.src = src;
            this.dest = dest;
            this.weight = weight;
        }
        
        @Override
        public int compareTo(Edge other) {
            return this.weight - other.weight;
        }
    }
    
    // Find operation with path compression
    static int find(int[] parent, int i) {
        if (parent[i] != i)
            parent[i] = find(parent, parent[i]);
        return parent[i];
    }
    
    // Union operation
    static void union(int[] parent, int x, int y) {
        parent[find(parent, x)] = find(parent, y);
    }
    
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        
        System.out.print("Enter number of vertices: ");
        int V = scanner.nextInt();
        
        // Input adjacency matrix
        int[][] matrix = new int[V][V];
        System.out.println("Enter the adjacency matrix (use 0 for no edge):");
        for (int i = 0; i < V; i++) {
            for (int j = 0; j < V; j++) {
                matrix[i][j] = scanner.nextInt();
            }
        }
        
        // Create edge list from matrix
        ArrayList<Edge> edges = new ArrayList<>();
        for (int i = 0; i < V; i++) {
            for (int j = i+1; j < V; j++) {
                if (matrix[i][j] != 0) {
                    edges.add(new Edge(i, j, matrix[i][j]));
                }
            }
        }
        
        // Sort edges by weight
        Collections.sort(edges);
        
        // Create parent array for union-find
        int[] parent = new int[V];
        for (int i = 0; i < V; i++) {
            parent[i] = i;
        }
        
        ArrayList<Edge> mst = new ArrayList<>();
        int totalWeight = 0;
        
        // Process edges in sorted order
        for (Edge edge : edges) {
            int rootSrc = find(parent, edge.src);
            int rootDest = find(parent, edge.dest);
            
            // If including this edge doesn't form a cycle
            if (rootSrc != rootDest) {
                mst.add(edge);
                totalWeight += edge.weight;
                union(parent, rootSrc, rootDest);
                
                // Stop if we have V-1 edges
                if (mst.size() == V - 1) {
                    break;
                }
            }
        }
        
        // Print results
        System.out.println("Edges in the Minimum Spanning Tree:");
        for (Edge edge : mst) {
            System.out.println(edge.src + " -- " + edge.dest + " == " + edge.weight);
        }
        System.out.println("Minimum Cost Spanning Tree: " + totalWeight);
        
        scanner.close();
    }
}
```

### Q7) Implement 0/1 Knapsack algorithm (Print length, total profit earned and matrix)

```java
import java.util.ArrayList;
import java.util.Scanner;

public class KnapsackProblem {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        
        // Get knapsack capacity
        System.out.print("Enter the capacity of the knapsack: ");
        int capacity = scanner.nextInt();
        
        // Get number of items
        System.out.print("Enter the number of items: ");
        int n = scanner.nextInt();
        
        int[] weights = new int[n];
        int[] profits = new int[n];
        
        // Get weights of items
        System.out.println("Enter the weights of the items:");
        for (int i = 0; i < n; i++) {
            System.out.print("Weight of item " + (i + 1) + ": ");
            weights[i] = scanner.nextInt();
        }
        
        // Get profits of items
        System.out.println("Enter the profits of the items:");
        for (int i = 0; i < n; i++) {
            System.out.print("Profit of item " + (i + 1) + ": ");
            profits[i] = scanner.nextInt();
        }
        
        // Solve the knapsack problem
        KnapsackResult result = knapsack01(weights, profits, capacity);
        
        // Print capacity
        System.out.println("\nKnapsack Capacity: " + capacity);
        
        // Print maximum profit
        System.out.println("Maximum Profit: " + result.maxProfit);
        
        // Print selected items
        System.out.print("Selected Items (indices): ");
        for (int index : result.selectedItems) {
            System.out.print((index + 1) + " "); // Adding 1 to make it 1-indexed for user
        }
        System.out.println();
        
        System.out.print("Selected Items (weights): ");
        for (int index : result.selectedItems) {
            System.out.print(weights[index] + " ");
        }
        System.out.println();
        
        System.out.print("Selected Items (profits): ");
        for (int index : result.selectedItems) {
            System.out.print(profits[index] + " ");
        }
        System.out.println();
        
        // Print DP matrix
        System.out.println("\nDP Matrix:");
        for (int i = 0; i <= n; i++) {
            for (int w = 0; w <= capacity; w++) {
                System.out.print(result.dpMatrix[i][w] + "\t");
            }
            System.out.println();
        }
        
        scanner.close();
    }
    
    public static KnapsackResult knapsack01(int[] weights, int[] profits, int capacity) {
        int n = weights.length;
        
        // Initialize the DP matrix with 0's
        int[][] dp = new int[n + 1][capacity + 1];
        
        // Fill the DP table
        for (int i = 1; i <= n; i++) {
            for (int w = 0; w <= capacity; w++) {
                // If current item weight is less than or equal to the current capacity
                if (weights[i-1] <= w) {
                    // Take maximum of including or excluding the current item
                    dp[i][w] = Math.max(profits[i-1] + dp[i-1][w-weights[i-1]], dp[i-1][w]);
                } else {
                    // Current item weight exceeds capacity, so exclude it
                    dp[i][w] = dp[i-1][w];
                }
            }
        }
        
        // Determine which items are included in the optimal solution
        ArrayList<Integer> selectedItems = new ArrayList<>();
        int i = n, j = capacity;
        while (i > 0 && j > 0) {
            if (dp[i][j] != dp[i-1][j]) {
                selectedItems.add(0, i-1); // Add at the beginning to maintain order
                j -= weights[i-1];
            }
            i--;
        }
        
        // Create and return the result
        KnapsackResult result = new KnapsackResult();
        result.maxProfit = dp[n][capacity];
        result.selectedItems = selectedItems;
        result.dpMatrix = dp;
        
        return result;
    }
    
    static class KnapsackResult {
        int maxProfit;
        ArrayList<Integer> selectedItems;
        int[][] dpMatrix;
    }
}
```

### Q8) Implement 0/1 Knapsack algorithm (Print length, total profit earned and matrix along with arrows)

```java
import java.util.Scanner;

public class LongestCommonSubsequence {
    
    // Directions for printing arrows
    private static final char DIAGONAL = '↖'; // Diagonal arrow (match)
    private static final char UP = '↑';       // Up arrow
    private static final char LEFT = '←';     // Left arrow
    
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        
        System.out.println("Longest Common Subsequence Implementation");
        System.out.println("----------------------------------------");
        
        // Get input strings
        System.out.print("Enter first string: ");
        String str1 = scanner.nextLine();
        
        System.out.print("Enter second string: ");
        String str2 = scanner.nextLine();
        
        scanner.close();
        
        // Compute LCS
        findLCS(str1, str2);
    }
    
    public static void findLCS(String str1, String str2) {
        int m = str1.length();
        int n = str2.length();
        
        // 2D array to store the lengths of LCS
        int[][] dp = new int[m + 1][n + 1];
        
        // 2D array to store directions for backtracking
        char[][] direction = new char[m + 1][n + 1];
        
        // Fill the dp table
        for (int i = 0; i <= m; i++) {
            for (int j = 0; j <= n; j++) {
                if (i == 0 || j == 0) {
                    dp[i][j] = 0;
                } else if (str1.charAt(i - 1) == str2.charAt(j - 1)) {
                    dp[i][j] = dp[i - 1][j - 1] + 1;
                    direction[i][j] = DIAGONAL;
                } else {
                    if (dp[i - 1][j] >= dp[i][j - 1]) {
                        dp[i][j] = dp[i - 1][j];
                        direction[i][j] = UP;
                    } else {
                        dp[i][j] = dp[i][j - 1];
                        direction[i][j] = LEFT;
                    }
                }
            }
        }
        
        // Print the length of LCS
        System.out.println("\nLength of Longest Common Subsequence: " + dp[m][n]);
        
        // Print the dp matrix with arrows
        printMatrix(dp, direction, str1, str2);
        
        // Print the characters in LCS
        System.out.print("Characters in LCS: ");
        printLCS(direction, str1, m, n);
        System.out.println();
    }
    
    public static void printMatrix(int[][] dp, char[][] direction, String str1, String str2) {
        int m = str1.length();
        int n = str2.length();
        
        System.out.println("\nLCS Matrix with Arrows:");
        
        // Print column headers (second string characters)
        System.out.print("    ");
        System.out.print("  ");
        for (int j = 0; j < n; j++) {
            System.out.print(str2.charAt(j) + "   ");
        }
        System.out.println();
        
        // Print the matrix with row headers (first string characters)
        for (int i = 0; i <= m; i++) {
            if (i == 0) {
                System.out.print("  ");
            } else {
                System.out.print(str1.charAt(i - 1) + " ");
            }
            
            for (int j = 0; j <= n; j++) {
                System.out.print(dp[i][j] + " ");
                if (direction[i][j] != 0) {
                    System.out.print(direction[i][j] + " ");
                } else {
                    System.out.print("  ");
                }
            }
            System.out.println();
        }
        System.out.println();
    }
    
    public static void printLCS(char[][] direction, String str1, int i, int j) {
        StringBuilder lcs = new StringBuilder();
        printLCSRecursive(direction, str1, i, j, lcs);
        System.out.print(lcs.toString());
    }
    
    private static void printLCSRecursive(char[][] direction, String str1, int i, int j, StringBuilder lcs) {
        if (i == 0 || j == 0) {
            return;
        }
        
        if (direction[i][j] == DIAGONAL) {
            printLCSRecursive(direction, str1, i - 1, j - 1, lcs);
            lcs.append(str1.charAt(i - 1));
        } else if (direction[i][j] == UP) {
            printLCSRecursive(direction, str1, i - 1, j, lcs);
        } else {
            printLCSRecursive(direction, str1, i, j - 1, lcs);
        }
    }
}
```

### Q9) Implement the Single Source Shortest Path algorithm using Dijkstra’s Algorithm. Print the final distance vector (D) and predecessor vector (π). Also, display the shortest path from the source to every other vertex.

```java

```

### Q10) Implement the All-Pairs Shortest Path algorithm using Floyd-Warshall. Print the final distance matrix (D) and predecessor matrix (π). Also, display the shortest path between every pair of vertices

```java

```

### Q11) Implement NQueen Probem (Print output in 1D and 2D and print total number of function calls)

```java
import java.util.ArrayList;
import java.util.List;
import java.util.Scanner;

public class NQueensProblem {
    private static int callCount = 0; // Counter for function calls
    private static int solutionCount = 0; // Counter for solutions
    
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.print("Enter the value of N: ");
        int n = scanner.nextInt();
        scanner.close();
        
        if (n <= 0) {
            System.out.println("N should be a positive integer.");
            return;
        }
        
        List<int[]> solutions = new ArrayList<>();
        int[] board = new int[n];
        // Initialize board with -1 indicating no queen placed yet
        for (int i = 0; i < n; i++) {
            board[i] = -1;
        }
        
        findAllSolutions(board, 0, n, solutions);
        
        if (solutions.isEmpty()) {
            System.out.println("\nNo solutions exist for N = " + n);
        } else {
            System.out.println("\nTotal number of solutions for N = " + n + ": " + solutions.size());
            
            // Print all solutions
            for (int i = 0; i < solutions.size(); i++) {
                System.out.println("\nSolution " + (i + 1) + ":");
                printSolution1D(solutions.get(i));
                printSolution2D(solutions.get(i), n);
                System.out.println("-------------------------------");
            }
        }
        
        System.out.println("\nTotal number of calls to queen procedure: " + callCount);
    }
    
    // Recursive function to find all solutions to N Queens problem
    private static void findAllSolutions(int[] board, int row, int n, List<int[]> solutions) {
        callCount++; // Increment call counter
        
        // Base case: All queens are placed
        if (row == n) {
            // Add current solution to the list
            int[] solution = board.clone();
            solutions.add(solution);
            solutionCount++;
            return;
        }
        
        // Try placing the queen in each column of the current row
        for (int col = 0; col < n; col++) {
            if (isSafe(board, row, col, n)) {
                // Place the queen
                board[row] = col;
                
                // Recur to place the rest of the queens
                findAllSolutions(board, row + 1, n, solutions);
                
                // Backtrack
                board[row] = -1;
            }
        }
    }
    
    // Check if it's safe to place a queen at board[row][col]
    private static boolean isSafe(int[] board, int row, int col, int n) {
        // Check for queens in the same column
        for (int i = 0; i < row; i++) {
            if (board[i] == col) {
                return false;
            }
        }
        
        // Check for queens in the upper-left diagonal
        for (int i = row - 1, j = col - 1; i >= 0 && j >= 0; i--, j--) {
            if (board[i] == j) {
                return false;
            }
        }
        
        // Check for queens in the upper-right diagonal
        for (int i = row - 1, j = col + 1; i >= 0 && j < n; i--, j++) {
            if (board[i] == j) {
                return false;
            }
        }
        
        return true;
    }
    
    // Print the board solution in 1D format
    private static void printSolution1D(int[] board) {
        System.out.println("1D Solution (column positions):");
        System.out.print("[");
        for (int i = 0; i < board.length; i++) {
            System.out.print(board[i]);
            if (i < board.length - 1) {
                System.out.print(", ");
            }
        }
        System.out.println("]");
    }
    
    // Print the board solution in 2D format
    private static void printSolution2D(int[] board, int n) {
        System.out.println("2D Solution:");
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                if (board[i] == j) {
                    System.out.print(" Q ");
                } else {
                    System.out.print(" . ");
                }
            }
            System.out.println();
        }
    }
}
```

### Q12) Implement Sum of Subsets Problem (Print total number of function calls)

```java
import java.util.Scanner;

public class SumOfSubsets {
    // Counter for the number of recursive calls
    private static int callCount = 0;

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        
        System.out.print("Enter the number of elements: ");
        int n = scanner.nextInt();
        
        int[] weights = new int[n + 1]; // 1-indexed for easier understanding
        
        System.out.println("Enter the " + n + " elements:");
        for (int i = 1; i <= n; i++) {
            weights[i] = scanner.nextInt();
        }
        
        System.out.print("Enter the target sum: ");
        int targetSum = scanner.nextInt();
        
        // Calculate total sum of all elements
        int totalSum = 0;
        for (int i = 1; i <= n; i++) {
            totalSum += weights[i];
        }
        
        // Reset call counter
        callCount = 0;
        
        // Create array to track which elements are in the solution
        boolean[] included = new boolean[n + 1];
        
        // Start with no elements selected
        System.out.println("\nSubsets with sum equal to " + targetSum + ":");
        sumOfSubsets(0, 0, totalSum, targetSum, weights, included, n);
        
        System.out.println("\nTotal number of calls to Sum of Subset procedure: " + callCount);
        
        scanner.close();
    }
    
    /**
     * Recursive function to find subsets with the given sum
     * @param currentSum - Current sum of selected elements
     * @param currentIndex - Current index being considered
     * @param remainingSum - Sum of remaining elements
     * @param targetSum - Target sum we're looking for
     * @param weights - Array of weights/values
     * @param included - Boolean array to track which elements are included
     * @param n - Total number of elements
     */
    private static void sumOfSubsets(int currentSum, int currentIndex, int remainingSum, 
                                   int targetSum, int[] weights, boolean[] included, int n) {
        // Increment call counter
        callCount++;
        
        // If current sum equals target sum, we found a solution
        if (currentSum == targetSum) {
            printSolution(included, weights, n);
            return;
        }
        
        // If we've gone too far or can't possibly reach the target, backtrack
        if (currentSum > targetSum || currentSum + remainingSum < targetSum) {
            return;
        }
        
        // If we've considered all elements but haven't found a solution, backtrack
        if (currentIndex == n) {
            return;
        }
        
        // Consider the next element
        int nextIndex = currentIndex + 1;
        
        // Include the current element
        included[nextIndex] = true;
        sumOfSubsets(currentSum + weights[nextIndex], nextIndex, 
                   remainingSum - weights[nextIndex], targetSum, weights, included, n);
        
        // Exclude the current element
        included[nextIndex] = false;
        sumOfSubsets(currentSum, nextIndex, 
                   remainingSum - weights[nextIndex], targetSum, weights, included, n);
    }
    
    /**
     * Print the current solution
     */
    private static void printSolution(boolean[] included, int[] weights, int n) {
        System.out.print("{ ");
        for (int i = 1; i <= n; i++) {
            if (included[i]) {
                System.out.print(weights[i] + " ");
            }
        }
        System.out.println("}");
    }
}
```

### Q13) Implement **String Matching Algorithm using KMP Method** (Print all occurrences of string)

```java
import java.util.Scanner;

public class KMPStringMatching {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        
        System.out.println("Enter the text string:");
        String text = scanner.nextLine();
        
        System.out.println("Enter the pattern to search for:");
        String pattern = scanner.nextLine();
        
        findPatternKMP(text, pattern);
        
        scanner.close();
    }
    
    /**
     * KMP algorithm to find all occurrences of pattern in text
     * @param text - The main text to search in
     * @param pattern - The pattern to search for
     */
    private static void findPatternKMP(String text, String pattern) {
        int n = text.length();
        int m = pattern.length();
        
        // Edge cases
        if (m == 0) {
            System.out.println("Pattern is empty!");
            return;
        }
        
        if (n < m) {
            System.out.println("Pattern is longer than text. No matches possible.");
            return;
        }
        
        // Compute the LPS (Longest Prefix Suffix) array
        int[] lps = computeLPSArray(pattern);
        
        // Counters for pattern matching
        int i = 0; // index for text
        int j = 0; // index for pattern
        
        boolean matchFound = false;
        System.out.println("\nOccurrences of the pattern:");
        
        // Search for pattern in text using the LPS array
        while (i < n) {
            // If characters match, move both pointers
            if (pattern.charAt(j) == text.charAt(i)) {
                i++;
                j++;
            }
            
            // If we've matched the entire pattern
            if (j == m) {
                // Pattern found at index i-j
                int position = i - j;
                System.out.println("Pattern found at index " + position);
                matchFound = true;
                
                // Use LPS values to shift the pattern for next search
                j = lps[j - 1];
            } 
            // If there's a mismatch after some matches
            else if (i < n && pattern.charAt(j) != text.charAt(i)) {
                // Use LPS values to skip comparisons
                if (j != 0) {
                    j = lps[j - 1];
                } else {
                    i++;
                }
            }
        }
        
        if (!matchFound) {
            System.out.println("No matches found.");
        }
    }
    
    /**
     * Computes the Longest Prefix Suffix (LPS) array for KMP algorithm
     * @param pattern - The pattern string
     * @return - The LPS array
     */
    private static int[] computeLPSArray(String pattern) {
        int m = pattern.length();
        int[] lps = new int[m];
        
        // Length of the previous longest prefix suffix
        int len = 0;
        int i = 1;
        
        // The first value in LPS is always 0
        lps[0] = 0;
        
        // Calculate LPS[i] for i = 1 to m-1
        while (i < m) {
            if (pattern.charAt(i) == pattern.charAt(len)) {
                len++;
                lps[i] = len;
                i++;
            } else {
                // This is the tricky part
                if (len != 0) {
                    // Use the LPS values calculated so far to find the next match
                    len = lps[len - 1];
                } else {
                    // No match found
                    lps[i] = 0;
                    i++;
                }
            }
        }
        
        return lps;
    }
    
    /**
     * Utility method to print the LPS array (useful for debugging)
     */
    private static void printLPSArray(int[] lps, String pattern) {
        System.out.println("LPS array for pattern \"" + pattern + "\":");
        for (int i = 0; i < lps.length; i++) {
            System.out.println("lps[" + i + "] = " + lps[i] + " (for '" + pattern.charAt(i) + "')");
        }
        System.out.println();
    }
}
```

### Q14) Implement **String Matching Algorithm using Rabin Karp Method** (Print all occurrences of string)

```java
import java.util.Scanner;

public class RabinKarpStringMatching {
    // A large prime number to avoid hash collisions
    private static final int PRIME = 101;
    
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        
        System.out.println("Enter the text string:");
        String text = scanner.nextLine();
        
        System.out.println("Enter the pattern to search for:");
        String pattern = scanner.nextLine();
        
        rabinKarpSearch(text, pattern);
        
        scanner.close();
    }
    
    /**
     * Rabin-Karp algorithm to find all occurrences of pattern in text
     * @param text - The main text to search in
     * @param pattern - The pattern to search for
     */
    private static void rabinKarpSearch(String text, String pattern) {
        int n = text.length();
        int m = pattern.length();
        
        // Edge cases
        if (m == 0) {
            System.out.println("Pattern is empty!");
            return;
        }
        
        if (n < m) {
            System.out.println("Pattern is longer than text. No matches possible.");
            return;
        }
        
        // Base value for rolling hash calculation (can be any number, but prime is good)
        int d = 256; // Number of characters in the input alphabet
        
        // Calculate hash value for pattern and first window of text
        int patternHash = 0;
        int textHash = 0;
        int h = 1;
        
        // Calculate h = d^(m-1) % PRIME
        for (int i = 0; i < m - 1; i++) {
            h = (h * d) % PRIME;
        }
        
        // Calculate initial hash values
        for (int i = 0; i < m; i++) {
            patternHash = (d * patternHash + pattern.charAt(i)) % PRIME;
            textHash = (d * textHash + text.charAt(i)) % PRIME;
        }
        
        boolean matchFound = false;
        System.out.println("\nOccurrences of the pattern:");
        
        // Slide the pattern over text one by one
        for (int i = 0; i <= n - m; i++) {
            // Check if hash values match
            if (patternHash == textHash) {
                // Check for character by character match
                boolean match = true;
                for (int j = 0; j < m; j++) {
                    if (text.charAt(i + j) != pattern.charAt(j)) {
                        match = false;
                        break;
                    }
                }
                
                if (match) {
                    System.out.println("Pattern found at index " + i);
                    matchFound = true;
                }
            }
            
            // Calculate hash value for next window of text
            if (i < n - m) {
                // Remove leading digit, add trailing digit
                textHash = (d * (textHash - text.charAt(i) * h) + text.charAt(i + m)) % PRIME;
                
                // We might get negative value of textHash, converting it to positive
                if (textHash < 0) {
                    textHash += PRIME;
                }
            }
        }
        
        if (!matchFound) {
            System.out.println("No matches found.");
        }
    }
}
```