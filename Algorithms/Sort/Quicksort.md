

#	Quicksort

##	Background

&emsp;The quicksort algorithm is used for sorting an array.

##	Pseudocode

&emsp;Assume that we have an array $arr$ whose length is $len$. The bold and italic number denotes the pivot number.

1. Get a pivot number randomly from the array $arr$. And we swap it with the far left number of $arr$. 

   <div align=center>
   
   | i |  0   |  1   |  2   |  3   |  4   |  5   |
   | :---: | :--: | :--: | :--: | :--: | :--: | :--: |
   | **arr[i]** |  5  |  1   | ***6***  |  6   |  9   |  2   |
   
   </div>
   
   <div align=center>
   
   | i |  0   |  1   |  2   |  3   |  4   |  5   |
   | :---: | :--: | :--: | :--: | :--: | :--: | :--: |
   | **arr[i]** |  ***6***  |  1   |   5  |  6   |  9   |  2   |
   
   </div>  

2. Follow the rule to modify the array $arr$. Scan all numbers which is on the right side of $arr[0]$ one by one. The variable $index$ is used for determining the final index of the pivot number in the sorted array. Currently, the value of $index$ is equal to $1$. If current number $arr[i]$ is less than the pivot number $arr[0]$, we will swap it with $arr[index]$ and increase $index$ by one. Otherwise, we do nothing but continue scanning the array. After scanning all the numbers, we will swap the pivot number $arr[0]$ with the number $arr[index-1]$. In this way, we **divide** the array into two parts, the left array $arr[0, index -1]$ and the right array $arr[index + 1, len -1]$. The process is called **partition**.

   <div align=center>$arr[0] \gt arr[i=1] \rightarrow swap(arr, i=1, j=index=1)​$, then $index = 1+1=2​$</div>

   <div align=center>

   |     i      |            0             |  1   |  2   |  3   |  4   |  5   |
   | :--------: | :----------------------: | :--: | :--: | :--: | :--: | :--: |
   | **arr[i]** | ***6*** |  1   |  5   |  6   |  9   |  2   |
   
   </div>

   <div align=center>$arr[0] \gt arr[i=1+1=2] \rightarrow swap(arr, i=2, j=index=2)$, then $index = 2+1=3$</div>

   <div align=center>

   |     i      |            0             |  1   |  2   |  3   |  4   |  5   |
   | :--------: | :----------------------: | :--: | :--: | :--: | :--: | :--: |
   | **arr[i]** | ***6*** |  1   |  5   |  6   |  9   |  2   |

   </div>

   <div align=center>$arr[0] \le arr[i=2+1=3] \rightarrow$ do nothing</div>

   <div align=center>

   |     i      |            0             |  1   |  2   |  3   |  4   |  5   |
   | :--------: | :----------------------: | :--: | :--: | :--: | :--: | :--: |
   | **arr[i]** | ***6*** |  1   |  5   |  6   |  9   |  2   |

   </div>

   <div align=center>$arr[0] \le arr[i=3+1=4] \rightarrow$ do nothing</div>

   <div align=center>

   |     i      |            0             |  1   |  2   |  3   |  4   |  5   |
   | :--------: | :----------------------: | :--: | :--: | :--: | :--: | :--: |
   | **arr[i]** | ***6*** |  1   |  5   |  6   |  9   |  2   |

   </div>

   <div align=center>$arr[0] \gt arr[i=4+1=5] \rightarrow swap(arr, i=5, j=index=2+1=3)$, then $index = 3+1=4$</div>

   <div align=center>

   |     i      |            0             |  1   |  2   |  3   |  4   |  5   |
   | :--------: | :----------------------: | :--: | :--: | :--: | :--: | :--: |
   | **arr[i]** | ***6*** |  1   |  5   |  2   |  9   |  6   |

   </div>

   <div align=center>$swap(arr, i=0, j=index-1=4-1=3)$</div>

   <div align=center>

   |     i      |  0   |  1   |  2   |            3             |  4   |  5   |
   | :--------: | :--: | :--: | :--: | :----------------------: | :--: | :--: |
   | **arr[i]** |  2   |  1   |  5   | ***6*** |  9   |  6   |

   </div>

3. Similar to what we did in step two, we partition two sub-arrays recursively till there is no sub-array.


##	Analysis

###		Time Complexity

###		Space Complexity

## Code

###		Java

```java
public class Quicksort {
    public static void main(String arg[]){
        int[] arr = {3,2,3,1,2,4,5,5,6};
        System.out.println(Arrays.toString(sort(arr, 0, arr.length - 1)));
    }

    public static int[] sort(int[] arr, int left, int right){
        if (left < right) {
            // System.out.println("Before:" + Arrays.toString(arr));
            int partitionIndex = partition(arr, left, right);
            // System.out.println("L:"+ String.valueOf(left) + " R:" + String.valueOf(right) + " P:" + String.valueOf(partitionIndex));
            // System.out.println("After:" + Arrays.toString(arr));
            // System.out.println("------------------------------------");
            sort(arr, left, partitionIndex - 1);
            sort(arr, partitionIndex + 1, right);
        }
        return arr;
    }

    public static int partition(int[] arr, int left, int right){
        int randomIndex = left + new Random().nextInt(right - left + 1);
        swap(arr,randomIndex,left);
        int pivot = left;
        int index = pivot + 1;
        for(int i = index; i <= right; i++){
            if (arr[i] < arr[pivot]){
                swap(arr, i, index);
                index++;
            }
        }
        swap(arr, pivot, index - 1);
        return index - 1;
    }

    public static void swap(int[] arr, int i, int j){
        int temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
    }
}
```



