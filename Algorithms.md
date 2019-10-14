### 一、冒泡排序

理解：冒泡排序（从小到大），比如给定一个数组 [3,5,2,1]，那么冒泡排序是通过两两比较，如果前面的数大于后面的数，则交换位置，每一趟比较下来都确定一个最大值，具体如下：

第一轮：比较3和5，发现3小于5，所以不交换，继续比较5和2，发现5大于2，因此交换位置，此时 为[3,2,5,1]，       

​               接下来拿5和1进行比较，发现5大于1，交换位置，到此第一轮就结束了，此时为[3,2,1,5],第一轮确定了

​               最大的数5

第二轮：3和2进行比较，发现3大于2，因此交换位置，此时为[2,3,1,5]，接下来拿3和1比较，发现3大于1，交换

​              位置，此时为[2,1,3,5]，第二轮确定了最大的数3

第三轮：2和1进行比较，发现2大于，因此交换位置，最后为[1,2,3,5]

通过上面的分析，可以发现一共需要`arr.length-1-i`轮，(此时的i是第几轮) 每次需要跑

```javascript
function bubbleSort(arr){
    //外出循环控制的是轮数
    for(var i=0;i<arr.length-1;i++){
        //里层控制的是每轮中数的比较，由于每轮都会确定一个最大的数，这个数下一轮可以不用再比较
        for(var j=0;j<arr.length-1-i;j++){
            if(arr[j]>arr[j+1]){
                var temp = arr[j]
                arr[j] = arr[j+1]
                arr[j+1] = temp
            }
        }
    }
    return arr
}
```

### 二、选择排序

理解： 选择排序，将数组进行循环，每一轮循环都挑出第一个数作为最小值，和其他值进行比较，一旦有比这个值小的，就交换，接着再拿下边的值和最小值进行比较，如此进行比较，直到比较结束，就可以找到这一轮的最小值，再将这个最小值赋给对应的arr[i]即可达到排序。

```javascript
function changeSort(arr){
    //最外层循环控制每一轮
        for(var i=0;i<arr.length;i++){
            var min = arr[i]
            //里层循环控制每一轮能找到一个最小值
            for(var j=i+1;j<arr.length;j++){
                if (arr[j]< min){
                    var temp = min
                    min = arr[j]
                    arr[j] = temp

                }
            }
            //每一轮确定好最小值后，将值付给数组的具体索引
            arr[i] = min
        }
        return arr
    }
```

### 三、插入排序

理解：插入排序就和打扑克牌一样，每轮设置一个值作为比较，比如设置temp,且设置的值从第二个开始，然后把这个值拿出来，和排在这个值前面的值进行比较，如果比这个值大，那么前面这个值就向右移一位，然后再拿前面的值和做个temp做比较，如果前面的值还是比temp大，则这个值继续向右移，反之，把temp插入到这个位置

```javascript
 function insertSort(arr) {
        for(let i=1;i<arr.length;i++){
            let j=i-1
            let temp = arr[i]
            while(j>=0 && arr[j]>temp){
                arr[j+1] = arr[j]
                j--
            }
            arr[j+1] = temp
        }
        return arr
    }

```

### 四、快速排序

理解：快速排序的核心思想是将数组的第一个元素拿出来，然后创建left和right 两个空数组，如果原数组里的值比拿出来的第一个数大，则加入到right，如果原数组里的值比拿出来的数小，则加到left，接下来，对left 和right 数组进行同样的操作

```javascript
function quickSort(arr) {
        if (arr.length < 2) return arr
        var middle = arr[0]
        var left = []
        var right = []
        for(var i=1;i<arr.length;i++){
            if(arr[i]>middle){
                right.push(arr[i])
            }else {
                left.push(arr[i])
            }
        }

        return quickSort(left).concat(middle,quickSort(right))
    }
```

### 五、归并排序

理解：核心是使用递归的方法

```javascript
const mergeSort = arr => {
        // 采用自伤而下的递归方法
        const len = arr.length

        if (len < 2) {
            return arr
        }

        let middle = Math.floor(len/2),
            left = arr.slice(0,middle),
            right = arr.slice(middle)
        return merge(mergeSort(left),mergeSort(right))
    }

    const merge = (left,right) => {
        const result = []
         while (left.length && right.length){
             // 注意: 判断的条件是小于或等于，如果只是小于，那么排序将不稳定.
             if(left[0]<=right[0]) {
                 result.push(left.shift())
             } else {
                 result.push(right.shift())
             }
         }

         while (left.length) result.push(left.shift())
         while(right.length) result.push(right.shift())

        return result
    }
```









