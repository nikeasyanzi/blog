# [2.Math](/math.md)

914.X of a Kind in a Deck of Cards

[https://leetcode.com/problems/x-of-a-kind-in-a-deck-of-cards/](https://leetcode.com/problems/x-of-a-kind-in-a-deck-of-cards/)

```py
import functools

class Solution:
    def hasGroupsSizeX(self, deck):
        """
        :type deck: List[int]
        :rtype: bool
        """
        def gcd(a, b):
            while b: a, b = b, a % b
            return a
        count = collections.Counter(deck).values();
        #print(count)

        if functools.reduce (gcd,count)>1:
                return True;
        return False;
```

這題 你要思考幾件事

1. 本來以為是要找偶數次數   但 這種 ex. {1,1,1,2,2,2} -&gt; \[1,1,1\] \[2,2,2\] 就不行
2. 主要是計算各數字 出現的次數, 再求這些數的公因數 

假設次數分別是$$a_{1},a_{2},...,a_{n}$$

問題是有必要先排序?

先從$$min(a_{1},a_{2},...,a_{n})$$ 開始找公因數嗎?

答案是**不用**

為什麼

假設 排序由大到小後  還是$$a_{1},a_{2},...,a_{n}$$好了

那 假設答案存在 , 則 $$a_{1}$$ 一定會是$$gcd(a_{n},a_{n-1})$$的因數



心得:

GCD, LCS 這種一定要背熟 

