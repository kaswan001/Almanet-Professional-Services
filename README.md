### Greedy Algorithm: 

## Subheader......
.........
A **Greedy Algorithm** is an algorithmic approach used to solve optimization problems by choosing the locally optimal solution at each step, with the hope that these local choices will lead to a globally optimal solution. It is often applied in problems where we need to maximize or minimize some value or find a subset of items that satisfies a particular condition.

### Greedy Algorithm Strategy:
The greedy strategy works in stages, making one decision at a time based on the current state of the problem, and once a choice is made, it cannot be undone. The decisions made in each step must meet two key properties:

1. **Greedy Choice Property**: A global (overall) optimal solution can be arrived at by choosing the best local option at every step.
2. **Optimal Substructure**: A problem exhibits optimal substructure if an optimal solution to the problem contains an optimal solution to its sub-problems. In other words, solutions to smaller parts of the problem can be used to construct the overall solution.

### How Greedy Algorithms Work:
1. **Start** with an empty solution set.
2. **Select** the best (local optimal) solution according to a certain criterion.
3. **Add** the selected solution to the overall solution.
4. **Repeat** the process until you either find the solution or exhaust all possibilities.
   
In some problems, the greedy approach works perfectly (e.g., finding the minimum spanning tree, Huffman coding), while in others it can lead to sub-optimal solutions. Therefore, it is crucial to verify whether a greedy approach will provide an optimal solution for a particular problem.

### Key Components:
1. **Candidate Set**: The possible choices or options to consider.
2. **Selection Criteria**: The logic that chooses the best candidate based on the problem's needs.
3. **Feasibility Check**: After each choice, check if the current selection is valid or fits within the problem constraints.
4. **Solution**: Once all choices are made, ensure that the solution meets the problem's requirements.

### Common Examples of Greedy Algorithms:
Here are some well-known problems that can be solved using a greedy approach:

1. **Activity Selection Problem**: Selecting the maximum number of activities that don't overlap.
2. **Fractional Knapsack Problem**: Maximizing the value of items placed in a knapsack with limited capacity, where items can be broken into fractions.
3. **Huffman Coding**: Minimizing the average length of code words when compressing data.
4. **Prim’s Algorithm**: Finding the minimum spanning tree in a graph.
5. **Kruskal’s Algorithm**: Another way to find the minimum spanning tree of a graph.
6. **Dijkstra’s Algorithm**: Finding the shortest path from a single source to all other vertices in a graph.

### Properties of Problems Suited for Greedy Algorithms:
- **Greedy Choice Property**: The problem allows making a locally optimal choice at each step that leads to a global optimal solution.
- **Optimal Substructure**: The problem can be divided into sub-problems, and solutions to these sub-problems lead to an overall optimal solution.

### Example Problem: Fractional Knapsack
This is a classical example where the greedy approach works perfectly.

#### Problem Statement:
You have a knapsack with a capacity \(W\) and \(n\) items, each with a weight \(w_i\) and a value \(v_i\). The goal is to maximize the total value placed in the knapsack, but unlike the 0/1 knapsack problem, you can take fractions of an item. The objective is to select items or parts of items such that their combined weight does not exceed \(W\) and their value is maximized.

#### Greedy Approach:
1. Compute the value-to-weight ratio for each item.
2. Sort the items based on this ratio in decreasing order.
3. Start adding items to the knapsack, taking as much as possible of each item (preferably in full), starting with the item with the highest value-to-weight ratio.
4. If adding the entire item exceeds the knapsack's capacity, take the fraction that fits.

#### Time Complexity:
- Sorting the items by value-to-weight ratio: **O(n log n)**
- Adding items to the knapsack: **O(n)**
- Overall time complexity: **O(n log n)**

#### Java Program to Implement Fractional Knapsack:

```java
import java.util.Arrays;
import java.util.Comparator;

class Item {
    int value, weight;

    // Constructor
    public Item(int value, int weight) {
        this.value = value;
        this.weight = weight;
    }
}

public class FractionalKnapsack {

    // Function to get maximum value in knapsack capacity
    public static double getMaxValue(int capacity, Item[] items) {
        // Sort items by value/weight ratio
        Arrays.sort(items, Comparator.comparingDouble(i -> -((double) i.value / i.weight)));

        double totalValue = 0.0;

        for (Item item : items) {
            // If the item can be added fully
            if (capacity >= item.weight) {
                capacity -= item.weight;
                totalValue += item.value;
            } else {
                // If we can only take a fraction of the item
                totalValue += (double) item.value * ((double) capacity / item.weight);
                break;  // Knapsack is full
            }
        }

        return totalValue;
    }

    public static void main(String[] args) {
        Item[] items = {
            new Item(60, 10),
            new Item(100, 20),
            new Item(120, 30)
        };
        int capacity = 50;

        System.out.println("Maximum value in Knapsack: " + getMaxValue(capacity, items));
    }
}
```

#### Explanation:
1. **Input**: An array of items with weights and values.
2. **Sorting**: The items are sorted based on their value-to-weight ratio.
3. **Selection**: Add full items to the knapsack until it becomes full. If a full item cannot fit, a fraction of the item is added to maximize the value.
4. **Output**: The maximum value that can be carried in the knapsack.

#### Output:
```
Maximum value in Knapsack: 240.0
```

### Greedy vs Other Algorithms:
- **Dynamic Programming (DP)**: DP algorithms store solutions to sub-problems and reuse them, ensuring an optimal solution. While DP guarantees optimal solutions, it can be slower than greedy algorithms in terms of time and space complexity.
- **Backtracking**: Greedy algorithms commit to choices, while backtracking explores all possible choices and backtracks if a choice leads to a suboptimal solution.

### Advantages of Greedy Algorithms:
- **Efficiency**: Greedy algorithms tend to have lower time and space complexity compared to dynamic programming and other exhaustive search methods.
- **Simple to Implement**: Often, greedy algorithms are straightforward to implement, requiring less code than more complex approaches like dynamic programming.

### Disadvantages:
- **Non-Optimal Solutions**: Not all problems can be solved optimally by greedy algorithms. It’s crucial to analyze whether the greedy choice property holds for the problem.
- **Limited Use**: Greedy algorithms are not suitable for problems where local choices do not lead to a global optimum.

### Conclusion:
Greedy algorithms are a powerful tool when solving optimization problems where the local optimal solution at each step leads to the global optimal solution. However, they should be applied with caution, and their effectiveness should be proven either by mathematical reasoning or by analyzing specific problem properties.
