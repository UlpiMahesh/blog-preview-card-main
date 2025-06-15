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

        # Shrink window if too many distinct elements
        while distinct_count > K:
            freq[A[left]] -= 1
            current_sum -= A[left]
            if freq[A[left]] == 0:
                distinct_count -= 1
            left += 1

        max_sum = max(max_sum, current_sum)

    return max_sum

# Input handling for platform-style input (as shown in the image)
import sys
input = sys.stdin.read

def main():
    data = input().split()
    N = int(data[0])
    K = int(data[1])
    A = list(map(int, data[2:2+N]))
    print(get_max_sum(N, K, A))

if __name__ == "__main__":
    main()