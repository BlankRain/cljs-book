
可变状态
----

数据是不可变的, 但是通过引用实现的状态是可以改变的.

### Atom

Atom 在 Clojure 中可以用于处理事务操作, cljs 由于是单线程, 玩不转.
不过 Atom 还是用于表示单个同步的状态修改, 用法一般是:

```clojure
(def *a (atom 1))
@*a
(reset! *a 2)
(swap! *a inc)
```

`swap!` 实际上是一个 Macro, 应对 `(reset! *a (inc @a))`.

Atom 类型的数据可以被监听, 在修改时调用代码:

```clojure
(defn handle-change []
  (println "changed"))
(add-watch *a :changes handle-change)
(remove-watch *a :changes)
```

### 宿主语言

另一种模拟可变数据的方式是通过宿主语言的类型系统来提供可变数据.
