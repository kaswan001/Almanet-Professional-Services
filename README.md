### Greedy Algorithm Explanation

The **Greedy Algorithm** is a problem-solving approach that makes a series of choices, each of which looks best at the moment. It selects the best option available at every step, hoping that the global optimum can be achieved by selecting local optima. This approach works well for problems where a globally optimal solution can be arrived at by making locally optimal choices.

#### Key Characteristics:
- **Greedy Choice Property**: A global optimal solution can be arrived at by selecting the locally optimal choices.
- **Optimal Substructure**: The problem can be broken down into smaller subproblems, and an optimal solution to the problem contains optimal solutions to these subproblems.

#### Examples of Problems:
- **Activity Selection Problem**: Choose the maximum number of activities that don't overlap.
- **Fractional Knapsack Problem**: Fill a knapsack to maximize its total value.
- **Huffman Coding**: Minimize the average length of codes used to represent a set of characters.

### Time Complexity
The time complexity of a greedy algorithm depends on the specific problem. Typically, it involves sorting the input data or making a series of decisions, so the time complexity could be \(O(n \log n)\) if sorting is involved, or \(O(n)\) if no sorting is required.

### Java Program Example: Fractional Knapsack Problem

The Fractional Knapsack Problem is a classic example of a greedy algorithm. Here, you have a knapsack with a maximum weight capacity, and you need to maximize the total value of items in the knapsack. You can take fractions of an item if taking the whole item exceeds the knapsack's capacity.

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

    // Function to get maximum value in the knapsack
    private static double getMaxValue(int capacity, Item[] items) {
        // Sort items by value/weight ratio in descending order
        Arrays.sort(items, new Comparator<Item>() {
            @Override
            public int compare(Item o1, Item o2) {
                double r1 = (double) o1.value / o1.weight;
                double r2 = (double) o2.value / o2.weight;
                return Double.compare(r2, r1);
            }
        });

        int currentWeight = 0;
        double finalValue = 0.0;

        // Loop through the items
        for (Item item : items) {
            if (currentWeight + item.weight <= capacity) {
                // Take the whole item
                currentWeight += item.weight;
                finalValue += item.value;
            } else {
                // Take the fraction of the remaining weight
                int remainingWeight = capacity - currentWeight;
                finalValue += item.value * ((double) remainingWeight / item.weight);
                break;
            }
        }

        return finalValue;
    }

    public static void main(String[] args) {
        Item[] items = {
            new Item(60, 10),
            new Item(100, 20),
            new Item(120, 30)
        };
        int capacity = 50;

        double maxValue = getMaxValue(capacity, items);
        System.out.println("Maximum value we can obtain = " + maxValue);
    }
}
```

### Explanation:
- **Input**: Three items with values {60, 100, 120} and weights {10, 20, 30}. The knapsack capacity is 50.
- **Output**: The program will output the maximum value that can be obtained, which is `240.0`.

### Time Complexity:
- Sorting the items based on their value-to-weight ratio takes \(O(n \log n)\).
- The iteration over the items to fill the knapsack takes \(O(n)\).
- So, the overall time complexity is \(O(n \log n)\).
