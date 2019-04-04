# 2nd week(2019.03.25)
因为迟交作业，做了两个相似的题目，都是关于数组元素去重的问题。
### 1. 算法题目：在一个有序整型数组中，就地（in-place）移除重复元素，返回数组的长度。
``` Java
class Solution {
    public int removeDuplicates(int[] nums) {
        int resultLength = nums.length;
        if (resultLength <= 1)
            return resultLength;
        for (int i = 0; i < resultLength - 1; i++) {
            int index = i;
            while (i < resultLength - 1 && nums[i + 1] == nums[index] && nums[index] != nums[nums.length - 1]) {
                i++;
                resultLength--;
            }
            if(nums[index] == nums[nums.length - 1]) {
                resultLength = index + 1;
                break;
            }
            int end = i;
            i = index;
            while (resultLength > 1 && end > index && end < nums.length - 1) {
                index++;
                end++;
                nums[index] = nums[end];
            }
        }
        return resultLength;
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

> 1. 第一题的解法走入了误区，复杂而且效率低下；
> 2. 第二题参考了第一题的解法，比较容易的给出了答案；
> 3. 缺乏算法的训练，缺乏思考，II型思考太少，处于自己的舒适区时间长了，一定要走出来；

### 2. Review


### 3. Tip


### 4. Share
