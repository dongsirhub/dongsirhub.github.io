# 16、synchronized 和 volatile 有什么区别

l volatile 本质是告诉JVM 当前变量在寄存器中的值是不确定的，需要从主存中读取，synchronized 则是锁定当前变量，只有当前线程可以访问该变量，其他线程被阻塞住。

l volatile 仅能用在变量级别，而synchronized 可以使用在变量、方法、类级别。

l volatile 仅能实现变量的修改可见性，不能保证原子性；而synchronized 则可以保证变量的修改可见性和原子性。

l volatile 不会造成线程阻塞，synchronized 可能会造成线程阻塞。

l volatile 标记的变量不会被编译器优化，synchronized 标记的变量可以被编译器优化。

> 更新: 2024-04-30 18:35:15  
