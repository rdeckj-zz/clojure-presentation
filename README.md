# clojure-presentation
Notes for an introductory presentation of Clojure

## The Basics
### Clojure: A Lisp

Clojure runs on the JVM, and the Clojure compiler is an executable JAR (`clojure.jar`). Clojure code can also run on the web (ClojureScript) and utilize the Microsoft Common Language Runtime (CLR).

### Setup

1. Install Java
2. Install [Leiningen](https://leiningen.org/)
3. Create a project via `lein new app <app-name>`
4. Run your project from the directory via `lein run`

You should see "Hello, World" output in the terminal.

### The REPL
Start a REPL via `lein repl`

```
(+ 1 2)
=> 3

(println "Hello")
=> Hello
=> nil
```

### IDE Options

[Cursive](https://cursive-ide.com/) (IntelliJ Plugin)

[Nightcode](https://sekao.net/nightcode/)

Emacs

### Resources
[Clojure For The Brave And True](https://www.braveclojure.com)

[Official Clojure Site](https://clojure.org/)

[Clojure Docs](https://clojuredocs.org)

## Code

### Operations
All operations take the form of: `(<operator> <operands>)`

```
(+ 7 8 9)
=> 24

(str "Clojure is " "awesome")
=> "Clojure is awesome"

(= true false)
=> false
```

### Conditionals

#### `if` and `do`
```
(if true
"Electric Boogaloo"
"Nope")
=> "Electric Boogaloo"

(if false
"Whatever")
=> nil

(if true
  (do (println "Wrapping forms")
      "Return this")
  (do (println "Meh")
      "This won't return anyway"))
=> Wrapping forms
=> "Return this"
```

#### `when`

```
(when true
  (println "This")
  (println "That")
  "The other thing")
=> This
=> That
"The other thing"
```

### Equality

#### `nil`
```
(nil? 12)
=> false

(nil? nil)
=> true
```

#### Truthy / Falsey
```
(if "a string"
  "Yep, it's a string")
=> "Yep, it's a string"

(if nil
  "Hi"
  "Nil is falsey")
```

#### `or` and `and`

`or` returns the first truthy value or the last value
`and` returns the first falsey value or the last truthy value
```
(or false nil "hello!" false)
=> "hello!"

(and "one" "two" false "three")
=> false
```

### def and defn
```
(def x 1) 
=> #'user/x

(+ x x)
=> 2

(defn add-one
  [value]
  (+ value 1))
=> #'user/add-one

(add-one 10)
=> 11
```

### Collections

#### `maps`
```
(def first-pres {:first "George" :last "Washington})
=> #`user/first-pres

(get first-pres :first)
=> "George"

(get first-pres :middle "Walter")
=> "Walter"
```

#### `Vectors`
```
(get [4 5 6] 0)
=> 4

(get (get [{:first "George" :last "Washington"} {:first "John" :last "Adams"}] 0) :first)
=> "George"
```

#### `Lists`
```
`(1 2 3 4)
=> (1 2 3 4)

(nth `("Lions" "Tigers" "Bears") 1)
=> "Tigers"

(conj `(1 2 3) 4)
=> (4 1 2 3)
```

#### `Sets`
```
(hash-set 1 1 2 2)
=> #{1 2} 

(= (hash-set 1 2 3) #{1 2 3})
=> true

(conj #{1 2} 2)
=> #{1 2}
```

### Anonymous Functions
```
(map (fn [person] (str "Hello, " person))["George" "John"])
=> ("Hello, George" "Hello, John")

(map #(str "Hello, " %) ["George" "John"])
=> ("Hello, George" "Hello, John")
```

### Clojures
```
(defn inc-maker
  [inc-by]
  #(+ % inc-by))
=> #`user/inc-maker

(def inc10 (inc-maker 10))
=> #`user/inc10

(inc10 10)
=> 20
```