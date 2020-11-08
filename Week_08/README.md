学习笔记

位运算：
    &   按位与
    |   按位或
    ^   按位异或
    ~   取反
    <<  左移，相当与*2
    >>  右移，正数高位补0，负数由计算机决定
    位运算速度快，有些计算可以直接用位运算来做，int a=b/2.可以写成int a=b>>1,int a=b*2.可以写成int a=b<<1,

布隆过滤器：
    本质上布隆过滤器是一种数据结构，比较巧妙的概率型数据结构（probabilistic data structure），特点是高效地插入和查询，可以用来告诉你 “某样东西一定不存在或者可能存在”。
    相比于传统的 List、Set、Map 等数据结构，它更高效、占用空间更少，但是缺点是其返回的结果是概率性的，而不是确切的。
    
应用场景：网页黑名单，垃圾邮件过滤，电话黑名单，url去重，内容推荐等。

改进：通常误杀的话，可以通过两个方法去补救，再建立一个白名单，从布隆器本身去优化，降低误杀率。


排序算法：
    一：比较类的排序：
        1.交换排序：冒泡排序、快速排序
        2.插入排序：简单插入排序、希尔排序
        3.选择排序：简单选择排序，堆排序
        4.归并排序：二路归并排序、多路归并排序
    二：非比较排序：
        1.计数排序
        2.桶排序
        3.基数排序
        
冒泡排序：
    for(int i=0；i<length;i++){
        for (j = 0; j < length-i-1; j++)
            if(nums[j]>num[j+1]){
                int num=nums[j];
                nums[j]=nums[j+1];
                nums[j+1]=num;
            }
        }
    }
    
快速排序：  
    public static void quickSort(int[] arr){
        qsort(arr, 0, arr.length-1);
    }
    private static void qsort(int[] arr, int low, int high){
        if (low < high){
            int pivot=partition(arr, low, high);        //将数组分为两部分
            qsort(arr, low, pivot-1);                   //递归排序左子数组
            qsort(arr, pivot+1, high);                  //递归排序右子数组
        }
    }
    private static int partition(int[] arr, int low, int high){
        int pivot = arr[low];     //枢轴记录
        while (low<high){
            while (low<high && arr[high]>=pivot) --high;
            arr[low]=arr[high];             //交换比枢轴小的记录到左端
            while (low<high && arr[low]<=pivot) ++low;
            arr[high] = arr[low];           //交换比枢轴小的记录到右端
        }
        //扫描完成，枢轴到位
        arr[low] = pivot;
        //返回的是枢轴的位置
        return low;
    }
    快速排序是所有内部排序算法中平均性能最好的排序算法。
    但是快速排序是不稳定的排序算法。
  
简单插入排序：
        int j=0;
        for(int i=1;i<arr.length;i++) {
            int temp=arr[i];
            //temp存放将要插入的数据
            if(arr[i]<arr[i-1]) {
                for( j=i-1;j>=0&&arr[j]>temp;j--) {
                    arr[j+1]=arr[j];
                    //temp的位置空出来，把第j个的值赋给第j+1个；
                }
                arr[j+1]=temp;
            }
        }
插入排序是把数组分为有序区和无序区两块，然后将无序区的指定索引的数插入到有序区的指定位置，假设第0个元素是已经排序好的，无序区第一次循环从1开始遍历，设置一个temp，找到要插入的位置，把temp插入到有序区指定位置。  
  
希尔排序：
int i, j, gap;  
for (gap = n / 2; gap > 0; gap /= 2) //步长  
    for (i = 0; i < gap; i++)        //直接插入排序  
    {  
        for (j = i + gap; j < n; j += gap)   
            if (A[j] < A[j - gap])  
            {  
                int temp = A[j];  //取当前下标
                int k = j - gap;  //取有序部门的最后一个结点
                while (k >= 0 && A[k] > temp)  //比较有序部分的最大值（最后一个即是最大值）
                {               
                    A[k + gap] = A[k]; //将有序部分的值后移
                    k -= gap;  //往前面的有序结点移动，继续比较（每个结点相隔gap）
                }  
                A[k + gap] = temp;  
            }  
    }  
    
希尔排序(Shell Sort)是插入排序的一种。也称缩小增量排序，是直接插入排序算法的一种更高效的改进版本。希尔排序是非稳定排序算法。
  
堆排序：
 堆排序(Heap Sort)是指利用堆这种数据结构所设计的一种排序算法。堆是一个近似完全二叉树的结构，并同时满足堆积的性质：即子结点的键值或索引总是小于(或者大于)它的父节点。  
   
选择排序：
        for(int i=0;i<arr.length-1;i++) {
                int k=i;
                      //位置还不确定的数据
                for(int j=i+1;j<arr.length;j++) {
                    if(arr[j]<arr[k]) {
                        k=j;
                        //遍历找到比k小的索引，然后把j赋给k；
                    }
                }
                if(i!=k) {
                    int temp=arr[i];
                    arr[i]=arr[k];
                    arr[k]=temp;
                }
            }
选择排序就是把无序区的最小元素与首元素互换位置，然后将有序区的区间扩大一位，直到所有无序区都变成有序区。


归并排序：
    public static void merge(int arr[],int low,int mid,int high ) {
        int temp[]=new int[high-low+1];
        int i=low;
        //第一个数组的首索引
        int j=mid+1;
        //第二个数组的首索引
        int k=0;
        //新数组的首索引
        while(i<=mid&&j<=high) {
            if(arr[i]<arr[j]) {
                temp[k++]=arr[i++];
            }
            else {
                temp[k++]=arr[j++];
            }
        }
        //把两个有序数组合并到新数组中
        while(i<=mid) {
            temp[k++]=arr[i++];
        }
        while(j<=high) {
            temp[k++]=arr[j++];
        }
        for(int n=0;n<temp.length;n++) {
            arr[n+low]=temp[n];
        }
        //排序好的数组放置在temp中，要将其复制到arr中。
    }
    public static void MergeSort(int arr[],int low,int high) {
        int mid=(low+high)/2;
        if(low<high) {
            //防止栈溢出异常
            MergeSort(arr,low,mid);
            MergeSort(arr,mid+1,high);
            merge(arr, low, mid, high); 
        }
归并排序要点有两个：对于两个有序数组的合并；递归思想。合并两个有序数组要定义一个新数组temp来存放合并后的数组，并通过判断条件让新的数组在合并后成为有序数组。归并的时候让数组调用自己，一步步将数组的长度变小，当子数组被分治到只有一个元素的时候，子数组也就是有序数组，这时候可以调用合并有序数组的方法，整个数组也就完成了排序。

计数排序：
    public static void sortCount(int[] arr, int m, int n) {
        int len = arr.length;
        int[] tem = new int[n - m + 1];
        for(int i = 0; i < len; i++) {
            tem[arr[i] - m] += 1;
        }
        for(int i = 0, index = 0; i < tem.length; i++) {
            int item = tem[i];
            while(item-- != 0) {
                arr[index++] = i + m;
            }
        }
    }
计数排序适用于有明确范围的数组，比如给定一个数组，且知道所有值得范围是[m,n]。这个时候可以使用一个n-m+1长度的数组，待排序的数组就可以散在这个数组上，数组的值就是当前值的个数，再经过一次遍历展开，得到的数组就有序了。



桶排序：
 //1.计算出最大值和最小值，求出两者的差值
        double min = arr[0];
        double max = arr[0];
        for (int i = 1; i < arr.length; i++) {
            if (max < arr[i]){
                max = arr[i];
            }
            if (arr[i] < min){
                min = arr[i];
            }
        }
        double d = max - min;

//2.初始化桶
        int bucketNum = arr.length;
        List<LinkedList<Double>> bucketList = new ArrayList<>(bucketNum);
        for (int i = 0; i < bucketNum; i++) {
            bucketList.add(new LinkedList<>());
        }

//3.遍历数组中的元素，把所有元素都放入对应的桶当中
        for (int i = 0; i < arr.length; i++) {
            //计算当前元素应该放在哪个桶里面
            int num = (int)((arr[i] - min) / (d / (bucketNum - 1)));
            bucketList.get(num).add(arr[i]);
        }

//4.对每个桶里面的元素进行排序
        for (int i = 0; i < bucketNum; i++) {
            Collections.sort(bucketList.get(i));
        }

//5.输出全部元素
        int k = 0;
        for(LinkedList<Double> doubles : bucketList){
            for (Double aDouble : doubles) {
                arr[k] = aDouble;
                k++;
            }
        }
桶排序是将数组中的数划分到不同的区间，再对每个桶中的数进行排序，这时用的排序算法一般为快速排序或者归并排序，然后再把所有桶中的数返回给原数组。


基数排序：
    a -- 数组  n -- 数组长度  exp -- 指数。对数组a按照该指数进行排序。
void count_sort(int a[], int n, int exp)
{
    int output[n];             // 存储"被排序数据"的临时数组
    int i, buckets[10] = {0};

   // 将数据出现的次数存储在buckets[]中
    for (i = 0; i < n; i++)
        buckets[ (a[i]/exp)%10 ]++;

   // 更改buckets[i]。目的是让更改后的buckets[i]的值，是该数据在output[]中的位置。
    for (i = 1; i < 10; i++)
        buckets[i] += buckets[i - 1];

   // 将数据存储到临时数组output[]中
    for (i = n - 1; i >= 0; i--)
    {
        output[buckets[ (a[i]/exp)%10 ] - 1] = a[i];
        buckets[ (a[i]/exp)%10 ]--;
    }

   // 将排序好的数据赋值给a[]
    for (i = 0; i < n; i++)
        a[i] = output[i];
}

基数排序(Radix Sort)是桶排序的扩展，它的基本思想是：将整数按位数切割成不同的数字，然后按每个位数分别比较。
具体做法是：将所有待比较数值统一为同样的数位长度，数位较短的数前面补零。然后，从最低位开始，依次进行一次排序。这样从最低位排序一直到最高位排序完成以后, 数列就变成一个有序序列。



