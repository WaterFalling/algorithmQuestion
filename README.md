# 剑指 offer 算法题

### 二维数组中的查找

#### 描述：在一个二维数组中（每个一维数组的长度相同），每一行都按照从左到右递增的顺序排序，每一列都按照从上到下递增的顺序排序。请完成一个函数，输入这样的一个二维数组和一个整数，判断数组中是否含有该整数。

+ 暴力法

```java
public class Solution{
    public boolean Find(int target, int[][] array){
        for(int i = 0; i < array.length; i++){
            for(int j = 0; j < array[0].length; j++){
                if(array[i][j] == target){
                    return true;
                }
            }
        }
        return false;
    }
}
```

+ 从左下找

```java
public class Solution{
    public boolean Find(int target, int[][] array){
        int rows = array.length;
        if(rows == 0){
            return false;
        }
        int cols = array[0].length;
        if(cols == 0){
            return false;
        }
        int row = rows - 1;
        int col = 0;
        while(row >= 0 && col < cols){
            if(array[row][col] < target){
                col++;
            }else if(array[row][col] > target){
                row--;
            }else{
                return true;
            }
        }
        return false;
    }
}
```

### 替换空格

#### 描述：请实现一个函数，将一个字符串中的每个空格替换成“%20”。例如，当字符串为We Are Happy.则经过替换之后的字符串为We%20Are%20Happy。

+ 调用自带函数

```java
public class Solution{
    public String replaceSpace(StringBuffer str){
        return str.toString().replace(" ", "%20");
    }
}
```

+ 用新的数组存

```java
import java.util.*;
public class Solution{
    public String replaceSpace(StringBuffer str){
        StringBuilder sb = new StringBuilder();
        for(int i = 0; i < str.length(); i++){
            char c = str.charAt(i);
            if(c == ' '){
                sb.append("%20");
            }else{
                sb.append(c);
            }
        }
        return sb.toString();
    }
}
```

### 从尾到头打印链表

#### 描述：输入一个链表，按链表从尾到头的顺序返回一个ArrayList

+ 递归

```java
import java.uitl.*;
public class Solution{
    Array<Integer> list = new ArrayList<>();
    public ArrayList<Integer> printListFromTailToHead(ListNode listNode) {
    	if(listNode != null){
            printListFromTailToHead(listNode.next);
            list.add(listNode.val);
        }
        return list;
    }
}
```

+ 非递归

```java
import java.util.*;
public class Solution {
    public ArrayList<Integer> printListFromTailToHead(ListNode listNode) {
        ArrayList<Integer> list = new ArrayList<>();
        ListNode tmp = listNode;
        while(tmp!=null){
            list.add(0,tmp.val);
            tmp = tmp.next;
        }
        return list;
    }
}
```

### 重建二叉树

#### 描述：输入某二叉树的前序遍历和中序遍历的结果，请重建出该二叉树。假设输入的前序遍历和中序遍历的结果中都不含重复的数字。例如输入前序遍历序列{1,2,4,7,3,5,6,8}和中序遍历序列{4,7,2,1,5,3,8,6}，则重建二叉树并返回。  

```java
/**
 * Definition for binary tree
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
import java.util.Arrays;
public class Solution {
    public TreeNode reConstructBinaryTree(int [] pre,int [] in) {
        if (pre.length == 0 || in.length == 0) {
            return null;
        }
        TreeNode root = new TreeNode(pre[0]);
        // 在中序中找到前序的根
        for (int i = 0; i < in.length; i++) {
            if (in[i] == pre[0]) {
                // 左子树，注意 copyOfRange 函数，左闭右开
                root.left = reConstructBinaryTree(Arrays.copyOfRange(pre, 1, i + 1), Arrays.copyOfRange(in, 0, i));
                // 右子树，注意 copyOfRange 函数，左闭右开
                root.right = reConstructBinaryTree(Arrays.copyOfRange(pre, i + 1, pre.length), Arrays.copyOfRange(in, i + 1, in.length));
                break;
            }
        }
        return root;
    }
}
```

### 用两个栈实现队列

#### 描述：用两个栈来实现一个队列，完成队列的Push和Pop操作。 队列中的元素为int类型。

+ 方法一

```java
import java.util.Stack;

public class Solution {
      Stack<Integer> stack1 = new Stack<Integer>();
    Stack<Integer> stack2 = new Stack<Integer>();

    public void push(int node) {
        stack1.push(node);
    }

    public int pop() {
        while(stack1.size() != 0){
            stack2.push(stack1.pop());
        }
        int temp = stack2.pop();
        while(stack2.size() != 0){
            stack1.push(stack2.pop());
        }
        return temp;
    }
}
```

+ 方法二

```java
import java.util.Stack;
public class Solution {
    Stack<Integer> stack1 = new Stack<Integer>();
    Stack<Integer> stack2 = new Stack<Integer>();
 
    public void push(int node) {
        stack1.push(node);
    }
 
    public int pop() {
        if (stack2.size() <= 0) {
            while (stack1.size() != 0) {
                stack2.push(stack1.pop());
            }
        }
        return stack2.pop();
    }
}
```

### 旋转数组的最小数字

### 描述：把一个数组最开始的若干个元素搬到数组的末尾，我们称之为数组的旋转。输入一个非递减排序的数组的一个旋转，输出旋转数组的最小元素。例如数组{3,4,5,1,2}为{1,2,3,4,5}的一个旋转，该数组的最小值为1。NOTE：给出的所有元素都大于0，若数组大小为0，请返回0。

+ 暴力法

```java
import java.util.ArrayList;
public class Solution {
    public int minNumberInRotateArray(int [] array) {
        if(array.length == 0){
            return 0;
        }
        int min = array[0];
        for(int i = 0; i < array.length; i++){
            if(min > array[i]){
                min = array[i];
            }
        }
        return min;
    }
}
```

+ 二分查找法

```java

```

### 斐波那契数列

#### 描述：大家都知道斐波那契数列，现在要求输入一个整数n，请你输出斐波那契数列的第n项（从0开始，第0项为0）。n<=39

+ 方法一

```java
public class Solution {
    public int Fibonacci(int n) {
        if(n == 0){
            return 0;
        }
        if(n == 1 || n == 2){
            return 1;
        }
        int pre = 1;
        int cur = 1;
        for(int i = 2; i < n; i++){
            int tmp = cur;
            cur = cur + pre;
            pre = tmp;
        }
        return cur;
    }
}
```

+ 递归法

```java
public class Solution {
    public int Fibonacci(int n) {
        if(n <= 1){
            return n;
        }
        return Fibonacci(n - 1) + Fibonacci(n - 2);
    }
}
```

+ 方法三

```java
public class Solution {
    public int Fibonacci(int n) {
        int a = 0;
        int b = 1;
        while(n-->0){
            b = a + b;
            a = b - a;
        }
        return a;
    }
}
```

### 跳台阶

#### 描述：一只青蛙一次可以跳上1级台阶，也可以跳上2级。求该青蛙跳上一个n级的台阶总共有多少种跳法（先后次序不同算不同的结果）。

```java
public class Solution {
    public int JumpFloor(int target) {
        if(target == 1){
            return 1;
        }
        if(target == 2){
            return 2;
        }
        return JumpFloor(target - 1) + JumpFloor(target - 2);
    }
}
```

