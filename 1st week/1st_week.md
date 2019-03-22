# 1st week(2019.03.18)
### 1. 算法题目：在一个整型数组中，找出两个相加等于给定结果值的两个元素，返回他们的索引。（假定只存在一组符合条件的组合，并且数组元素不可以重复使用）
##### 思路步骤：
1. 感觉如果是一个有序数组，解决的方式会比较简单和直接，所以就考虑首先进行排序。
2. 假设数组排序后为降序，则可以如下方式解决：从数组两端元素开始相加计算，也就是数组中最大值和最小值相加。

> ###### a. 如果结果小于给定结果值，则用次最小值与最大值相加，以此类推，直到找到符合条件的组合或循环终止返回；
###### b. 如果结果大于给定结果值，则用次最大值与最小值相加，以此类推，直到找到符合条件的组合或循环终止返回；

``` Java
class Solution {
    public static int[] twoSum(int[] nums, int target) {
        int[] original = nums.clone();
        int[] result = new int[2];
        quickSort(nums, 0, nums.length - 1);
        int smaller = 0;
        int bigger = nums.length - 1;
        for(; smaller < bigger;) {
            if(nums[smaller] + nums[bigger] > target)
                bigger--;
            else if(nums[smaller] + nums[bigger] < target)
                smaller++;
            else 
                break;
        }
        boolean firstSeted = false;
        boolean secondSeted = false;
        for (int i = 0; i < original.length; i++) {
            if (original[i] == nums[smaller] && !firstSeted) {
                result[0] = i;
                firstSeted = true;
            } else if (original[i] == nums[bigger] && !secondSeted) {
                result[1] = i;
                secondSeted = true;
            }
        }
        return result;
    }
    
    public static void quickSort(int[] nums, int start, int end) {
        if(start < end) {
            int index = partition(nums, start, end);
            quickSort(nums, start, index - 1);
            quickSort(nums, index + 1, end);
        }
        
    }
    
    public static int partition(int[] nums, int start, int end) {
        int index = start;
        int pivot = nums[index];
        while(index < end) {
            while(index < end && nums[end] > pivot) {
                end--;
            }
            nums[index] = nums[end];
            while(index < end && nums[index] <= pivot) {
                index++;
            }
            nums[end] = nums[index];
        }
        nums[index] = pivot;
        return index;
    }
}
```

需要注意的点是如果存在相同值的元素，而且相同值的元素恰好就是答案，需要进行判断。
> 我开始审题错误，误以为数组不含重复元素，结果没有通过测试。

### 2. Review
[Goodbye, Object Oriented Programming](https://medium.com/@cscalfani/goodbye-object-oriented-programming-a59cda4c0e53)
##### 读后感：
文章说的第一个关于继承的问题其实之前在不同的文章和书籍中看到过不止一次了，记得四人帮的《设计模式》中也提到了用组合替代继承的方法。当然本处的继承指的是类的继承，而非接口的继承。继承在某种程度上可以说是耦合的，对于松散耦合的原则是有破坏的，但是我觉得内聚和耦合在一定层次上是有关系的，一个模块有高内聚性，内部的设计必定是有互相联系的，换句话说，就是耦合的。所以对于很多的特性或架构模式会有争论，归根结底是要根据具体应用场景的，没有不合适的特性，只用不合适的场景。另外，作为技术人员，对于技术架构和语言应该保持中立的态度，开放的心态，在纵向为主的技术提升中，会不自觉的有一定的横向拓展，提升自己的维度后，就会自然的根据具体问题去给出合适的解法，不然如果某一方面研究很深但横向广度不够，或者体系不健全，也许会对于擅长的技术有滥用的倾向，说的严重一些，可能手里拿着锤子，眼里看到的都是钉子。

> 技术人或多或少都会有这方面的问题。我自己也有。
> 保持自省，开放心态，养成思考归纳的习惯。

### 3. Tip
这个最近没什么特别的，问题倒是遇到了：Jenkins 权限管理不严，防护不够，被人种了挖矿木马，因为 Jenkins 服务器的 ssh pub key 添加到了另外两台服务器，共三台中了招。
#### 具体表现：
1. 正常命令被拦截替换，比如 netstat；
2. crond 被添加不明定时任务，删除后重复出现；
3. 伪装系统服务添加，删除后重复出现；
4. 在 /etc/init.d/rc*.d/ 目录中出现很多 S99 开头的启动脚本；
5. /usr/bin/ 下出现不明可执行程序，删除后重复出现；
6. /tmp 目录下出现不明可执行程序，删除后重复出现；

> 目前依旧在挣扎处理中。

### 4. Share
 
