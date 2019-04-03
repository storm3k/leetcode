[TOC]

### 66. Plus One

Given a **non-empty** array of digits representing a non-negative integer, plus one to the integer.

The digits are stored such that the most significant digit is at the head of the list, and each element in the array contain a single digit.

You may assume the integer does not contain any leading zero, except the number 0 itself.

**Example 1:**

```
Input: [1,2,3]
Output: [1,2,4]
Explanation: The array represents the integer 123.
```

**Example 2:**

```
Input: [4,3,2,1]
Output: [4,3,2,2]
Explanation: The array represents the integer 4321.
```



给一个 int 的列表，+1 操作

#### 方法1

思考，9 + 1为 10，需要进位操作；第一位是9，列表需要增加一个元素

直接按照上述操作

```python
class Solution:
    def plusOne(self, digits: List[int]) -> List[int]:
        n = len(digits)
        while n > 0:
            digits[n-1] += 1
            if digits[n-1] == 10:
                digits[n-1] = 0
                n -= 1
            else:
                break

        # 第一位可能是 0
        if digits[0] == 0:
            digits.insert(0, 1)

        return digits
```

评价：

1. 直观的思考
2. 如果是 +2 等操作，需要判断是否大于10
3. 如果列表 允许 0开头，则此代码有 BUG，会将第一个 0 变成 10，修改方法，可以设置一个 flag ，当列表长度和第一个数都达到要求时候，变为1

#### 方法2

```python
class Solution:
    def plusOne(self, digits: List[int]) -> List[int]:
        num = int("".join(map(str, digits))) + 1
        return [int(i) for i in str(num)]
```

解析

* 思路，将列表转化为数字，此处先转换成 str 再执行 join 操作，最后执行 + 1 操作

  * 另外一种方法，乘以10的次幂

    ```python
    num = 0
    for i in range(len(digits)):
    	num += digits[i] * pow(10, (len(digits)-1-i))
    ```

* 直观，执行 + N 操作修改简单



### Pythonic

`"".join(map(str, digits))` 列表 --> 字符串 —— 66

> map 返回的是生成器