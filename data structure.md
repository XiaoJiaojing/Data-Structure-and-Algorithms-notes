
### 一、栈结构的实现

以下针对每种数据结构，本文都将其封装在一个类（构造函数）中，以便多次使用。

**首先是栈结构，可以看做是羽毛球筒，只有一个口，这个口即是数据的出口也是数据的入口，也就是说栈是只能在一端进行插入和删除操作的特殊线性表，同时是一种`先进后出`的数据结构，且是只能在一端进行插入和删除操作的特殊线性表，如下图所示：**

![image-20190924154208183](/Users/yghysdr/Library/Application Support/typora-user-images/image-20190924154208183.png)

**主要有 入栈（push），出栈（pop），检查栈顶（peek），栈大小（size）等操作，以下是具体的代码实现：**

```javascript
 var Stack = function () {
        var items = [];     //私有的，通过数组来模拟一个栈，存储数据
        // this.items = [];   //共有的
        this.push = function (element) {
            items.push(element)
        }
     	
        this.pop = function () {
            return items.pop()
        }
        // peek 检查栈顶
        this.peek = function () {
            return items[items.length-1]
        }

        // 检查栈是否为空？
        this.isEmpty = function () {
            return items.length == 0
        }
        // 清除栈
        this.clear = function () {
            items = []
        }
        // 获取栈的大小
        this.size = function () {
            return items.length
        }
     
     //获取内部的items
        this.getItems = function () {
            return items;
        }
    }

```

### 二、队列结构的实现

**队列结构和栈十分相似，它们都是线性表，特殊之处在于它只允许在表的前端（front）进行删除操作，而在表的后端（rear）进行插入操作，也就是遵循`先进先出`的原则，队列从尾部添加新元素，从顶部移除元素，最新添加的元素必须排列在队列的末尾。如下图：**

![img](https://lc-api-gold-cdn.xitu.io/254fc2db33e98b3c6738?imageslim)



**主要有入列，出列，返回队列第一个元素，检查队列是否为空，队列长度等操作，具体的代码实现如下：**

```javascript
var Queue = function () {
        items = []  //私有的，通过数组来模拟一个队列，存储数据
        // 入列
        this.enqueue = function (element) {
            items.push(element)
        }
    	//出列
        this.dequeue = function () {
          return  items.shift()
        }
		//返回队列中第一个元素
        this.front = function () {
            return items[0]
        }
		//检查队列是否为空
        this.isEmpty = function () {
            return items.length === 0
        }
		//获取队列的长度
        this.size = function () {
            return items.length
        }
    	//清空队列
        this.clear = function () {
			items = []
        }
    	//获取队列
        this.getItems = function () {
			return items
        }
    }
```

### 三、链表结构的实现

**链表有单向链表，双向链表和循环链表，这里主要讲的是单向链表，单向链表中的每一个元素都是由元素本身数据和指向下一个元素的指针构成，所以添加或是移除某一个元素不需要对链表整体进行操作，只需要改变相关元素的指针指向就可以了。**

​      链表在实际生活中的例子也有很多，比如自行车的链条，环环相扣，或者是火车的车厢，每一节车厢就是元素，想要移除或是添加某一节车厢，只需要把连接车厢的链条改变一下就好了。

​    主要有一下操作：

+ append(element):向链表尾部添加一个新的元素；

+ insert(position,element):向链表特定位置插入元素；

+ remove(element):从链表移除一项；

+ indexOf(element):返回链表中某元素的索引，如果没有返回-1；

+ removeAt(position):从特定位置移除一项；

+ isEmpty():判断链表是否为空，如果为空返回true,否则返回false;

+ size():返回链表包含的元素个数；

+ toString():重写继承自Object类的toString()方法，因为我们使用了Node类；

具体代码实现如下：

```javascript
function LinkedList() {
    //Node类声明 模拟链表中每个节点的数据结构
    let Node = function(element){
        this.element = element;
        this.next = null;
    };
    //初始化链表长度
    let length = 0;
    //初始化第一个元素
    let head = null;
    this.append = function(element){
        //初始化添加的Node实例
        let node = new Node(element);
           
        if (head === null){
            //第一个Node实例进入链表，之后在这个LinkedList实例中head就不再是null了
            head = node;
        } else {
            current = head;
            //循环链表知道找到最后一项，循环结束current指向链表最后一项元素
            while(current.next){
                current = current.next;
            }
            //找到最后一项元素后，将他的next属性指向新元素node,j建立链接
            current.next = node;
        }
        //更新链表长度
        length++;
    };
    this.insert = function(position, element){
        //检查是否越界，超过链表长度或是小于0肯定不符合逻辑的
        if (position >= 0 && position <= length){
            let node = new Node(element),
                current = head,
                previous = null,
                index = 0;
            if (position === 0){
                //在第一个位置添加
                 head = node;
                 node.next = current;
               
            } else {
                //循环链表，找到正确位置，循环完毕，previous，current分别是被添加元素的前一个和后一个元素
                while (index < position){
                    previous = current;
                    current = current.next;
                    index++
                }
                node.next = current;
                previous.next = node;
            }
            //更新链表长度
            length++;
            return true;
        } else {
            return false;
        }
    };
    this.removeAt = function(position){
        //检查是否越界，超过链表长度或是小于0肯定不符合逻辑的
        if (position > -1 && position < length){
            let current = head,
                previous,
                index = 0;
            //移除第一个元素
            if (position === 0){
                //移除第一项，相当于head=null;
                head = current.next;
            } else {
                //循环链表，找到正确位置，循环完毕，previous，current分别是被添加元素的前一个和后一个元素
                while (index++ < position){
                    previous = current;
                    current = current.next;
                }
                //链接previous和current的下一个元素，也就是把current移除了
                previous.next = current.next;
            }
            length--;
            return current.element;
        } else {
            return null;
        }
    };
    this.indexOf = function(element){
        let current = head,
            index = 0;
        //循环链表找到元素位置
        while (current) {
            if (element === current.element) {
                return index;
            }
            index++;
            current = current.next;
        }
        return -1;
    };
    this.remove = function(element){
        //调用已经声明过的indexOf和removeAt方法
        let index = this.indexOf(element);
        return this.removeAt(index);
    };
    this.isEmpty = function() {
        return length === 0;
    };
    this.size = function() {
        return length;
    };
    this.getHead = function(){
        return head;
    };
    this.toString = function(){
        let current = head,
            string = '';
        while (current) {
            string += current.element + (current.next ? ', ' : '');
            current = current.next;
        }
        return string;
    };
    this.print = function(){
        console.log(this.toString());
    };
}
//一个实例化后的链表，里面是添加的数个Node类的实例
```

### 四、集合数据结构的实现，对应的是ES6中的 Set结构

**集合是类似于对象的一种数据结构，但是它是 value-value 的形式存在的**，特点是： 没有重复的数据

集合中主要有以下操作：

+ add(value):向集合添加一个新的项

+ remove(value):从集合移除一个值

+ has(value):如果值在集合中，返回true,否则返回false

+ clear():移除集合中的所有项

+ size():返回集合所包含的元素数量，与数组的length属性相似

+ values():返回一个集合中所有值的数组

+ union(setName):并集，返回包含两个集合所有元素的新集合(元素不重复)

+ intersection(setName):交集，返回包含两个集合中共有的元素的集合、

+ difference(setName):差集，返回包含所有存在本集合而不存在setName集合的元素的新集合

+ subset(setName):子集，验证setName是否是本集合的子集

```javascript
var Set2 = function () {
        var items = {}

        // has 检查元素是否存在 return boolean
        this.has = function (value) {
            return items.hasOwnProperty(value)
        }

        // 添加元素
        this.add = function (value) {
            if(this.has(value)){
                // 存在
                return false
            } else {
                items[value] = value
                return value
            }
        }
        
        // 删除方法
        this.remove = function (value) {
            if(this.has(value)){
                // delete 用来删除键值对
                delete items[value]
                return true
            } else {
                // 不用管
                return false
            }
        }

        // 清空集合
        this.clear = function () {
            items = {}
        }

        // 集合的大小
        this.size = function () {
            // var count = 0
            // // 遍历集合
            // for(var key in items){
            //     if(items.hasOwnProperty(key)){
            //         count++
            //     }
            // }
            // return count

            // 方法2
            // Object.keys(items)  返回所有键组成的数组
            return Object.keys(items).length
        }

        // 提取集合里所有的值
        this.value = function () {
            var value = []
            for(var key in items){
                if(items.hasOwnProperty(key)){
                    value.push(items[key])
                }
            }
            return value
        }

        // 并集
        this.union = function (otherSet) {
            var resultSet = new Set2()
            // 1.把自己的值提取出来
            var arr = this.value()
            for(var i=0;i<arr.length;i++){
                resultSet.add(arr[i])
            }
            // 把另一个集合的值取出来
            arr = otherSet.value()
            for(var i=0;i<arr.length; i++){
                resultSet.add(arr[i])
            }
            return resultSet
        }

        // 交集
        this.intersection = function (otherSet) {
            var resultSet = new Set2()
            var arr = this.value()
            for(var i=0;i<arr.length;i++){
                if(otherSet.has(arr[i])){
                    resultSet.add(arr[i])
                }
            }
            return resultSet
        }
        //差值
        this.difference = function (otherSet) {
            var resultSet = new Set2()

            var arr = this.value()

            for(var i=0;i<arr.length;i++){
                if(!otherSet.has(arr[i])){
                    resultSet.add(arr[i])
                }
            }
            return resultSet
        }

        // 调试
        this.getItems = function () {
            return items
        }

    }
```

### 五、字典结构的实现，对应ES6中的 Map 结构

**字典结构类似于对象，存储结构以键--值的方式存储，特点是字典中不存在重复的键**

```javascript
  var Dictionary = function () {
       // 添加键值对
        var items = {}

        this.has = function (key) {
            return items.hasOwnProperty(key)
        }
        this.set = function (key,value) {
            items[key]= value
        }

        // 删除对象中某个键值
        this.delete = function (key) {
            if(this.has(key)){
               var s = delete items[key]

                return true
            }
            return false
        }
        // 获取对象中指定 key 的值
        this.get = function (key) {
            if(this.has(key)){
                return items[key]
            }
            return undefined
        }

        this.getItems = function () {
            return items
        }
    }
```

##### 5.1 基于字典的 哈希表的出现

我们知道在数组中存储数据的时候，如果要找到某个元素。需要去遍历，这样的效率比较低，因此，我们希望把数据以 `键-值`的形式存储，通过键，就能获取到对应的值，或者把键转化成一个数字，以数组-索引的方式存储，通过索引来获取值，本文中的哈希表就是通过数组-索引来获取对应值的。哈希表的关键是将键转化成一个数字，这个转化过程主要是应用了不同字符对应不同的 ASCLL 码。

第一版本的哈希表代码如下：

```javascript
var Haxibiao = function () {
        var items = []  // 存储数据
		// 键 转 特殊数字   的函数
        var loseloseHashCode = function (key) {
            var hash = 0
            for(var i=0;i<key.length;i++){
                hash += key[i].charCodeAt()
            }
            return hash % 37
        }

        // 设置哈希表
        this.put = function (key,value) {
            var position = loseloseHashCode(key)
            items[position] = value
        }

        // 移除表中某个元素
        this.remove = function (key) {
            items[loseloseHashCode(key)] = undefined
        }

        this.get = function (key) {
            return items[loseloseHashCode(key)]
        }

        this.getItems = function () {
            return items
        }
    }
```

​        这样看似能解决问题，但是有时候，不同的键转化后的数字可能是相同的，这时候，就会产生新的问题。当键转化过来的数字相同的时候，后面的数据会覆盖前面的数据，针对这种情况，有两种解决方法，第一种是通过链表来解决，第二种是每次键转化后的数字都要先判断，该位置是否已经被占用，如果被占用，则继续向下找，下面如果没被占用，则将数据放在该位置，否则继续向下找。

​      **首先通过链表解决**

在 键 转化成 数字 的位置 比如 items[position] 的位置生成一个链表，如果下一个数据还是在这个位置，则将数据添加到链表尾部，具体代码如下：

```javascript
// 需要链表，因此我们把上面封装好的链表的构造函数拿过来
var LikedList = function () {
        var head = null
        var length = 0
        var Node = function (element) {
            this.element = element
            this.next = null
        }
        // 链表尾添加元素
        this.append = function (element) {
            var node = new Node(element)

            if(head == null){
                head = node
            } else {
                var current = head
                while(current.next){
                    current = current.next
                }
                current.next = node
            }
            length++
        }

        // 链表某一个位置添加元素
        this.insert = function (position,element) {
            //越界
            if(position > -1 && position < length){
                var node = new Node(element)
                if (position === 0){
                    var current = head
                    head = node
                    head.next = current
                } else {
                    var index = 0
                    var current = head
                    var previous = null
                    while(index < position){
                        previous = current
                        current = current.next
                        index++
                    }
                    previous.next = node
                    node.next = current
                }
                length++

            }
        }
        this.removeAt = function (position) {
            if(position>-1 && position < length){
                if(position===0){
                    var current = head
                    head = current.next
                } else {
                    var current = head
                    previous = null
                    index = 0
                    while(index<position){
                        previous = current
                        current = current.next
                        index++
                    }
                    previous.next = current.next
                }
                length--
                return current
            }
            return null

        }
        this.indexOf = function (element) {
            var current = head
            var index  = 0
            while(current){
                if(element === current.element){
                    return index
                }
                current = current.next
                index++
            }
        }

        // removeAt(position)    删除某个位置的元素
        // indexOf(element)      获取某个元素的位置
        // remove                删除某个元素
        this.remove = function (element) {
            return this.removeAt(this.indexOf(element))
        }
        this.isEmpty = function () {
            return length = 0
        }
        this.size = function () {
            return length
        }

        this.getHead = function () {
            return head
        }
    }
//使用分离链接法：
var HashTable_L = function () {
    var items = []  
    
    var loseloseHashCode = function (key) {
        var hash = 0
        for(var i=0;i<key.length;i++){
            hash += key[i].charCodeAt()
        }
        return hash % 37
    }
    //为了后面的遍历，存值的时候需要将键-值都存进去
    var Node = function (key,value){
        this.key = key
        this.value = value
    }
    this.put = function (key,value) {
        var node = new Node(key,value)
        var position = loseloseHashCode(key)
        if(items[position]){
            items[position].append(node)
        } else {
            var list = new LikedList()
            items[position] = list
            items[position].append(node)
        }
    }
    this.get = function (key){
        var position = loseloseHashCode(key)
        if(items[position]){
            var current = items[position].getHead()
            while(current){
                if(current.element.key === key){  //这里需要用到element判断，是因为链表里设置了链表中每个元素的结构。现在我们传入的element是一个包含 key 和 value 的 对象，因此需要用element.key来帮助判断
                    return current.element.value
                }
                current = current.next
            }
        } else {
            return undefined
        }
    }
    
    this.remove = function (key){
        var position = loseloseHashCode(key)
        if(items[position]){
            var current = items[position].getHead()
            while(current){
                if(current.element.key === key){
                    items[position].remove(current.element)
                   // 删除后判断当前链表是否为空，如果为空，则设置为 undefined
                    if(items[position].isEmpty()){
                        items[position] = undefined
                    }
                }
                return true
            }
            current  = current.next
        } else {
            return false
        }
    }
    
    this.getItems = function () {
        return table
    }   
}

```

解决哈希表的第二种方法： 线性探查表

```javascript
var HaxiTable_X = function () {
    var items  = []
    var loseloseHashCode = function (key) {
        var hash = 0
        for(var i=0;i<key[i].length;i++){
            hash += key[i].charCodeAt()
        }
        return hash % 37
    }
    var Node = function (key,value) {
        this.key = key
        this.value = value
    }
    
    this.put = function (key,value){
        var position = loseloseHashCode(key)
        if (items[position] == undefined){
            items[position] = new Node(key,value)
        } else {
            var index = position + 1
            while(items[position]!==undefined){
                index++
            }
            items[index] = new Node(key,value)
        }
    }
    //根据某个键 获取值
    this.get = function (key){
        var position = loseloseHashCode(key)
        if(items[position].key === key){
            return item[position].value
        } else {
            var index = position+1
            while(items[index].key !== key){
                index++
            }
            return item[index].value
        }
    }
    //删除某对键值
    this.remove = function (key) {
        var position = loselosehashCode(key)
        if(items[position].key === key){
            items[position] = undefined
        } else {
            var index = position+1
            while(items[position].key !== key){
                index++
            }
            items[index] = undefined
        }
        return true
    } else {
        return false
    }
    this.getTable = function () {
        return table
    }
}
```

接下来，还有另一种哈希算法，可以用来制作哈希表

```javascript
 var Haxibiao = function () {
        var table = []
        //新的哈希算法 这个算法可以大大减少出现重复的机率
        var djb2HashCode = function (key) {
            var hash = 5381
            for(var i=0;i<key.length;i++){
                hash = hash * 33 + key[i].charCodeAt()
            }
            return hash % 1013
        }
        this.put = function (key,value) {
            var position = djb2HashCode(key)
            table[position] = value

        }
        this.get = function (key) {
            var position = djb2HashCode(key)
            return table[position]
        }

        this.getTable = function () {
            return table
        }
    }
```

### 六、二叉树结构的实现

**树是用来模拟具有树状结构性质的数据集合。根据它的特性可以分为很多类，在本文中主要讲二叉树，二叉树是一种典型的树状结构，如名字描述的那样，二叉树是每个节点有两个子节点的树结构，且左子节点  < 节点 ，右子节点  > 节点，树结构的实现主要是用递归实现的。**

![image-20190924231832874](/Users/yghysdr/Library/Application Support/typora-user-images/image-20190924231832874.png)

主要的操作如下：

+ insertNode ：树结构中插入某个节点
+  traverse ： 遍历树结构中的节点
+ removeNode : 移除树结构中的某个节点

具体代码实现如下：

```javascript
var Tree = function () {
    var Node = function (value){
        this.value = value
        this.left = null
        this.right = null
    }
    
    var root = null
    
    //插入节点的递归函数
    var insertNode = function (node,newNode) {
        if(newNode.value > node.value){
            if(node.right === null){
                node.right = newNode
            } else {
                insertNode(node.right,newNode)
            }
        } else if (newNode.value < node.value){
            if (node.left === null){
                node.left = newNode
            } else {
                insertNode(node.left,newNode)
            }
        }
    }
    
    //插入某个节点
    this.insert = function (value) {
    	var newNode = new Node(value)
        if(root === null){
            root = newNode
        } else {
           //通过递归找到一个空的位置插入
           //因此需要重新定义一个递归函数  insertNode
            insertNode(root,newNode)
        }
    }
   //遍历的递归函数
    var traversed = function (node,callback) {
        if (node === null) {
            return 
        }
        
        /* 
         * 前序遍历
         * callback(node.value)
        */
        traversed(node.left,callback)
        //中序遍历
        callback(node.value)
        
        traversed(node.right,callback)
        
        /* 
         * 后序遍历
         * callback(node.value)
        */
        
    }
    
    //遍历节点  需要传入一个操作的回调函数
    this.traverse = function (callback) {
       // 遍历需要递归，因此要定义个递归函数
        traversed(root,callback)
    }
      // 移除有左右子节点时的辅助函数
        var findMinNode = function (node) {
            if (node == null) return null
            while(node && node.left){
                node = node.left
            }
            return node
        }
    //移除节点的递归函数
    var removeNode = function (node,value) {
        if(node === null) return null
        if(value > ndoe.value){
           node.right =  removeNode(node.right,value)
        } else if (value < node.value){
           node.left =  removeNode(node.left,value)
            return node
        } else {
            // 两个的值相等  value == node.value
                // 执行删除过程
            if (node.left === null && node.right === null){
                //删除叶节点的条件
                node = null
                return node
            }
              // 只有一个子节点条件
                if(node.left == null && node.right){
                    node = node.right
                    return node
                } else if (node.right == null && node.left){
                    node = node.left
                    return node
                }

                // 有两个子节点的条件
                var aux = findMinNode(node.right)  //查找右侧的最小子节点
                node.value = aux.value
                node.right = removeNode(node.right,aux.value)
                return node
        }   
    }
   // 移除节点
    this.remove = function (value) {
        //移除节点，也需要遍历节点，找到需要移除的节点，然后重构树
        // 定义移除节点的递归函数
        root = removeNode(root,value)
    }
     // 树结构中的最小值就是树结构的最左边的分支
        // 1.树还是空的
        // 2.树不是空的
        var min = function (node) {
            if (node == null) return null
            while(node && node.left){
                node = node.left
            }
            console.log(node)
        }
        this.min = function () {
           return min(root)
        }

        // 树结构中的最大值
        var max = function (node) {
            if(node == null) return null
            while(node && node.right){
                node = node.right
            }
            console.log(node)
        }
        this.max = function () {
            return max(root)
        }
        // 测试
        this.getRoot = function () {
            return root
        } 
}
```

### 七、图结构的实现

图是一种复杂的非线性结构。

在线性结构中，数据元素之间满足唯一的线性关系，每个数据元素(除第一个和最后一个外)只有一个直接前趋和一个直接后继；

在树形结构中，数据元素之间有着明显的层次关系，并且每个数据元素只与上一层中的一个元素(双亲节点)及下一层的多个元素(孩子节点)相关；

而在图形结构中，节点之间的关系是任意的，图中任意两个数据元素之间都有可能相关。

**图结构可以分为有向图和无向图两种**

本文主要学习的是`无向图`，如下： 顶点A有三条边，分别是B、C、D，顶点B有A、E、F三条边

A ==> B   C   D

B ==> A   E    

具体代码如下：

```javascript
var MyMap = function () {
        var vertices = []   //存储顶点
        var adjList = {}     //存储边
        // 把每个顶点作为对象的键，把边放在一个数组中，这样就能知道每个顶点分别有哪些边
        // adjList {
        //     A : [B,C,D]
        // }

        // 设置顶点的方法

        this.setVertices = function (value) {
            vertices.push(value)    //把顶点加入顶点数组中
            adjList[value] = []     // 每次添加顶点的时候，先设置每个顶点的边为空
        }

        //设置边的方法
        this.setAdj = function (a,b) {
            //由于我们现在构建的是一个无向图，因此当A-B两个顶点相连接时，A是顶点时，B是A的边，B是顶点时，A是B的边
            adjList[a].push(b)
            adjList[b].push(a)
        }
		//测试代码
        this.print = function () {
            var s = '\n'
            for(var i=0;i<vertices.length;i++){
                var dindian = vertices[i]
                s += dindian + '====>'
                for(var j=0;j<adjList[dindian].length;j++){
                  
                    s+=adjList[dindian][j]+ '\t'
                }
                s+= '\n'
            }
            console.log(s)
        }
    }
 var myMap = new MyMap()
 //添加以下顶点和边
    myMap.setVertices('A')
    myMap.setVertices('B')
    myMap.setVertices('C')
    myMap.setVertices('D')
    myMap.setVertices('E')
    myMap.setVertices('F')

    myMap.setAdj('A','B')
    myMap.setAdj('A','C')
    myMap.setAdj('A','D')
    myMap.setAdj('B','E')
    myMap.setAdj('B','F')
    myMap.print()
    //打印结果如下：
	/*
    A====>B	C	D	
    B====>A	E	F	
    C====>A	
    D====>A	
    E====>B	
    F====>B	
    */
```

至此，我们就简单的模拟了一个无向图结构，在此基础上，去实现广度优先遍历，也就是会先遍历每个顶点的所有边，然后再以这些边作为顶点，继续遍历它的边，如下图所示

![image-20190925152652186](/Users/yghysdr/Library/Application Support/typora-user-images/image-20190925152652186.png)

#### 广度优先遍历的代码实现

```javascript
// 需要借助 队列
var Queue = function () {
        items = []
        this.enqueue = function (element) {
            items.push(element)
        }
        this.dequeue = function () {
            return  items.shift()
        }

        this.front = function () {
            return items[0]
        }

        this.isEmpty = function () {
            return items.length === 0
        }

        this.size = function () {
            return items.length
        }
    }
	// 图结构
    var MyMap = function () {
        var vertices = []   //存储顶点
        var adjList = {}     //存储边
        // 把每个顶点作为对象的键，把边放在一个数组中，这样就能知道每个顶点分别有哪些边
        // adjList {
        //     A : [B,C,D]
        // }

        // 设置顶点的方法

        this.setVertices = function (value) {
            vertices.push(value)    //把顶点加入顶点数组中
            adjList[value] = []     // 每次添加顶点的时候，先设置每个顶点的边为空
        }

        //设置边的方法
        this.setAdj = function (a,b) {
            //由于我们现在构建的是一个无向图，因此当A-B两个顶点相连接时，A是顶点时，B是A的边，B是顶点时，A是B的边
            adjList[a].push(b)
            adjList[b].push(a)
        }
       /* 广度优先遍历的内容   开始了
         一开始要设置所有的顶点的颜色都是 white  表示所有的顶点都是未发现的
         {
            'A': 'white',
            'B': 'white',
            ...
           }
		*/
        var initColor = function () {
            var color = {}
            for(var i=0;i<vertices.length;i++){
                var dingdian = vertices[i]
                color[dingdian] = 'white'
            }
            return color
        }
        //广度优先遍历
        this.bfs = function (value,callback) {
            // 新建一个队列， 队列的在此的作用就是保证广度优先遍历，因为队列的特性：先进先出
            var queue = new Queue()
            // 一开始所有的点都是未发现的   用 white 表示
            var color = initColor()
            // 一旦入列后，标记为   已发现未探索  用 grey 表示
            queue.enqueue(value)
            color[value] = 'grey'

            // 接下来要 将队列中的数据拿出来，进行探索
            // 如果队列不为空，就可继续执行

            while(!queue.isEmpty()){
                var now = queue.dequeue()
                var edges = adjList[now]   //顶点对应的所有边
                for(var i=0;i<edges.length;i++){
                    var w = edges[i]
                    if(color[w] === 'white'){
                        //未发现的全部入列，并标记为已发现
                        queue.enqueue(w)
                        color[w] = 'grey'
                    }
                }
                color[now] = 'black'  //表示已探索
                if(callback){
                    callback(now)
                }

            }
        }
        /*广度优先遍历的内容 结束了*/

        this.print = function () {
            var s = '\n'
            for(var i=0;i<vertices.length;i++){
                var dingdian = vertices[i]
                s += dingdian + '====>'
                for(var j=0;j<adjList[dingdian].length;j++){

                    s+=adjList[dingdian][j]+ '\t'
                }
                s+= '\n'
            }
            console.log(s)
        }

    }
```

##### 在上面广度优先遍历的基础上，寻找最短路径，代码如下：

```javascript
        // 寻找路径的两个重要点是： 两个点之间的距离和回溯点
        // 寻找最短路径
        //d: 距离值
        //pred: 回溯点

        this.BFS = function (value,callback) {
            // 新建一个队列， 队列的在此的作用就是保证广度优先遍历，因为队列的特性：先进先出
            var queue = new Queue()
            // 一开始所有的点都是未发现的   用 white 表示
            var color = initColor()
            // 一旦入列后，标记为   已发现未探索  用 grey 表示
            queue.enqueue(value)

            var d = {}
            var pred = {}

            for(var i=0;i<vertices.length;i++){
                var dindian = vertices[i]
                d[dindian] = 0
                pred[dindian] = null
            }
            console.log(d,pred)

            // 接下来要 将队列中的数据拿出来，进行探索
            // 如果队列不为空，就可继续执行

            while(!queue.isEmpty()){
                var now = queue.dequeue()
                var edges = adjList[now]   //顶点对应的所有边
                for(var i=0;i<edges.length;i++){
                    var w = edges[i]
                    if(color[w] === 'white'){
                        //未发现的全部入列，并标记为已发现
                        queue.enqueue(w)
                        color[w] = 'grey'
                        // 此时可以知道该点的回溯点是 now
                        pred[w] = now
                        d[w] = d[now]+ 1
                    }
                }
                color[now] = 'black'  //表示已探索
                if(callback){
                    callback(now)
                }
            }
            return {
                pred: pred,
                d: d
            }
        }
//构造函数外部进行测试
 var zuiduan = function (from,to) {

        var v = to  //设置当前点

        var path = new Stack()  // 使用栈结构  主要是为了让数据正向显示
        while(v !== from){
            path.push(v)
            v = pred[v]
        }
        path.push(v)
        var str = ''
        while(!path.isEmpty()){
            str+=path.pop()+ '-'
        }
        str = str.slice(0,str.length-1)
        console.log(str)

    }
    zuiduan('A','F')  // A-B-F
```

#### 深度优先遍历    核心思想： 使用递归

```javascript
 // 深度优先算法的递归函数
        var dfsVisite = function (u,color,callback) {
            color[u] = 'grey'
            var n = adjList[u]
            for(var i=0;i<n.length;i++){
                var w = n[i]
                if(color[w] === 'white'){
                    dfsVisite(w,color,callback)
                }
            }
            color[u] = 'black'
            if(callback){
                callback(u)
            }
        }
        //深度优先算法
        this.dfs = function (v,callback) {
            var color = initColor()
            dfsVisite(v,color,callback)
        }
```





