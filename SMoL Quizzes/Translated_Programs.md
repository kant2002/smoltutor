# Quiz 1

<h2>
arithmetic operators
</h2>
<table>
<tr>
<th>
SMoL
</th>
<th>
JavaScript
</th>
<th>
Python
</th>
</tr>
<tr>
<td>
<pre>(deffun (f o) (o 1 1))
(f +)</pre>
</td>
<td>
<pre>function f(o) {
  return o(1, 1);
}
console.log(f((function(x, y) { return x + y; })));</pre>
</td>
<td>
<pre>def f(o):
    return o(1, 1)
print(f(+))</pre>
</td>
</tr>
</table>
<h2>
0 as condition
</h2>
<table>
<tr>
<th>
SMoL
</th>
<th>
JavaScript
</th>
<th>
Python
</th>
</tr>
<tr>
<td>
<pre>(if 0 #t #f)</pre>
</td>
<td>
<pre>console.log((0 ? true : false));</pre>
</td>
<td>
<pre>print(True if 0 else False)</pre>
</td>
</tr>
</table>
<h2>
redeclare var using defvar
</h2>
<table>
<tr>
<th>
SMoL
</th>
<th>
JavaScript
</th>
<th>
Python
</th>
</tr>
<tr>
<td>
<pre>(defvar x 0)
(defvar y x)
(defvar x 2)
x
y</pre>
</td>
<td>
<pre>let x = 0;
let y = x;
let x = 2;
console.log(x);
console.log(y);</pre>
</td>
<td>
<pre>x = 0
y = x
x = 2
print(x)
print(y)</pre>
</td>
</tr>
</table>
<h2>
expose local defvar
</h2>
<table>
<tr>
<th>
SMoL
</th>
<th>
JavaScript
</th>
<th>
Python
</th>
</tr>
<tr>
<td>
<pre>(defvar x 42)
(deffun (create)
  (defvar y 42)
  y)
(create)
(equal? x y)</pre>
</td>
<td>
<pre>let x = 42;
function create() {
  let y = 42;
  return y;
}
console.log(create());
console.log(x === y);</pre>
</td>
<td>
<pre>x = 42
def create():
    y = 42
    return y
print(create())
print(x == y)</pre>
</td>
</tr>
</table>
<h2>
pair?
</h2>
<table>
<tr>
<th>
SMoL
</th>
<th>
JavaScript
</th>
<th>
Python
</th>
</tr>
<tr>
<td>
<pre>(pair? (pair 1 2))
(pair? (ivec 1 2))
(pair? '#(1 2))
(pair? '(1 2))</pre>
</td>
<td>
<pre>N/A</pre>
</td>
<td>
<pre>N/A</pre>
</td>
</tr>
</table>
<h2>
let* and let
</h2>
<table>
<tr>
<th>
SMoL
</th>
<th>
JavaScript
</th>
<th>
Python
</th>
</tr>
<tr>
<td>
<pre>(let* ([v 1]
       [w (+ v 2)]
       [y (* w w)])
  (let ([v 3]
        [y (* v w)])
    y))</pre>
</td>
<td>
<pre>console.log(((v)=>{return ((w)=>{return ((y)=>{return ((v, y)=>{return y;})(3, v * w);})(w * w);})(v + 2);})(1));</pre>
</td>
<td>
<pre>N/A</pre>
</td>
</tr>
</table>
<h2>
defvar and let
</h2>
<table>
<tr>
<th>
SMoL
</th>
<th>
JavaScript
</th>
<th>
Python
</th>
</tr>
<tr>
<td>
<pre>(defvar x 3)
(defvar y (let ([y 6] [x 5]) x))
(* x y)</pre>
</td>
<td>
<pre>let x = 3;
let y = ((y, x)=>{return x;})(6, 5);
console.log(x * y);</pre>
</td>
<td>
<pre>N/A</pre>
</td>
</tr>
</table>
<h2>
fun-id equals to arg-id
</h2>
<table>
<tr>
<th>
SMoL
</th>
<th>
JavaScript
</th>
<th>
Python
</th>
</tr>
<tr>
<td>
<pre>(deffun (f f) f)
(f 5)</pre>
</td>
<td>
<pre>function f(f) {
  return f;
}
console.log(f(5));</pre>
</td>
<td>
<pre>def f(f):
    return f
print(f(5))</pre>
</td>
</tr>
</table>
<h2>
scoping rule of let
</h2>
<table>
<tr>
<th>
SMoL
</th>
<th>
JavaScript
</th>
<th>
Python
</th>
</tr>
<tr>
<td>
<pre>(let ([x 4]
      [y (+ x 10)])
  y)</pre>
</td>
<td>
<pre>console.log(((x, y)=>{return y;})(4, x + 10));</pre>
</td>
<td>
<pre>N/A</pre>
</td>
</tr>
</table>
<h2>
the right component of ivec
</h2>
<table>
<tr>
<th>
SMoL
</th>
<th>
JavaScript
</th>
<th>
Python
</th>
</tr>
<tr>
<td>
<pre>(right (ivec 1 2 3))</pre>
</td>
<td>
<pre>console.log(ivec(1, 2, 3)[1]);</pre>
</td>
<td>
<pre>print(ivec(1, 2, 3)[1])</pre>
</td>
</tr>
</table>
<h2>
identifiers
</h2>
<table>
<tr>
<th>
SMoL
</th>
<th>
JavaScript
</th>
<th>
Python
</th>
</tr>
<tr>
<td>
<pre>(defvar x 5)
(deffun (reassign var_name new_val)
  (defvar var_name new_val)
  (pair var_name x))
(reassign x 6)
x</pre>
</td>
<td>
<pre>let x = 5;
function reassign(var_name, new_val) {
  let var_name = new_val;
  return [ var_name, x ];
}
console.log(reassign(x, 6));
console.log(x);</pre>
</td>
<td>
<pre>x = 5
def reassign(var_name, new_val):
    var_name = new_val
    return [ var_name, x ]
print(reassign(x, 6))
print(x)</pre>
</td>
</tr>
</table>
<h2>
defvar, deffun, and let
</h2>
<table>
<tr>
<th>
SMoL
</th>
<th>
JavaScript
</th>
<th>
Python
</th>
</tr>
<tr>
<td>
<pre>(defvar a 1)
(deffun (what-is-a) a)
(let ([a 2])
  (ivec
   (what-is-a)
   a))</pre>
</td>
<td>
<pre>let a = 1;
function whatIsA() {
  return a;
}
console.log(((a)=>{return ivec(whatIsA(), a);})(2));</pre>
</td>
<td>
<pre>N/A</pre>
</td>
</tr>
</table>
<h2>
syntax pitfall
</h2>
<table>
<tr>
<th>
SMoL
</th>
<th>
JavaScript
</th>
<th>
Python
</th>
</tr>
<tr>
<td>
<pre>(deffun (f a b) a + b)
(f 5 10)</pre>
</td>
<td>
<pre>function f(a, b) {
  a;
  (function(x, y) { return x + y; });
  return b;
}
console.log(f(5, 10));</pre>
</td>
<td>
<pre>def f(a, b):
    a
    +
    return b
print(f(5, 10))</pre>
</td>
</tr>
</table>
<h1 id="quiz-2">Quiz 2</h1>
<h2>
circularity
</h2>
<table>
<tr>
<th>
SMoL
</th>
<th>
JavaScript
</th>
<th>
Python
</th>
</tr>
<tr>
<td>
<pre>(defvar x (mvec 2 3))
(set-right! x x)
(set-left! x x)
x</pre>
</td>
<td>
<pre>let x = [ 2, 3 ];
console.log(x[1]=x);
console.log(x[0]=x);
console.log(x);</pre>
</td>
<td>
<pre>x = [2, 3]
x[1] = x
x[0] = x
print(x)</pre>
</td>
</tr>
</table>
<h2>
eval order
</h2>
<table>
<tr>
<th>
SMoL
</th>
<th>
JavaScript
</th>
<th>
Python
</th>
</tr>
<tr>
<td>
<pre>(defvar x 0)
(ivec x (begin (set! x 1) x) x)</pre>
</td>
<td>
<pre>let x = 0;
console.log(ivec(x, (x = 1, x), x));</pre>
</td>
<td>
<pre>x = 0
print(ivec(x, [x := 1, x][-1], x))</pre>
</td>
</tr>
</table>
<h2>
mvec as arg
</h2>
<table>
<tr>
<th>
SMoL
</th>
<th>
JavaScript
</th>
<th>
Python
</th>
</tr>
<tr>
<td>
<pre>(defvar x (mvec 1 2))
(deffun (f x)
  (vset! x 0 0))
(f x)
x</pre>
</td>
<td>
<pre>let x = [ 1, 2 ];
function f(x) {
  return x[0] = 0;
}
console.log(f(x));
console.log(x);</pre>
</td>
<td>
<pre>x = [1, 2]
def f(x):
    return x.__setitem__(0, 0)
print(f(x))
print(x)</pre>
</td>
</tr>
</table>
<h2>
var as arg
</h2>
<table>
<tr>
<th>
SMoL
</th>
<th>
JavaScript
</th>
<th>
Python
</th>
</tr>
<tr>
<td>
<pre>(defvar x 12)
(deffun (f x)
  (set! x 0))
(f x)
x</pre>
</td>
<td>
<pre>let x = 12;
function f(x) {
  return x = 0;
}
console.log(f(x));
console.log(x);</pre>
</td>
<td>
<pre>x = 12
def f(x):
    return (x := 0)
print(f(x))
print(x)</pre>
</td>
</tr>
</table>
<h2>
seemly aliasing a var
</h2>
<table>
<tr>
<th>
SMoL
</th>
<th>
JavaScript
</th>
<th>
Python
</th>
</tr>
<tr>
<td>
<pre>(defvar x 5)
(deffun (set1 x y)
  (set! x y))
(deffun (set2 a y)
  (set! x y))
(set1 x 6)
x
(set2 x 7)
x</pre>
</td>
<td>
<pre>let x = 5;
function set1(x, y) {
  return x = y;
}
function set2(a, y) {
  return x = y;
}
console.log(set1(x, 6));
console.log(x);
console.log(set2(x, 7));
console.log(x);</pre>
</td>
<td>
<pre>x = 5
def set1(x, y):
    return (x := y)
def set2(a, y):
    global x
    return (x := y)
print(set1(x, 6))
print(x)
print(set2(x, 7))
print(x)</pre>
</td>
</tr>
</table>
<h2>
mutable var in vec
</h2>
<table>
<tr>
<th>
SMoL
</th>
<th>
JavaScript
</th>
<th>
Python
</th>
</tr>
<tr>
<td>
<pre>(defvar x 3)
(defvar v (mvec 1 2 x))
(set! x 4)
v
x</pre>
</td>
<td>
<pre>let x = 3;
let v = [ 1, 2, x ];
x = 4;
console.log(v);
console.log(x);</pre>
</td>
<td>
<pre>x = 3
v = [1, 2, x]
x = 4
print(v)
print(x)</pre>
</td>
</tr>
</table>
<h2>
aliasing mvec in mvec
</h2>
<table>
<tr>
<th>
SMoL
</th>
<th>
JavaScript
</th>
<th>
Python
</th>
</tr>
<tr>
<td>
<pre>(defvar v (mvec 1 2 3 4))
(defvar vv (mvec v v))(vset! (vref vv 1) 0 100)
vv</pre>
</td>
<td>
<pre>let v = [ 1, 2, 3, 4 ];
let vv = [ v, v ];
vv[1][0] = 100;
console.log(vv);</pre>
</td>
<td>
<pre>v = [1, 2, 3, 4]
vv = [v, v]
vv[1][0] = 100
print(vv)</pre>
</td>
</tr>
</table>
<h2>
vset! in let
</h2>
<table>
<tr>
<th>
SMoL
</th>
<th>
JavaScript
</th>
<th>
Python
</th>
</tr>
<tr>
<td>
<pre>(defvar x (mvec 123))
(let ([y x])
  (vset! y 0 10))
x</pre>
</td>
<td>
<pre>let x = [ 123 ];
console.log(((y)=>{return y[0] = 10;})(x));
console.log(x);</pre>
</td>
<td>
<pre>N/A</pre>
</td>
</tr>
</table>
<h2>
set! in let
</h2>
<table>
<tr>
<th>
SMoL
</th>
<th>
JavaScript
</th>
<th>
Python
</th>
</tr>
<tr>
<td>
<pre>(defvar x 123)
(let ([y x])
  (set! y 10))
x</pre>
</td>
<td>
<pre>let x = 123;
console.log(((y)=>{return y = 10;})(x));
console.log(x);</pre>
</td>
<td>
<pre>N/A</pre>
</td>
</tr>
</table>
<h2>
seemingly aliasing a var again
</h2>
<table>
<tr>
<th>
SMoL
</th>
<th>
JavaScript
</th>
<th>
Python
</th>
</tr>
<tr>
<td>
<pre>(defvar x 10)
(deffun (f y z)
  (set! x z)
  y)
(f x 20)
x</pre>
</td>
<td>
<pre>let x = 10;
function f(y, z) {
  x = z;
  return y;
}
console.log(f(x, 20));
console.log(x);</pre>
</td>
<td>
<pre>x = 10
def f(y, z):
    global x
    x = z
    return y
print(f(x, 20))
print(x)</pre>
</td>
</tr>
</table>
<h1 id="quiz-3">Quiz 3</h1>
<h2>
fun returns lambda
</h2>
<table>
<tr>
<th>
SMoL
</th>
<th>
JavaScript
</th>
<th>
Python
</th>
</tr>
<tr>
<td>
<pre>(deffun (f x)
  (lambda (y) (+ x y)))
((f 2) 1)</pre>
</td>
<td>
<pre>function f(x) {
  return function (y) {
    return x + y;
  };
}
console.log(f(2)(1));</pre>
</td>
<td>
<pre>def f(x):
    return lambda y: x + y
print(f(2)(1))</pre>
</td>
</tr>
</table>
<h2>
filter gt
</h2>
<table>
<tr>
<th>
SMoL
</th>
<th>
JavaScript
</th>
<th>
Python
</th>
</tr>
<tr>
<td>
<pre>(filter (lambda (n) (> 3 n)) '(1 2 3 4 5))</pre>
</td>
<td>
<pre>N/A</pre>
</td>
<td>
<pre>N/A</pre>
</td>
</tr>
</table>
<h2>
fun and state 1/4
</h2>
<table>
<tr>
<th>
SMoL
</th>
<th>
JavaScript
</th>
<th>
Python
</th>
</tr>
<tr>
<td>
<pre>(defvar x 1)
(defvar f
  (lambda (y)
    (+ x y)))
(set! x 2)
(f x)</pre>
</td>
<td>
<pre>let x = 1;
let f = function (y) {
  return x + y;
};
x = 2;
console.log(f(x));</pre>
</td>
<td>
<pre>x = 1
f = lambda y: x + y
x = 2
print(f(x))</pre>
</td>
</tr>
</table>
<h2>
fun and state 2/4
</h2>
<table>
<tr>
<th>
SMoL
</th>
<th>
JavaScript
</th>
<th>
Python
</th>
</tr>
<tr>
<td>
<pre>(defvar x 1)
(deffun (f y)
  (+ x y))
(set! x 2)
(f x)</pre>
</td>
<td>
<pre>let x = 1;
function f(y) {
  return x + y;
}
x = 2;
console.log(f(x));</pre>
</td>
<td>
<pre>x = 1
def f(y):
    return x + y
x = 2
print(f(x))</pre>
</td>
</tr>
</table>
<h2>
fun and state 3/4
</h2>
<table>
<tr>
<th>
SMoL
</th>
<th>
JavaScript
</th>
<th>
Python
</th>
</tr>
<tr>
<td>
<pre>(defvar x 1)
(defvar f
  (lambda (y)
    (+ x y)))
(let ([x 2])
  (f x))</pre>
</td>
<td>
<pre>let x = 1;
let f = function (y) {
  return x + y;
};
console.log(((x)=>{return f(x);})(2));</pre>
</td>
<td>
<pre>N/A</pre>
</td>
</tr>
</table>
<h2>
fun and state 4/4
</h2>
<table>
<tr>
<th>
SMoL
</th>
<th>
JavaScript
</th>
<th>
Python
</th>
</tr>
<tr>
<td>
<pre>(defvar x 1)
(deffun (f y)
  (+ x y))
(let ([x 2])
  (f x))</pre>
</td>
<td>
<pre>let x = 1;
function f(y) {
  return x + y;
}
console.log(((x)=>{return f(x);})(2));</pre>
</td>
<td>
<pre>N/A</pre>
</td>
</tr>
</table>
<h2>
eval order
</h2>
<table>
<tr>
<th>
SMoL
</th>
<th>
JavaScript
</th>
<th>
Python
</th>
</tr>
<tr>
<td>
<pre>(deffun (f x) (+ x 1))
(deffun (new-f x) (* x x))
(f (begin
     (set! f new-f)
     10))</pre>
</td>
<td>
<pre>function f(x) {
  return x + 1;
}
function newF(x) {
  return x * x;
}
console.log(f((f = newF, 10)));</pre>
</td>
<td>
<pre>def f(x):
    return x + 1
def new_f(x):
    return x * x
print(f([f := new_f, 10][-1]))</pre>
</td>
</tr>
</table>
<h2>
Counter
</h2>
<table>
<tr>
<th>
SMoL
</th>
<th>
JavaScript
</th>
<th>
Python
</th>
</tr>
<tr>
<td>
<pre>(deffun (make-counter)
  (let ([count 0])
    (lambda ()
      (begin
        (set! count (+ count 1))
        count))))
(defvar f (make-counter))
(defvar g (make-counter))
(f)
(g)
(f)
(f)
(g)</pre>
</td>
<td>
<pre>function makeCounter() {
  return ((count)=>{return function () {
    return (count = count + 1, count);
  };})(0);
}
let f = makeCounter();
let g = makeCounter();
console.log(f());
console.log(g());
console.log(f());
console.log(f());
console.log(g());</pre>
</td>
<td>
<pre>N/A</pre>
</td>
</tr>
</table>
<h2>
hof + set!
</h2>
<table>
<tr>
<th>
SMoL
</th>
<th>
JavaScript
</th>
<th>
Python
</th>
</tr>
<tr>
<td>
<pre>(defvar y 3)
(+ ((lambda (x) (set! y 0) (+ x y)) 1)
   y)</pre>
</td>
<td>
<pre>let y = 3;
console.log(function (x) {
  y = 0;
  return x + y;
}(1) + y);</pre>
</td>
<td>
<pre>y = 3
print(lambda x: ("WARNING: the translation might be inaccurate", (y := 0, x + y)[-1])[-1](1) + y)</pre>
</td>
</tr>
</table>
<h2>
filter
</h2>
<table>
<tr>
<th>
SMoL
</th>
<th>
JavaScript
</th>
<th>
Python
</th>
</tr>
<tr>
<td>
<pre>(defvar l (list (ivec) (ivec 1) (ivec 2 3)))
(filter (lambda (x) (vlen x)) l)</pre>
</td>
<td>
<pre>let l = list(ivec(), ivec(1), ivec(2, 3));
console.log(filter(function (x) {
  return x.length;
}, l));</pre>
</td>
<td>
<pre>l = list(ivec(), ivec(1), ivec(2, 3))
print(filter(lambda x: len(x), l))</pre>
</td>
</tr>
</table>
<h2>
eq? fun fun 1/3
</h2>
<table>
<tr>
<th>
SMoL
</th>
<th>
JavaScript
</th>
<th>
Python
</th>
</tr>
<tr>
<td>
<pre>(eq? (λ (x) (+ x x))
     (λ (x) (+ x x)))</pre>
</td>
<td>
<pre>console.log(λ(x(), x + x) === λ(x(), x + x));</pre>
</td>
<td>
<pre>print(λ(x(), x + x) == λ(x(), x + x))</pre>
</td>
</tr>
</table>
<h2>
eq? fun fun 2/3
</h2>
<table>
<tr>
<th>
SMoL
</th>
<th>
JavaScript
</th>
<th>
Python
</th>
</tr>
<tr>
<td>
<pre>(deffun (f x) (+ x x))
(deffun (g x) (+ x x))
(eq? f g)</pre>
</td>
<td>
<pre>function f(x) {
  return x + x;
}
function g(x) {
  return x + x;
}
console.log(f === g);</pre>
</td>
<td>
<pre>def f(x):
    return x + x
def g(x):
    return x + x
print(f == g)</pre>
</td>
</tr>
</table>
<h2>
eq? fun fun 3/3
</h2>
<table>
<tr>
<th>
SMoL
</th>
<th>
JavaScript
</th>
<th>
Python
</th>
</tr>
<tr>
<td>
<pre>(deffun (f x) (+ x x))
(deffun (g) f)
(eq? f (g))</pre>
</td>
<td>
<pre>function f(x) {
  return x + x;
}
function g() {
  return f;
}
console.log(f === g());</pre>
</td>
<td>
<pre>def f(x):
    return x + x
def g():
    return f
print(f == g())</pre>
</td>
</tr>
</table>
<h2>
equal? fun fun
</h2>
<table>
<tr>
<th>
SMoL
</th>
<th>
JavaScript
</th>
<th>
Python
</th>
</tr>
<tr>
<td>
<pre>(deffun (f) (lambda () 1))
(equal? (f) (f))</pre>
</td>
<td>
<pre>function f() {
  return function () {
    return 1;
  };
}
console.log(f() === f());</pre>
</td>
<td>
<pre>def f():
    return lambda: 1
print(f() == f())</pre>
</td>
</tr>
</table>
