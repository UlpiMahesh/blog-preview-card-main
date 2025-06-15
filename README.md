for right in range(N):
    val = A[right]
    freq[val] += 1
    if freq[val] == 1:
        distinct_count += 1
    current_sum += val

    while distinct_count > K:
        freq[A[left]] -= 1
        current_sum -= A[left]
        if freq[A[left]] == 0:
            distinct_count -= 1
        left += 1

    # This line must be inside the main loop, after the while
    max_sum = max(max_sum, current_sum)