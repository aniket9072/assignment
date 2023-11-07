import time

def knapsack_01(values, weights, weight_limit):
    n = len(values)
    dp = [[0] * (weight_limit + 1) for _ in range(n + 1)]
    print(dp)
    for i in range(n + 1):
        for w in range(weight_limit + 1):
            if i == 0 or w == 0:
                dp[i][w] = 0
            elif weights[i - 1] <= w:
                dp[i][w] = max(values[i - 1] + dp[i - 1][w - weights[i - 1]], dp[i - 1][w])
            else:
                dp[i][w] = dp[i - 1][w]
            print(dp)

    selected_items = []
    i, w = n, weight_limit
    while i > 0 and w > 0:
        if dp[i][w] != dp[i - 1][w]:
            selected_items.append(i - 1)
            w -= weights[i - 1]
        i -= 1
        print(selected_items)
    selected_items.reverse()
    print(dp)
    return dp[n][weight_limit], selected_items

if __name__ == "__main__":
    n_items = int(input("Enter number of items: "))
    values = []
    weights = []
    for i in range(n_items):
        weight = int(input(f"Enter weight of item: "))
        value = int(input("Enter value of item: "))
        weights.append(weight)
        values.append(value)
    weight_limit = int(input("Enter maximum weight: "))

    start = time.time()
    max_value, selected_items = knapsack_01(values, weights, weight_limit)
    end = time.time()
    print("Maximum value that can be obtained:", max_value)
    print("Selected items:", selected_items)
    print("Time COmplexity: ",end - start)

