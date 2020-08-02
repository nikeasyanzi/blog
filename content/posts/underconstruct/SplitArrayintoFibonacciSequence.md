# [3. Array/String](/arraystring.md)
## [842.Split Array into Fibonacci Sequence](https://leetcode.com/problems/split-array-into-fibonacci-sequence/)

```c
class Solution(object):
    def splitIntoFibonacci(self, S):
        for i in range( len(S)-2):
            x = S[:i+1]
            print(x)
            if x != '0' and x.startswith('0'): break
            a = int(x)
            for j in range(i+1,len(S)-1):
                
                y = S[i+1: j+1]
                print("y="+y)
                if y != '0' and y.startswith('0'): break
                b = int(y)
                fib = [a, b]
                k = j + 1
                while k < len(S):
                    nxt = fib[-1] + fib[-2]
                    print(fib[-1], fib[-2],nxt)
                    nxtS = str(nxt)
                    if nxt <= 2**31 - 1 and S[k:].startswith(nxtS):
                        k += len(nxtS)
                        fib.append(nxt)
                    else:
                        break
                else:
                    if len(fib) >= 3:
                        return fib
        return []
```


說明:
這題基本上是切字串



