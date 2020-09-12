学习笔记
刷题步骤：
1.分析题意。
2.找出特殊情况
3.整理解题思路，编写代码。
4.对编写的代码进行时间复杂度和空间复杂度进行分析
5.查看别人的代码，自己抄写几遍，将好的记住。
6.拓展问题，寻找相似的问题。
7.制定时间表，定期对已完成的题目重写

学习难题：
1.学习习惯问题：学习了几天发现最大的障碍不是没时间学习也不是无法理解题目的解析。
最大的障碍是自己的学习习惯，从小就养成了看别人的答案是不好的，自己做出来才是自己的，和别人的答案一样都不好意思给任何人看到。
最近几天看到题目，自己没有解题思路就会使劲想解题思路，真不是自己不想看别人的解题思路，是自己潜意识的要自己去想解题思路，控制不了自己。
等我发现这样死磕是不行的时候，已经过去了好几小时。
自己有解题思路的时候，写代码完老是调不通，一直在那里调试，一直不成功。即使成功了也是好几小时过去了。
尝试的解决办法：拿到题目是手机15分钟的倒计时，到时间就直接看别人的题目解析。

2.学习拖延症：经常对自己说刷题可以明天补上，今天已经可以了。每天都积攒了好多题目要完成。
尝试的解决办法：尽量控制自己完成。


刷题：
21.合并两个有序链表
class Solution {
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        if(l1 == null ) return l2;
        if(l2 == null ) return l1;
        if(l1.val < l2.val ){            
            l1.next =mergeTwoLists(l1.next, l2);     
            return l1;
        }  else {
            l2.next = mergeTwoLists(l1, l2.next);
            return l2;
        }
    }
}
这题的拓展：第876题链表的中间节点 和 第148题排序链表，单独做第148题时比较难，但先做21题和876题后，再去做148就比较简单。


42.接雨水
class Solution {
    public int trap(int[] height) {
        int len = height.length;
        int count = 0;
        int[] lNums = new int[len];
        int[] rNums = new int[len];
        //从左边往右扫描，把左边最大值替代右边。
        for(int j=0; j < len ; j++){
            if(height[j] > count ) {
                count = height[j];
            }
            lNums[j]=count;
        }
        count = 0;
         //从右边往左扫描，把右边最大值替代左边。
        for(int i=len-1; i >=0 ; i--){
              if(height[i] > count ) {
                count = height[i];
            }
            rNums[i]=count;            
        }
        count = 0;
        //找到左和右数组中最小值，减去原来数组的值就是能接的雨水值。        
        for(int k=0; k < len ; k++){
            if( rNums[k] > lNums[k]) {
                count = count + lNums[k] -height[k];
            }else{
                count = count + rNums[k] -height[k];
            }
        }
        return count;
    }
}

这题的拓展：第407题 接雨水II ，把m*n二维数组拆成 m个长度时n的一维数组和n个长度时m的一维数组.
m个长度时n的一维数组, 每个数组接雨水值组成一个二维数组。
n个长度时m的一维数组, 每个数组接雨水值组成一个二维数组。
这两个二维数组对应的位置取最小值相加就是m*n二维数组的接雨水量。




