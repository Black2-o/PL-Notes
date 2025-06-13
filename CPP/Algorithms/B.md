# Greedy Algorithm Notes

## Introduction
Greedy algorithms make locally optimal choices at each step to reach the global optimum. These approaches are often used in problems related to optimization, scheduling, and resource allocation.

## Strategies for Solving Greedy Problems
1. **Sort the input if necessary** – Many greedy problems require sorting elements first.
2. **Use a greedy selection criterion** – Determine what makes an optimal choice at each step.
3. **Use two pointers if applicable** – This is useful for interval problems, pairing, or merging.
4. **Check problem constraints** – Some problems require additional checks to ensure the greedy approach is valid.
5. **Use prefix sums or tracking variables** – Helps maintain intermediate values efficiently.

## Example: Two Pointers Approach
### Problem Statement:
You have two sorted arrays of numbers. You need to find pairs whose sum is closest to a given target value.

### Solution Using Two Pointers:
```cpp
#include <iostream>
using namespace std;

void findClosestPair(int arr1[], int n, int arr2[], int m, int target) {
    int left = 0, right = m - 1;
    int closestSum = 1e9;
    int bestA = -1, bestB = -1;

    while (left < n && right >= 0) {
        int sum = arr1[left] + arr2[right];
        if (abs(target - sum) < abs(target - closestSum)) {
            closestSum = sum;
            bestA = arr1[left];
            bestB = arr2[right];
        }
        if (sum < target) left++; // Move left pointer forward
        else right--; // Move right pointer backward
    }
    cout << "Closest Pair: " << bestA << ", " << bestB << endl;
}

int main() {
    int arr1[] = {1, 4, 7, 10};
    int arr2[] = {2, 5, 8, 11};
    int target = 13;
    findClosestPair(arr1, 4, arr2, 4, target);
    return 0;
}
```
### Explanation:
1. Start with one pointer at the beginning of the first array and the other at the end of the second array.
2. Adjust pointers based on the sum compared to the target.
3. Track the closest sum found and update when necessary.

## Common Contest Scenarios Where Greedy Works Well
1. **Interval Scheduling** – Sorting events and selecting non-overlapping ones greedily.
2. **Activity Selection** – Picking the earliest finishing activity first.
3. **Minimum Coins for Change** – Using the highest denomination first (if allowed).
4. **Task Scheduling with Deadlines** – Assign tasks to maximize efficiency.
5. **Merging Intervals** – Using sorting and two pointers to efficiently merge overlapping intervals.

## Final Tips for Contest Success
- Always **think about sorting first** – Many greedy problems benefit from sorted data.
- Consider using **two pointers** when dealing with pairs, ranges, or merging.
- Always **validate the greedy choice** – Check if a counterexample exists.
- If greedy fails, consider **dynamic programming** as an alternative.

By mastering these strategies and practicing problems, you'll improve your problem-solving skills for competitive programming! 🚀

