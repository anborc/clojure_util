# clojure_util
To make coding more fluently by only using parentheses

```
(ns util.core)

(defmacro defun
  [fun str arg & body]
  (if (or (string? str) (symbol? str))
    `(defn ~fun ~str [~@arg] ~@body)
    `(defn ~fun [~@str] ~arg ~@body)))
    
;;(defun foox (x y) (+ x y))
;;(defun foox2 "hello" (x y) (+ x y))
;;(defun ^:export init () (println "hello"))

(defmacro for>
  [arg body]
  `(for [~@arg] ~body))

;;(for> (a '(:mouse :duck :lory) c '(:red :blue)
;;        :when (= c :blue))
;;  (str (name c) "-" (name a)))

(defmacro lambda [arg & body]
  `(fn [~@arg] ~@body))

(defmacro fun [arg & body]
  `(fn [~@arg] ~@body))

(defmacro dotimes> [arg & body]
  `(dotimes [~@arg] ~@body))

(defmacro let- [arg & body]
  `(let [~@arg] ~@body))

(defmacro let> [arg & body]
  `(let [~@arg] ~@body))

;;(let> ([color size] '("blue" "small")) (str "the " color " door is " size))
;;(let> ({:keys (v- flower1 flower2)} (m- :flower1 "red" :flower2 "blue")) (str "The flowers are " flower1 " and " flower2))

(defmacro v-
  [& items]
  `(vector ~@items))

(defmacro v>
  [& items]
  `(vector ~@items))

(defmacro m-
  [& items]
  `(hash-map ~@items))

(defmacro m>
  [& items]
  `(hash-map ~@items))

(defmacro s-
  [& items]
  `(set (list ~@items)))

(defmacro s>
  [& items]
  `(set (list ~@items)))

(defmacro car
  [seq]
  `(first ~seq))

(defmacro cdr
  [seq]
  `(rest ~seq))

;;State Management
(defn setf [var val]
  (cond
    (instance? clojure.lang.Ref var) (dosync (ref-set var val))
    (instance? clojure.lang.Atom var) (reset! var val)
    (instance? clojure.lang.Agent var) (send var (fn [x] val))))
```


