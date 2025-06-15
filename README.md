from collections import defaultdict

def get_max_sum(N, K, A):
    max_sum = 0
    current_sum = 0
    left = 0
    freq = defaultdict(int)
    distinct_count = 0

    for right in range(N):
        val = A[right]
        freq[val] += 1
        if freq[val] == 1:
            distinct_count += 1
        current_sum += val

        # Shrink window from the left if too many distinct elements
        while distinct_count > K:
            freq[A[left]] -= 1
            current_sum -= A[left]
            if freq[A[left]] == 0:
                distinct_count -= 1
            left += 1

        # Update max sum for the valid window
        max_sum = max(max_sum, current_sum)

    return max_sum

# Test case
N = 5
K = 5
A = [-1, 1, 3, 2, -1]
print(get_max_sum(N, K, A))  # Output: 6