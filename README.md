# LeetCode
力扣
方法一：
class Solution {
    // 动态规划
    // 判断最长回文字符串，在这过程中统计回文字符串的个数
    // 最终再加上 s 中字符的个数
    public int countSubstrings(String s) {
        if (s == null || s.length() == 0) {
            return 0;
        }
        char[] chars = s.toCharArray();
        int sum = 0;
        boolean[][] dp = new boolean[chars.length][chars.length];
        for (int i = 1; i < chars.length; i++) {
            for (int j = 0; j < i; j++) {
                if (chars[j] == chars[i]) {
                    if (i - j < 3) {
                        dp[j][i] = true;
                    } else {
                        dp[j][i] = dp[j + 1][i - 1];
                    }
                }
                if (dp[j][i]) {
                    sum++;
                }
            }
        }
        return sum + chars.length;
    }
}

方法二：暴力破解，一一统计回文字符串个数
class Solution {
    public int countSubstrings(String s) {
        if (s == null || s.length() == 0) {
            return 0;
        }
        char[] chars = s.toCharArray();
        int sum = 0;
        for (int i = 0; i < chars.length; i++) {
            sum++;
            for (int j = i + 1; j < chars.length; j++) {
                if (isTrue(chars, i, j)) {
                    sum++;
                }
            }
        }
        return sum;
    }
    public boolean isTrue(char[] chars, int left, int right) {
        while (left < right) {
            if (chars[left] != chars[right]) {
                return false;
            }
            left++;
            right--;
        }
        return true;
    }
}
