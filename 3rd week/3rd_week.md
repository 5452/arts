# 3rd week(2019.04.05)
### 1. 算法题目：反转整数，给定一个整型的值，返回它的反转后的值，如果溢出则返回0。
##### Example 1

> * input：123
> * output：321

##### Example 2

> * input: -123
> * output: -321

##### Example 2

> * input: 120
> * output: 21

``` Java
class Solution {
    public int reverse(int x) {
        if(x == 0 || -10 < x && x < 10)
            return x;
        StringBuilder builder = new StringBuilder();
        long l = (long)x;
        String s = String.valueOf(Math.abs(l));
        for (int j = s.length() - 1; j >= 0; j--) {
            builder.append(s.charAt(j));
        }
        builder.toString();
        if (x < 0) {
            l = -1 * Long.parseLong(builder.toString());
            x = l < Integer.MIN_VALUE ? 0 : (int)l;
        } else {
            l = Long.parseLong(builder.toString());
            x = l > Integer.MAX_VALUE ? 0 : (int)l;
        }
        return x;    
    }
}
```
### 2. 同样的有序数组，去重的条件是相同元素不能出现超过两次。
#### 例1:
> 给出数组：nums = [1,1,1,2,2,3],
> 应该给出返回值为 5，并且数组的前五的元素为：1, 1, 2, 2, 3,
> 剩余元素的排列和数量不做要求；

``` Java
public int removeTriples(int[] nums) {
        if (nums.length <= 2) return nums.length;
        int i = 0;
        for (int j = 1; j < nums.length; j++) {
            if (nums[j] != nums[i]) {
                i++;
                nums[i] = nums[j];
            } else if(i == 0 || nums[j] != nums[i - 1]) {
                i++;
                nums[i] = nums[j];
            }        
        }
        return i + 1;
    }
```

### 2. Review


### 3. Tip


### 4. Share
