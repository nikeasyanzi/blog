

# [10.Dynamic Programming](/dynamic-programming.md)

## 837. New 21 Game

    Alice plays the following game, loosely based on the card game "21".
    
    Alice starts with 0 points, and draws numbers while she has less than K points.  During each draw, she gains an integer number of points randomly from the range [1, W], where W is an integer.  Each draw is independent and the outcomes have equal probabilities.
    
    Alice stops drawing numbers when she gets K or more points.  What is the probability that she has N or less points?
    
    Example 1:
    
    Input: N = 10, K = 1, W = 10
    Output: 1.00000
    Explanation:  Alice gets a single card, then stops.
    Example 2:
    
    Input: N = 6, K = 1, W = 10
    Output: 0.60000
    Explanation:  Alice gets a single card, then stops.
    In 6 out of W = 10 possibilities, she is at or below N = 6 points.
    Example 3:
    
    Input: N = 21, K = 17, W = 10
    Output: 0.73278
    Note:
    
    0 <= K <= N <= 10000
    1 <= W <= 10000
    Answers will be accepted as correct if they are within 10^-5 of the correct answer.
    The judging time limit has been reduced for this question.


https://leetcode.com/problems/new-21-game/description/

    Intuition:
    The same problems as "Climbing Stairs".
    
    Explanation:
    In a word,
    dp[i]: probability of get points i
    dp[i] = sum(last W dp values) / W
    
    Time Complexity:
    O(N)
    
```c
def new21Game(self, N, K, W):
if K == 0 or N >= K + W: return 1
dp = [1.0] + [0.0] * N
Wsum = 1.0
for i in range(1, N + 1):
dp[i] = Wsum / W
if i < K: Wsum += dp[i]
if i - W >= 0: Wsum -= dp[i - W]
return sum(dp[K:])
```

precisely, I wanted to understand the 3rd example of N=21, K=17, W=10
For this case, could you help visualize, how the DP list builds up, so that the last 5 gives the result ?
Could you please tell if my understanding of the below is correct?
Case: N=3, K=1, W=10
i=1 (drawn card-1) : You win as you get 1(1<=N), P(i=1)=1/10=0.1
i=2 (drawn card-2) : You win as you get 2(2<=N), P(i=2)=1/10=0.1
i=3 (drawn card-3) : You win as you get 3(3<=N), P(i=3)=1/10=0.1
All events are independent: Total prob = 0.1+0.1+0.1 = 0.3
Case: N=3, K=2, W=10
i=1 (draw 1) P(draw=1)=0.1 [call this A], Same event, we do not stop now we can draw either 1 or 2 , as i<K, for drawing 1 or 2 , P(1 or 2)=0.1+0.1=0.2 [call this B], P(complete draw) = P(A)*P(B)=0.1*0.2 = 0.02
i=2 (drawn card-2) : You win as you get 2(2<=N) and you stop as 2>=K, P(i=2)=1/10=0.1
i=3 (drawn card-3) : You win as you get 3(3<=N) and you stop as 2>=K, P(i=3)=1/10=0.1
All events are independent: Total prob = 0.02+0.1+0.1 = 0.22
In Python code instead of adding dp[i] += Wsum / W you can just assign value dp[i] = Wsum / W
You can also start with only one item in the list dp = [1.0] and extend it by appending items as you go: dp.append(Wsum / W)

```c
class Solution:
    def new21Game(self, N, K, W):
        if N < K:
            return 0.0
        if K == 0 or N >= K - 1 + W:
            return 1.0
        dp = [1.0]  // no matter how much points we get, we stop
        Wsum = dp[0]
        for i in range(1, N + 1):
            p = Wsum / W
            dp.append(p)
        if i < K:
            Wsum += p
        if i - W >= 0:  ///
            Wsum -= dp[i - W]
    return sum(dp[K:])
```

The solution can be further optimized in memory size as O(min(K, N, W)) by using a cyclic buffer for dp to keep no more than W last values.


舉例

N=6, K=2, W=10

1st draw | probability|
---|---|
 1 |      -> we can have 1,2,3,4,5 in the next draw -> probability = 1/10 * (1/10*5)
 2 |     -> we stop -> probability= 1/10 
 3 |      -> 1/10
 4 |
 5 |
 6 |
 
i= 1 wsum= 1.0
[1.0, 0.1]
i= 2 wsum= 1.1
[1.0, 0.1, 0.11000000000000001]
i= 3 wsum= 1.1
[1.0, 0.1, 0.11000000000000001, 0.11000000000000001]
i= 4 wsum= 1.1
[1.0, 0.1, 0.11000000000000001, 0.11000000000000001, 0.11000000000000001]
i= 5 wsum= 1.1
[1.0, 0.1, 0.11000000000000001, 0.11000000000000001, 0.11000000000000001, 0.11000000000000001]
i= 6 wsum= 1.1
[1.0, 0.1, 0.11000000000000001, 0.11000000000000001, 0.11000000000000001, 0.11000000000000001, 0.11000000000000001]

N=4, K=4, W=3

1st draw | 2st draw | probability|
---|---|
 1 |   1,2,3 |   -> we can have 3, in 2nd draw -> probability = 1/3 * (1/3)
 2 |   1,2,3 | -> 2 we stop -> probability= 1/3 
 3 |   1,2,3 |  -> 1 1/10

i= 1 wsum= 1.0
[1.0, 0.3333333333333333]
i= 2 wsum= 1.3333333333333333
[1.0, 0.3333333333333333, 0.4444444444444444]
i= 3 wsum= 1.7777777777777777
[1.0, 0.3333333333333333, 0.4444444444444444, 0.5925925925925926]
i= 4 wsum= 1.3703703703703702
[1.0, 0.3333333333333333, 0.4444444444444444, 0.5925925925925926, 0.4567901234567901]
 
0.45679
