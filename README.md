import static java.lang.Math.ceil;

/**
 * 各种排序算法 Java实现
 * Created by zsd on 16-7-14.
 */
public class sortTest {
    /**
     * 冒泡排序(升序)
     * @param a
     * @return 升序序列
     */
    public static int[] bubbleSort1(int[]a){
        int len = a.length;
        int num = len;
        for(int i=0;i<len;i++){
            for(int j = 0;j<num-1;j++){
                if(a[j+1]<a[j]){
                    int temp = a[j+1];
                    a[j+1]=a[j];
                    a[j]=temp;
                }
            }
            num--;
        }
        return a;
    }

    /**
     * 冒泡排序(升序)
     * @param a
     * @return 升序序列
     */
    public static int[] bubbleSort2(int[] a){
        int len = a.length;
        boolean flag = true;
        for(int i =0 ;i<len&&flag;i++){
            flag = false;
            for(int j =len-1;j>0;j--){
                if(a[j-1]>a[j]){
                    int temp = a[j];
                    a[j]=a[j-1];
                    a[j-1]=temp;
                    flag = true;
                }
            }
        }
        return a;
    }
    /**
     * 简单选择排序(升序)
     * @param a
     * @return 升序序列
     */
    public static int[] choiceSort(int[] a) {
        int len = a.length;
        for (int j = 0; j < len; j++) {
            int minValue = j;
            for (int i = j; i < len; i++) {
                if (a[i] < a[minValue]) {
                    minValue = i;
                }
            }
            int temp = a[j];
            a[j]=a[minValue];
            a[minValue]=temp;
        }
        return a;
    }

    /**
     * 插入排序(升序)
     *
     * @param a 待排的整型序列
     * @return 升序序列
     */
    public static int[] insertSort1(int[] a) {
        int len = a.length;
        for (int i = 1; i < len; i++) {
            int curValue = a[i];
            for (int j = i - 1; j > -1; j--) {
                if (curValue < a[j]) {
                    a[j + 1] = a[j];
                    a[j] = curValue;
                } else {
                    a[j + 1] = curValue;
                    break;
                }
            }
        }
        return a;
    }

    /**
     * 改进版插入排序（升序）
     *
     * @param a 待排序的整型序列
     * @return 升序序列
     */
    public static int[] insertSort2(int[] a) {
        int len = a.length;
        int k = 0; //初始化一个变量用于记录前一个排好序的元素的位置
        int v = a[0]; //初始化一个变量用于记录前一个排好序的元素的值
        int flag = 0; //初始化一个变量用于记录当前待排元素与前一个已排好序的元素的大小
        for (int i = 1; i < len; i++) {
            flag = a[i] - v;
            int curValue = a[i];
            if (flag < 0) { //当前待排元素小于前一个已排元素
                for (int n = i; n > k; n--) { //将大于前一个已排元素的有序序列后移一位
                    a[n] = a[n - 1];
                }
                if (k - 1 < 0) { //若前一个已排元素为当前有序序列的最小元素
                    a[k] = curValue;
                    v = curValue;
                }
                for (int j = k - 1; j > -1; j--) { // 将小于前一个已排元素的其他元素与当前待排元素进行比较
                    if (a[j] > curValue) {
                        a[j + 1] = a[j];
                        a[j] = curValue;
                        k = j;
                        v = curValue;
                    } else {
                        a[j + 1] = curValue;
                        k = j + 1;
                        v = curValue;
                    }
                }
            } else { // 当前待排元素大于前一个已排元素
                for (int m = i - 1; m > k; m--) {
                    if (a[m] > curValue) {
                        a[m + 1] = a[m];
                    } else {
                        a[m + 1] = curValue;
                        k = m + 1;
                        v = curValue;
                    }
                }
            }
        }
        return a;
    }

    /**
     * 希尔排序(升序)
     *
     * @param a
     * @return 升序序列
     */
    public static int[] shellSort(int[] a) {
        int len = a.length;
        int n = len / 3;
        while (n > 0) {
            for (int i = n; i < len; i++) {
                if (a[i] < a[i - n]) {
                    int curValue = a[i];
                    int k = i - n;
                    for (; k >= 0 && curValue < a[k]; k -= n) {
                        a[k + n] = a[k];
                    }
                    a[k + n] = curValue;
                }

            }
            n = n / 3;
        }
        return a;
    }

    /**
     * 堆排序(大顶堆)
     * @param a 待排序序列
     * @return 有序序列(升序)
     */
    public static int[] heapSort(int[] a){
        int len = a.length;
        int temp = 0;
        for(int j=0;j<len;j++){
            adjustHeap(a,len-j);
            temp = a[0];
            a[0]=a[len-j-1];
            a[len-j-1]=temp;
        }
        return a;
    }

    /**
     * 将现有序列a的长度为len的子序列调整成大顶堆
     * @param a
     * @param len
     * @return 大顶堆序列
     */
    public static int[] adjustHeap(int[] a,int len){
        boolean flag = (len%2==0);//当len为偶数时,(2*i+2)会超出index范围
        for(int i= len/2-1;i>=0;i--){
            int temp = 0;
            if(a[i]<a[2*i+1]){
                temp=a[i];
                a[i]=a[2*i+1];
                a[2*i+1]=temp;
            }
            if(flag){
                flag = !flag;
                continue;
            }
            if(a[i]<a[2*i+2]){
                temp=a[i];
                a[i]=a[2*i+2];
                a[2*i+2]=temp;
            }
        }
        return a;
    }

    /**
     * 快速排序(升序)
     * @param a 待排序列
     * @return 升序序列
     */
    public static int[] quickSort(int[] a){
        int len = a.length;
        partQuickSort(a,0,len-1);
        return a;
    }
    /**
     * 快速排序部分排序
     * @param a 待排序列
     * @param low 部分的起始索引
     * @param high 部分的结束索引
     * @return 升序序列
     */
    public static int[] partQuickSort(int[] a,int low,int high){
        if(low<high){
            int flag = a[low];
            int start = low;
            for(int i =low;i<high+1;i++){
                if(a[i]<flag){
                    int temp =a[i];
                    for(int j=i;j>low;j--){
                        a[j]=a[j-1];
                    }
                    a[low]=temp;
                    start++;
                }
            }
            partQuickSort(a,0,start);
            partQuickSort(a,start+1,high);
        }
        return a;
    }

    /**
     * 桶排序(未完成)
     * @param a
     * @param bucketNum
     * @return
     */
    public static int[] bucketSort(int[] a,int bucketNum){
        int len = a.length;
        int max = a[0];
        int min = a[0];
        for(int i=1;i<len;i++){
            if(max<a[i]){
                max=a[i];
            }
            if(min>a[i]){
                min=a[i];
            }
        }
        int level = (max-min)/bucketNum;
        StringBuffer[] sbs = new StringBuffer[bucketNum];
        for(int i =0;i<len;i++){ // 分桶
            int bukect = (int) ceil((a[i]-min)/(1.0*level))-1; // 桶号
            sbs[bukect].append(a[i]);
        }
        for(int i =0;i<bucketNum;i++){
            // 此处调用普通排序算法即可

        }
        return a;
    }

    public static void test(){

        System.out.println(ceil(5/(2*1.0)));
    }
    public static void main(String[] args) {
        int[] a = {6, 7, 3, 6, 6, 5, 7, 5, 4, 3, 9, 10, 34};
        for (int e : a) {
            System.out.print(e + " ");
        }
        System.out.println();
        long startTime = System.currentTimeMillis();
        int[] res = quickSort(a);
        long endTime = System.currentTimeMillis();
        long time = endTime - startTime;
        for (int e : res) {
            System.out.print(e + " ");
        }
        System.out.println();
        System.out.println(time);
        test();
    }
}
