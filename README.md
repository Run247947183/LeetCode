# LeetCode
力扣
方法一：
class Solution {
    // 按每一列来计算雨水，求每一列的雨水数
    // 假设当前列为：height[i]，左边最高柱子：maxLeft,右边最高柱子：maxRight
    // 求左边最高柱子和右边最高柱子的最低柱子，Math.min(maxLeft,maxRight) = tmp
    // 第一种：height[i] < tmp；则可以接到雨水，tmp - height[i]
    // 第二种：height[i] = tmp; 则可以接到雨水为 0
    // 第三种：height[i] < tmp; 则可以接到雨水为 0
    public int trap(int[] height) {
        if (height.length < 3) {
            return 0;
        }
        int sum = 0;
        for (int i = 1; i < height.length - 1; i++) {
            int maxLeft = 0;
            // 找出 height[i] 左边最高的柱子
            for (int j = 0; j < i; j++) {
                maxLeft = Math.max(maxLeft, height[j]);
            }
            int maxRight = 0;
            // 找出 height[i] 右边最高的柱子
            for (int j = i + 1; j < height.length; j++) {
                maxRight = Math.max(maxRight, height[j]);
            }
            int tmp = Math.min(maxLeft, maxRight);
            // 只有 tmp > height[i] 时，才能接到雨水
            if (tmp > height[i]) {
                sum += tmp - height[i];
            }
        }
        return sum;
    }
}

方法二：在方法一的基础上进行改进，每一次都要求 height[i] 的左边和右边的最高柱子
通过动态规划，来求左边和右边的最高柱子，这样就不需要每一次都重新求最高柱子
class Solution {
    // 注意：每次计算左边或者右边的最高柱子时，都不包括自己
    // 所以移动后，才会 dp[i - 1] 和 height[i - 1] 判断
    public int trap(int[] height) {
        if (height.length < 3) {
            return 0;
        }
        int[] dpLeft = new int[height.length];
        int[] dpRight = new int[height.length];
        for (int i = 1; i < height.length; i++) {
            dpLeft[i] = Math.max(dpLeft[i - 1], height[i - 1]);
        }
        for (int i = height.length - 2; i >= 0; i--) {
            dpRight[i] = Math.max(dpRight[i + 1], height[i + 1]);
        }
        int sum = 0;
        for (int i = 1; i < height.length - 1; i++) {
            int tmp = Math.min(dpLeft[i], dpRight[i]);
            if (tmp > height[i]) {
                sum += tmp - height[i];
            }
        }
        return sum;
    }
}
