# 两数之和 II - 输入有序数组

## 题目描述

给定一个已按照 **升序排列**  的整数数组 `numbers` ，请你从数组中找出两个数满足相加之和等于目标数 `target` 。

函数应该以长度为 `2` 的整数数组的形式返回这两个数的下标值。`numbers` 的下标 **从0开始计数** ，所以答案数组应当满足 `0 <= answer[0] < answer[1] < numbers.length` 。

假设数组中存在且只存在一对符合条件的数字，同时一个数字不能使用两次。

## 示例1:

>### 输入：
>numbers = [2,7,11,15], target = 9
>### 输出：
>[0,1]
>### 解释：
>2 与 7 之和等于目标数 9 。因此 index1 = 1, index2 = 2 。

## 示例2:

>### 输入：
>numbers = [2,3,4], target = 6
>### 输出：
>[0,2]

## 代码：

1.

    public class Solution {
        public int[] TwoSum(int[] numbers, int target) {
            int[] twoSum=new int[2];
            bool loop=true;
            for(int i=0;i<numbers.Length-1&&loop;i++){
                for(int n=i+1;n<numbers.Length;n++){
                    if(numbers[i]+numbers[n]==target){
                        twoSum=[i,n];
                        loop=false;
                        break;
                    }
                }
            }
            return twoSum;
        }
    }

2.

    public class Solution {
        public int[] TwoSum(int[] numbers, int target) {
            int length = numbers.Length;
            for (int i = 0; i < length; i++) {
                int nextIndex = Search(numbers, target - numbers[i], i + 1, length - 1);
                if (nextIndex >= 0) {
                    return new int[]{i, nextIndex};
                }
            }
            return new int[]{-1, -1};
        }

        public int Search(int[] numbers, int target, int low, int high) {
            while (low <= high) {
                int mid = low + (high - low) / 2;
                if (numbers[mid] == target) {
                    return mid;
                } else if (numbers[mid] > target) {
                    high = mid - 1;
                } else {
                    low = mid + 1;
                }
            }
            return -1;
        }
    }

3.

    public class Solution {
        public int[] TwoSum(int[] numbers, int target) {
            int left = 0;
            int right = numbers.Length - 1;

            while (left < right) {
                int sum = numbers[left] + numbers[right];
                if (sum == target) {
                    return new int[] { left, right };
                }
                if (sum < target) {
                    left++;
                } else {
                    right--;
                }
            }

            // 按照题目假设，数组中存在且只存在一对符合条件的数字
            throw new InvalidOperationException("No solution found");
        }
    }


