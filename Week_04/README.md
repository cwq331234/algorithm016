学习笔记

深度优先搜索：适合解决必须走到最深处(例如对于树，须走到它的叶子节点)才能得到一个解的问题。通常利用递归实现，暴力递归所有的状态。
每次递归开始的时候要判断是否达到收敛条件，若达到了则得到一个可行解。
若没达到，则对当前状态进行处理，去掉一些不符合条件的状态。
示例代码：
visited=set();
void dfs(node,visited) {
    visited.add(node);
    ...
  for next_node in node , children():
    if not next_node in visited:
     dfs( next node,visited)
  
 广度优先搜索：
  广度优先搜索一层一层地进行遍历，每层遍历都以上一层遍历的结果作为起点，遍历一个距离能访问到的所有节点。
  广度优先搜索通常帮助我们解决一类最优问题: 距离最短,次数最少,时间最短等...以及连通块等图问题。
示例代码：
public class TreeNode {
    int val;
    TreeNode left;
    TreeNode right;

    TreeNode(int x) {
        val = x;
    }
}

public List<List<Integer>> levelOrder(TreeNode root) {
    List<List<Integer>> allResults = new ArrayList<>();
    if (root == null) {
        return allResults;
    }
    Queue<TreeNode> nodes = new LinkedList<>();
    nodes.add(root);
    while (!nodes.isEmpty()) {
        int size = nodes.size();
        List<Integer> results = new ArrayList<>();
        for (int i = 0; i < size; i++) {
            TreeNode node = nodes.poll();
            results.add(node.val);
            if (node.left != null) {
                nodes.add(node.left);
            }
            if (node.right != null) {
                nodes.add(node.right);
            }
        }
        allResults.add(results);
    }
    return allResults;
}




贪心算法：
在对问题求解时，总是做出在当前看来是最好的选择。也就是说，不从整体最优上加以考虑，它所做出的仅仅是在某种意义上的局部最优解。
贪心算法不是对所有问题都能得到整体最优解，选择的贪心策略必须具备无后效性（即某个状态以后的过程不会影响以前的状态，只与当前状态有关。）
所以，对所采用的贪心策略一定要仔细分析其是否满足无后效性。
示例代码：
从问题的某一初始解出发：
while (朝给定总目标前进一步)
{
利用可行的决策，求出可行解的一个解元素。
}
由所有解元素组合成问题的一个可行解；


二分查找：
二分查找是一种算法，其输入是一个有序的元素列表（必须是有序的），如果查找的元素包含在列表中，二分查找返回其位置，否则返回NULL。
二分查找的时间复杂度为O(logn)，远远好于顺序查找的O(n)。
虽然二分查找的效率高，但是要将表按关键字排序。而排序本身是一种很费时的运算。既使采用高效率的排序方法也要花费O(nlgn)的时间。
示例代码：
left,right=0,len(array)-1
while left<=right;
 mid = (left+right)/2
 if array[mid]== target;
 # find the target!!
 break or retunr result 
  if array[min] <target;
  left=mid+1;
  else:
   right = mid -1;



