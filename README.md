from collections import defaultdict

def get_max_sum(N, K, A):
    max_sum = 0
    current_sum = 0
    left = 0
    freq = defaultdict(int)
    distinct = 0

    for right in range(N):
        val = A[right]
        freq[val] += 1
        if freq[val] == 1:
            distinct += 1
        current_sum += val

        # Shrink window if too many distincts
        while distinct > K:
            freq[A[left]] -= 1
            current_sum -= A[left]
            if freq[A[left]] == 0:
                distinct -= 1
            left += 1

        # If sum is negative, drop the window
        if current_sum < 0:
            freq.clear()
            distinct = 0
            current_sum = 0
            left = right + 1
        else:
            max_sum = max(max_sum, current_sum)

    return max_sum

# Test
N = 5
K = 5
A = [-1, 1, 3, 2, -1]
print(get_max_sum(N, K, A))  # ✅ Output: 6