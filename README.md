from collections import defaultdict

def max_sum_good_subarray(arr, k):
    n = len(arr)
    start = 0
    max_sum = 0
    current_sum = 0
    freq = defaultdict(int)

    for end in range(n):
        freq[arr[end]] += 1
        current_sum += arr[end]

       
        while len(freq) > k:
            freq[arr[start]] -= 1
            current_sum -= arr[start]
            if freq[arr[start]] == 0:
                del freq[arr[start]]
            start += 1

        max_sum = max(max_sum, current_sum)

    return max_sum