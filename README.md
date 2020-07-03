# LeetCode
力扣
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode[] listOfDepth(TreeNode tree) {
        if (tree == null) {
            return null;
        }
        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(tree);
        List<ListNode> res = new ArrayList<>();
        while (!queue.isEmpty()) {
            int size = queue.size();
            ListNode head = new ListNode(-1);
            ListNode tail = head;
            while (size > 0) {
                size--;
                TreeNode cur = queue.poll();
                tail.next = new ListNode(cur.val);
                tail = tail.next;
                if (cur.left != null) {
                    queue.offer(cur.left);
                }
                if (cur.right != null) {
                    queue.offer(cur.right);
                }
            }
            res.add(head.next);
        }
        ListNode[] ln = new ListNode[res.size()];
        for (int i = 0; i < res.size(); i++) {
            ln[i] = res.get(i);
        }
        return ln;
    }
}
