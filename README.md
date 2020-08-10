# -CodeVita-2019-Digit-Pairs

def largest(num):
    num_str = str(num)
    i = 9
    while i >= 0:
        if str(i) in num_str:
            return i
        i-= 1
 
    
 
def smallest(num):
    num_str = str(num)
    i = 0
    while i <= 9:
        if str(i) in num_str:
            return i
        i+= 1
 
 
 
def pairs_from(num):
    if num == 2:
        return 1
    if num >= 3:
        return 2
    return 0
 
 
 
 
T = int(input())
 
for case in range(T):
    N = int(input())
    nums = list(map(int, input().split()))
 
    assert(len(nums) == N)
 
    bitscore = [""]*N
 
    for i in range(len(bitscore)):
        curr_score = str(11*largest(nums[i]) + 7*smallest(nums[i]))
        if len(curr_score) > 2:
            curr_score = curr_score[1:]
        bitscore[i] = curr_score
 
    odd_pos_freqs = [0] * 10
    even_pos_freqs = [0] * 10
 
    for i in range(len(bitscore)):
        index = int(bitscore[i][0])
        if (i+1)%2 == 0:
            even_pos_freqs[index]+= 1
        else:
            odd_pos_freqs[index]+= 1
    
    count_pairs = [0]*10
 
    for i in range(10):
        if even_pos_freqs[i] <= 1 and odd_pos_freqs[i] <= 1:
            continue
        count_pairs[i]+= pairs_from(even_pos_freqs[i]) + pairs_from(odd_pos_freqs[i])
        count_pairs[i] = min(2, count_pairs[i])
 
   
    print(sum(count_pairs))
