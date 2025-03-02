# 14、ConcurrentHashMap 底层原理

<font style="color:rgb(0,111,192);">Java7 中ConcurrentHashMap 使用的分段锁，也就是每一个Segment 上同时只有一个线程可以操作，每一个Segment 都是一个类似HashMap 数组的结构，它可以扩容，它的冲突会转化为链表。但是Segment 的个数一但初始化就不能改变。</font>

```java
public V put(K key, V value) {
 Segment<K,V> s;
if (value == null)
throw new NullPointerException(); int hash = hash(key);
// hash 值无符号右移 28 位（初始化时获得），然后与 segmentMask=15 做与运
算
// 其实也就是把高 4 位与segmentMask（1111）做与运算
// this.segmentMask = ssize - 1;
//对hash 值进行右移segmentShift 位，计算元素对应segment 中数组下表的位置
//把hash 右移segmentShift，相当于只要hash 值的高 32-segmentShift 位，右移的目的是保留了hash 值的高位。然后和segmentMask 与操作计算元素在 segment 数组中的下表
int j = (hash >>> segmentShift) & segmentMask;
//使用unsafe 对象获取数组中第j 个位置的值，后面加上的是偏移量
if ((s = (Segment<K,V>)UNSAFE.getObject	// nonvolatile; recheck (segments, (j << SSHIFT) + SBASE)) == null) // in ensureSegment
// 如果查找到的 Segment 为空，初始化 s = ensureSegment(j);
//插入segment 对象
return s.put(key, hash, value, false);
}

/**
*Returns the segment for the given index, creating it and
*recording in segment table (via CAS) if not already present.
*
*@param  k the index 
*@return  the segment 
*/ @SuppressWarnings("unchecked")
private Segment<K,V> ensureSegment(int k) { final Segment<K,V>[] ss = this.segments;
long u = (k << SSHIFT) + SBASE; // raw offset Segment<K,V> seg;
// 判断 u 位置的 Segment 是否为null
if ((seg = (Segment<K,V>)UNSAFE.getObjectVolatile(ss, u)) == null) { Segment<K,V> proto = ss[0]; // use segment 0 as prototype
// 获取 0 号 segment 里的 HashEntry<K,V> 初始化长度 int cap = proto.table.length;
// 获取 0 号 segment 里的 hash 表里的扩容负载因子，所有的 segment 的 loadFactor 是相同的
float lf = proto.loadFactor;
// 计算扩容阀值
int threshold = (int)(cap * lf);
// 创建一个 cap 容量的 HashEntry 数组
HashEntry<K,V>[] tab = (HashEntry<K,V>[])new HashEntry[cap];
if ((seg = (Segment<K,V>)UNSAFE.getObjectVolatile(ss, u)) == null) { // recheck了操作
// 再次检查 u 位置的 Segment 是否为null，因为这时可能有其他线程进行
Segment<K,V> s = new Segment<K,V>(lf, threshold, tab);
// 自旋检查 u 位置的 Segment 是否为null
while ((seg = (Segment<K,V>)UNSAFE.getObjectVolatile(ss, u))
== null) {
// 使用CAS 赋值，只会成功一次
if (UNSAFE.compareAndSwapObject(ss, u, null, seg = s)) break;
}
}
}
return seg;
}

final V put(K key, int hash, V value, boolean onlyIfAbsent) {
// 获取 ReentrantLock 独占锁，获取不到，scanAndLockForPut 获取。HashEntry<K,V> node = tryLock() ? null : scanAndLockForPut(key, hash,
value);
V oldValue; try {
HashEntry<K,V>[] tab = table;
// 计算要put 的数据位置
int index = (tab.length - 1) & hash;
// CAS 获取 index 坐标的值 HashEntry<K,V> first = entryAt(tab, index); for (HashEntry<K,V> e = first;;) {
if (e != null) {
// 检查是否 key 已经存在，如果存在，则遍历链表寻找位置，找到后替
换 value

K k;
if ((k = e.key) == key ||
(e.hash == hash && key.equals(k))) { oldValue = e.value;
if (!onlyIfAbsent) { e.value = value;
++modCount;
}
break;
}
e = e.next;
}

的表头

else {
// first 有值没说明 index 位置已经有值了，有冲突，链表头插法。 if (node != null)
node.setNext(first); else
node = new HashEntry<K,V>(hash, key, value, first); int c = count + 1;
// 容量大于扩容阀值，小于最大容量，进行扩容
if (c > threshold && tab.length < MAXIMUM_CAPACITY) rehash(node);
else
// index 位置赋值 node，node 可能是一个元素，也可能是一个链表
setEntryAt(tab, index, node);
++modCount; count = c; oldValue = null; break;
}
}
} finally {
unlock();
}
return oldValue;
}
1. Java8 中的ConcurrentHashMap 使用的Synchronized 锁加CAS 的机制。结构Node 数组+ 链表/ 红黑树，Node 是类似于一个HashEntry 的结构。它的冲突再达到一定大小时会转化成红黑树，在冲突小于一定数量时又退回链表。
public V put(K key, V value) { return putVal(key, value, false);
}

/** Implementation for put and putIfAbsent */
final V putVal(K key, V value, boolean onlyIfAbsent) {
// key 和 value 不能为空
if (key == null || value == null) throw new NullPointerException(); int hash = spread(key.hashCode());
int binCount = 0;
for (Node<K,V>[] tab = table;;) {
// f = 目标位置元素
Node<K,V> f; int n, i, fh;// fh 后面存放目标位置的元素 hash 值if (tab == null || (n = tab.length) == 0)
// 数组桶为空，初始化数组桶（自旋+CAS) tab = initTable();
else if ((f = tabAt(tab, i = (n - 1) & hash)) == null) {
// 桶内为空，CAS 放入，不加锁，成功了就直接break 跳出
if (casTabAt(tab, i, null,new Node<K,V>(hash, key, value, null))) break; // no lock when adding to empty bin
}
else if ((fh = f.hash) == MOVED) tab = helpTransfer(tab, f);
else {public V put(K key, V value) { return putVal(key, value, false);
}

/** Implementation for put and putIfAbsent */
final V putVal(K key, V value, boolean onlyIfAbsent) {
// key 和 value 不能为空
if (key == null || value == null) throw new NullPointerException(); int hash = spread(key.hashCode());
int binCount = 0;
for (Node<K,V>[] tab = table;;) {
// f = 目标位置元素
Node<K,V> f; int n, i, fh;// fh 后面存放目标位置的元素 hash 值if (tab == null || (n = tab.length) == 0)
// 数组桶为空，初始化数组桶（自旋+CAS) tab = initTable();
else if ((f = tabAt(tab, i = (n - 1) & hash)) == null) {
// 桶内为空，CAS 放入，不加锁，成功了就直接break 跳出
if (casTabAt(tab, i, null,new Node<K,V>(hash, key, value, null))) break; // no lock when adding to empty bin
}
else if ((fh = f.hash) == MOVED) tab = helpTransfer(tab, f);
else {}
}
}
}
if (binCount != 0) {
if (binCount >= TREEIFY_THRESHOLD) treeifyBin(tab, i);
if (oldVal != null) return oldVal;
break;
}
}
}
addCount(1L, binCount); return null;
}
```





> 更新: 2024-04-30 18:33:54  
> [原文](https://www.yuque.com/zhichangzhishiku/edrbqg/mgei2d6l3s2bz6h0>