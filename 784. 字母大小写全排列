# LeetCode
力扣
class Solution {
    // 回溯算法
    // 先将 char[] chars 填满 S 中的字符，然后从最后一个字符开始判断 if 情况
    // 如果为数字则跳过，为字母则需要改变大小写，并且开启另外一个分支
    // 每次开启一个分支，相当于从该字符再次往下重新赋值 chars ，然后再 if 判断
    // 例如 a1b2，假设从 b 开始 if 判断，则改变 b 为 B 然后再给 chars[3] 赋值 2
    // 将 a1B2 加入 list,如果回到 a 位置进行 if 判断，则发现是字母，需要改变大小写
    // 然后重新往下进行 chars 赋值，将最后一个字符 2 赋值后，将 A1b2 加入list
    // 然后再返回来进行 if 判断，2 不是字母跳过，到 b 处，发现是字母，然后改变 b 为大写 B
    // 接着往下赋值 chars[3] = 2，然后将 A1B2 加入 list
    public List<String> list;
    public List<String> letterCasePermutation(String S) {
        list = new ArrayList<>();
        if (S == null) {
            return list;
        }
        char[] chars = new char[S.length()];
        dfs(S, 0, chars);
        return list;
    }
    public void dfs(String S, int start, char[] chars) {
        if (start == S.length()) {
            list.add(new String(chars));
            return;
        }
        chars[start] = S.charAt(start);
        dfs(S, start + 1, chars);
        if (chars[start] >= '0' && chars[start] <= '9') {
            return;
        }
        // 如果当前字符是字母，则开启另外一个分支
        if (chars[start] >= 'A' && chars[start] <= 'Z') {
            chars[start] = (char)(chars[start] + 32);
            dfs(S, start + 1, chars);
        } else {
            chars[start] = (char)(chars[start] - 32);
            dfs(S, start + 1, chars);
        }
    }
}
