## scope1::warmup_defvar
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
(defvar y (+ x 2))
x
y</pre>
</td>
<td>
<pre>let x = 1;
let y = x + 2;
console.log(x);
console.log(y);</pre>
</td>
<td>
<pre>x = 1
y = x + 2
print(x)
print(y)</pre>
</td>
</tr>
</table>

## scope1::warmup_error

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
<pre>(defvar xyz 173)
abc</pre>
</td>
<td>
<pre>let xyz = 173;
console.log(abc);</pre>
</td>
<td>
<pre>xyz = 173
print(abc)</pre>
</td>
</tr>
</table>

## scope1::warmup_fun

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
<pre>(deffun (sum x y z)
  (+ x (+ y z)))
(sum 2 1 3)</pre>
</td>
<td>
<pre>function sum(x, y, z) {
  return x + (y + z);
}
console.log(sum(2, 1, 3));</pre>
</td>
<td>
<pre>def sum(x, y, z):
    return x + (y + z)
print(sum(2, 1, 3))</pre>
</td>
</tr>
</table>

## scope1::local_def_is_possible

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
<pre>(deffun (addy x)
  (defvar y 1)
  (+ x y))
(addy 2)</pre>
</td>
<td>
<pre>function addy(x) {
  let y = 1;
  return x + y;
}
console.log(addy(2));</pre>
</td>
<td>
<pre>def addy(x):
    y = 1
    return x + y
print(addy(2))</pre>
</td>
</tr>
</table>

## scope1::refer_global_is_possible

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
<pre>(defvar y 1)
(deffun (addy x)
  (+ x y))
(addy 2)</pre>
</td>
<td>
<pre>let y = 1;
function addy(x) {
  return x + y;
}
console.log(addy(2));</pre>
</td>
<td>
<pre>y = 1
def addy(x):
    return x + y
print(addy(2))</pre>
</td>
</tr>
</table>

## scope1::defs_are_recursive

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
<pre>(deffun (addy x)
  (+ x y))
(defvar y 1)
(addy 2)</pre>
</td>
<td>
<pre>function addy(x) {
  return x + y;
}
let y = 1;
console.log(addy(2));</pre>
</td>
<td>
<pre>def addy(x):
    return x + y
y = 1
print(addy(2))</pre>
</td>
</tr>
</table>

## scope1::shadow_or_overwrite

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
<pre>(defvar y 100)
(deffun (addy x)
  (defvar y 200)
  (+ x y))
(addy 2)</pre>
</td>
<td>
<pre>let y = 100;
function addy(x) {
  let y = 200;
  return x + y;
}
console.log(addy(2));</pre>
</td>
<td>
<pre>y = 100
def addy(x):
    y = 200
    return x + y
print(addy(2))</pre>
</td>
</tr>
</table>

## scope1::shadow_rather_than_overwrite

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
<pre>(defvar y 100)
(deffun (addy x)
  (defvar y 200)
  (+ x y))
(+ (addy 2) y)</pre>
</td>
<td>
<pre>let y = 100;
function addy(x) {
  let y = 200;
  return x + y;
}
console.log(addy(2) + y);</pre>
</td>
<td>
<pre>y = 100
def addy(x):
    y = 200
    return x + y
print(addy(2) + y)</pre>
</td>
</tr>
</table>

## scope1::error_when_refer_to_undefined

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
<pre>(deffun (addy x)
  (defvar y 200)
  (+ x y))
(+ (addy 2) y)</pre>
</td>
<td>
<pre>function addy(x) {
  let y = 200;
  return x + y;
}
console.log(addy(2) + y);</pre>
</td>
<td>
<pre>def addy(x):
    y = 200
    return x + y
print(addy(2) + y)</pre>
</td>
</tr>
</table>

## scope1::what_is_x_1

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
(deffun (main)
  (defvar x 2)
  (deffun (get-x) x)
  (get-x))

(main)</pre>
</td>
<td>
<pre>let x = 1;
function main() {
  let x = 2;
  function getX() {
    return x;
  }
  return getX();
}
console.log(main());</pre>
</td>
<td>
<pre>x = 1
def main():
    x = 2
    def get_x():
        return x
    return get_x()
print(main())</pre>
</td>
</tr>
</table>

## scope1::what_is_x_2

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
(deffun (get-x) x)

(deffun (main)
  (defvar x 2)
  (get-x))
(main)</pre>
</td>
<td>
<pre>let x = 1;
function getX() {
  return x;
}
function main() {
  let x = 2;
  return getX();
}
console.log(main());</pre>
</td>
<td>
<pre>x = 1
def get_x():
    return x
def main():
    x = 2
    return get_x()
print(main())</pre>
</td>
</tr>
</table>

## scope1::what_is_x_3

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
(deffun (main)
  (defvar x 2)
  (get-x))
(deffun (get-x) x)

(main)</pre>
</td>
<td>
<pre>let x = 1;
function main() {
  let x = 2;
  return getX();
}
function getX() {
  return x;
}
console.log(main());</pre>
</td>
<td>
<pre>x = 1
def main():
    x = 2
    return get_x()
def get_x():
    return x
print(main())</pre>
</td>
</tr>
</table>

## scope1::what_is_x_4

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
(deffun (main)
  (deffun (get-x) x)
  (defvar x 2)
  (get-x))

(main)</pre>
</td>
<td>
<pre>let x = 1;
function main() {
  function getX() {
    return x;
  }
  let x = 2;
  return getX();
}
console.log(main());</pre>
</td>
<td>
<pre>x = 1
def main():
    def get_x():
        return x
    x = 2
    return get_x()
print(main())</pre>
</td>
</tr>
</table>

## scope1::define_twice_global

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
(defvar x 2)
x</pre>
</td>
<td>
<pre>let x = 1;
let x = 2;
console.log(x);</pre>
</td>
<td>
<pre>x = 1
x = 2
print(x)</pre>
</td>
</tr>
</table>

## scope1::define_twice_arg

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
<pre>(deffun (f x x)
  (+ x x))
(f 1 2)</pre>
</td>
<td>
<pre>function f(x, x) {
  return x + x;
}
console.log(f(1, 2));</pre>
</td>
<td>
<pre>def f(x, x):
    return x + x
print(f(1, 2))</pre>
</td>
</tr>
</table>

## scope2::warmup_error

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
<pre>(/ 1 0)</pre>
</td>
<td>
<pre>console.log(1 / 0);</pre>
</td>
<td>
<pre>print(1 / 0)</pre>
</td>
</tr>
</table>

## scope2::defvar_binding_cause_evaluation

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
<pre>(defvar x (/ 1 0))
42</pre>
</td>
<td>
<pre>let x = 1 / 0;
console.log(42);</pre>
</td>
<td>
<pre>x = 1 / 0
print(42)</pre>
</td>
</tr>
</table>

## scope2::funcall_binding_cause_evaluation

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
  42)
(f (/ 1 0))</pre>
</td>
<td>
<pre>function f(x) {
  return 42;
}
console.log(f(1 / 0));</pre>
</td>
<td>
<pre>def f(x):
    return 42
print(f(1 / 0))</pre>
</td>
</tr>
</table>

## scope2::good_order

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
(defvar y (+ x 2))
x
y</pre>
</td>
<td>
<pre>let x = 1;
let y = x + 2;
console.log(x);
console.log(y);</pre>
</td>
<td>
<pre>x = 1
y = x + 2
print(x)
print(y)</pre>
</td>
</tr>
</table>

## scope2::bad_order

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
<pre>(defvar y (+ x 2))
(defvar x 1)
x
y</pre>
</td>
<td>
<pre>let y = x + 2;
let x = 1;
console.log(x);
console.log(y);</pre>
</td>
<td>
<pre>y = x + 2
x = 1
print(x)
print(y)</pre>
</td>
</tr>
</table>

## scope2::order_and_funcall_warmup

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
<pre>(deffun (getx)
  x)
(defvar x 12)
(defvar y (getx))
y</pre>
</td>
<td>
<pre>function getx() {
  return x;
}
let x = 12;
let y = getx();
console.log(y);</pre>
</td>
<td>
<pre>def getx():
    return x
x = 12
y = getx()
print(y)</pre>
</td>
</tr>
</table>

## scope2::order_and_funcall_1

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
<pre>(deffun (getx)
  x)
(defvar y (getx))
(defvar x 12)
y</pre>
</td>
<td>
<pre>function getx() {
  return x;
}
let y = getx();
let x = 12;
console.log(y);</pre>
</td>
<td>
<pre>def getx():
    return x
y = getx()
x = 12
print(y)</pre>
</td>
</tr>
</table>

## scope2::order_and_funcall_2

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
<pre>(defvar x 2)
(deffun (main)
  (deffun (getx)
    x)
  (defvar y (getx))
  (defvar x 3)
  y)

(main)</pre>
</td>
<td>
<pre>let x = 2;
function main() {
  function getx() {
    return x;
  }
  let y = getx();
  let x = 3;
  return y;
}
console.log(main());</pre>
</td>
<td>
<pre>x = 2
def main():
    def getx():
        return x
    y = getx()
    x = 3
    return y
print(main())</pre>
</td>
</tr>
</table>

## mut-vars1::scope_review_1

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

## mut-vars1::scope_review_2

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
<pre>(deffun (foo)
  y)
(defvar y 1)
(foo)</pre>
</td>
<td>
<pre>function foo() {
  return y;
}
let y = 1;
console.log(foo());</pre>
</td>
<td>
<pre>def foo():
    return y
y = 1
print(foo())</pre>
</td>
</tr>
</table>

## mut-vars1::scope_review_3

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
(deffun (gety)
  (defvar y x)
  (defvar x 2)
  y)
(gety)</pre>
</td>
<td>
<pre>let x = 1;
function gety() {
  let y = x;
  let x = 2;
  return y;
}
console.log(gety());</pre>
</td>
<td>
<pre>x = 1
def gety():
    y = x
    x = 2
    return y
print(gety())</pre>
</td>
</tr>
</table>

## mut-vars2::warmup_setbang

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
<pre>(defvar rent 100)
(set! rent (* 100 2))
rent</pre>
</td>
<td>
<pre>let rent = 100;
rent = 100 * 2;
console.log(rent);</pre>
</td>
<td>
<pre>rent = 100
rent = 100 * 2
print(rent)</pre>
</td>
</tr>
</table>

## mut-vars2::update_undefined

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
<pre>(set! foobar 2)
foobar</pre>
</td>
<td>
<pre>foobar = 2;
console.log(foobar);</pre>
</td>
<td>
<pre>foobar = 2
print(foobar)</pre>
</td>
</tr>
</table>

## mut-vars2::not_aliased_by_defvar_1

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
(defvar y x)
(set! x 0)
x
y</pre>
</td>
<td>
<pre>let x = 12;
let y = x;
x = 0;
console.log(x);
console.log(y);</pre>
</td>
<td>
<pre>x = 12
y = x
x = 0
print(x)
print(y)</pre>
</td>
</tr>
</table>

## mut-vars2::not_aliased_by_defvar_2

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
<pre>(defvar m 40)
(defvar n m)
(set! n 22)
m
n</pre>
</td>
<td>
<pre>let m = 40;
let n = m;
n = 22;
console.log(m);
console.log(n);</pre>
</td>
<td>
<pre>m = 40
n = m
n = 22
print(m)
print(n)</pre>
</td>
</tr>
</table>

## mut-vars2::not_aliased_by_defvar_3

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
(defvar y (+ x 100))
(set! x 2)
x
y</pre>
</td>
<td>
<pre>let x = 1;
let y = x + 100;
x = 2;
console.log(x);
console.log(y);</pre>
</td>
<td>
<pre>x = 1
y = x + 100
x = 2
print(x)
print(y)</pre>
</td>
</tr>
</table>

## mut-vars2::remote_update_possible

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
(deffun (f)
  (set! x 0))
(f)
x</pre>
</td>
<td>
<pre>let x = 12;
function f() {
  return x = 0;
}
console.log(f());
console.log(x);</pre>
</td>
<td>
<pre>x = 12
def f():
    global x
    return (x := 0)
print(f())
print(x)</pre>
</td>
</tr>
</table>

## mut-vars2::not_aliased_by_funarg_1

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

## mut-vars2::funs_remember_vars_not_vals

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
(deffun (getx)
  x)
(deffun (setx new-val)
  (set! x new-val))
(getx)
(setx 2)
(getx)</pre>
</td>
<td>
<pre>let x = 1;
function getx() {
  return x;
}
function setx(newVal) {
  return x = newVal;
}
console.log(getx());
console.log(setx(2));
console.log(getx());</pre>
</td>
<td>
<pre>x = 1
def getx():
    return x
def setx(new_val):
    global x
    return (x := new_val)
print(getx())
print(setx(2))
print(getx())</pre>
</td>
</tr>
</table>

## mut-vars2::not_aliased_by_funarg_2

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
(deffun (set-and-return y)
  (set! y 0)
  x)
(set-and-return x)</pre>
</td>
<td>
<pre>let x = 12;
function setAndReturn(y) {
  y = 0;
  return x;
}
console.log(setAndReturn(x));</pre>
</td>
<td>
<pre>x = 12
def set_and_return(y):
    y = 0
    return x
print(set_and_return(x))</pre>
</td>
</tr>
</table>

## mut-vars2::not_aliased_by_funarg_3

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
(deffun (set-and-return y)
  (set! x 0)
  y)
(set-and-return x)
x</pre>
</td>
<td>
<pre>let x = 12;
function setAndReturn(y) {
  x = 0;
  return y;
}
console.log(setAndReturn(x));
console.log(x);</pre>
</td>
<td>
<pre>x = 12
def set_and_return(y):
    global x
    x = 0
    return y
print(set_and_return(x))
print(x)</pre>
</td>
</tr>
</table>

## vectors1::warmup_mvec

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
<pre>(defvar n 3)
(deffun (f x)
  (+ x 1))
(mvec n (f n))</pre>
</td>
<td>
<pre>let n = 3;
function f(x) {
  return x + 1;
}
console.log([ n, f(n) ]);</pre>
</td>
<td>
<pre>n = 3
def f(x):
    return x + 1
print([n, f(n)])</pre>
</td>
</tr>
</table>

## vectors1::vec_hetero

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
<pre>(mvec (mvec 1 2) 3)</pre>
</td>
<td>
<pre>console.log([ [ 1, 2 ], 3 ]);</pre>
</td>
<td>
<pre>print([[1, 2], 3])</pre>
</td>
</tr>
</table>

## vectors1::vec_print

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
<pre>(mvec (mvec 123) (mvec 4 5))</pre>
</td>
<td>
<pre>console.log([ [ 123 ], [ 4, 5 ] ]);</pre>
</td>
<td>
<pre>print([[123], [4, 5]])</pre>
</td>
</tr>
</table>

## vectors1::warmup_veclen

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
(vec-len v)</pre>
</td>
<td>
<pre>let v = [ 1, 2, 3, 4 ];
console.log(v.length);</pre>
</td>
<td>
<pre>v = [1, 2, 3, 4]
print(len(v))</pre>
</td>
</tr>
</table>

## vectors1::veclen_nested

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
<pre>(vec-len (mvec 4 (mvec 5 6)))</pre>
</td>
<td>
<pre>console.log([ 4, [ 5, 6 ] ].length);</pre>
</td>
<td>
<pre>print(len([4, [5, 6]]))</pre>
</td>
</tr>
</table>

## vectors1::warmup_vecref

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
<pre>(defvar v (mvec (mvec 10 20) (mvec 30 40)))
(vec-ref (vec-ref v 1) 0)</pre>
</td>
<td>
<pre>let v = [ [ 10, 20 ], [ 30, 40 ] ];
console.log(v[1][0]);</pre>
</td>
<td>
<pre>v = [[10, 20], [30, 40]]
print(v[1][0])</pre>
</td>
</tr>
</table>

## vectors1::warmup_vecset_1

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
(vec-set! x 0 100)
x</pre>
</td>
<td>
<pre>let x = [ 2, 3 ];
x[0] = 100;
console.log(x);</pre>
</td>
<td>
<pre>x = [2, 3]
x[0] = 100
print(x)</pre>
</td>
</tr>
</table>

## vectors1::warmup_vecset_2

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
<pre>(defvar x (mvec 2))
(vec-set! x 0 100)
x</pre>
</td>
<td>
<pre>let x = [ 2 ];
x[0] = 100;
console.log(x);</pre>
</td>
<td>
<pre>x = [2]
x[0] = 100
print(x)</pre>
</td>
</tr>
</table>

## vectors1::mpairs_are_mvec

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
<pre>(defvar mv (mvec 4 5))
(left mv)</pre>
</td>
<td>
<pre>let mv = [ 4, 5 ];
console.log(mv[0]);</pre>
</td>
<td>
<pre>mv = [4, 5]
print(mv[0])</pre>
</td>
</tr>
</table>

## vectors1::vector_not_flatten

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
<pre>(defvar m (mvec 1 2))
(vec-set! m 1 (mvec 3 4))
(vec-ref m 2)</pre>
</td>
<td>
<pre>let m = [ 1, 2 ];
m[1] = [ 3, 4 ];
console.log(m[2]);</pre>
</td>
<td>
<pre>m = [1, 2]
m[1] = [3, 4]
print(m[2])</pre>
</td>
</tr>
</table>

## vectors2::alias_with_defvar

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
<pre>(defvar x (mvec 100))
(defvar y x)
(vec-set! x 0 200)
y</pre>
</td>
<td>
<pre>let x = [ 100 ];
let y = x;
x[0] = 200;
console.log(y);</pre>
</td>
<td>
<pre>x = [100]
y = x
x[0] = 200
print(y)</pre>
</td>
</tr>
</table>

## vectors2::alias_with_funcall

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
<pre>(defvar x (mvec 1 0))
(deffun (f y)
  (vec-set! y 0 173))
(f x)
x</pre>
</td>
<td>
<pre>let x = [ 1, 0 ];
function f(y) {
  return y[0] = 173;
}
console.log(f(x));
console.log(x);</pre>
</td>
<td>
<pre>x = [1, 0]
def f(y):
    return y.__setitem__(0, 173)
print(f(x))
print(x)</pre>
</td>
</tr>
</table>

## vectors2::alias_var_in_mvec

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
v</pre>
</td>
<td>
<pre>let x = 3;
let v = [ 1, 2, x ];
x = 4;
console.log(v);</pre>
</td>
<td>
<pre>x = 3
v = [1, 2, x]
x = 4
print(v)</pre>
</td>
</tr>
</table>

## vectors2::alias_mvec_in_mvec

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
<pre>(defvar x (mvec 3))
(defvar v (mvec 1 2 x))
(vec-set! x 0 4)
v</pre>
</td>
<td>
<pre>let x = [ 3 ];
let v = [ 1, 2, x ];
x[0] = 4;
console.log(v);</pre>
</td>
<td>
<pre>x = [3]
v = [1, 2, x]
x[0] = 4
print(v)</pre>
</td>
</tr>
</table>

## vectors2::alias_mvec_in_mvec_trick

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
<pre>(defvar x (mvec 3))
(defvar v (mvec 1 2 x))
(set! x 4)
v</pre>
</td>
<td>
<pre>let x = [ 3 ];
let v = [ 1, 2, x ];
x = 4;
console.log(v);</pre>
</td>
<td>
<pre>x = [3]
v = [1, 2, x]
x = 4
print(v)</pre>
</td>
</tr>
</table>

## vectors2::alias_mvec_in_mpair

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
<pre>(defvar v (mvec 1 2 3))
(defvar vv (mpair v v))
(vec-set! (right vv) 0 100)
(left vv)</pre>
</td>
<td>
<pre>let v = [ 1, 2, 3 ];
let vv = [ v, v ];
vv[1][0] = 100;
console.log(vv[0]);</pre>
</td>
<td>
<pre>v = [1, 2, 3]
vv = [ v, v ]
vv[1][0] = 100
print(vv[0])</pre>
</td>
</tr>
</table>

## vectors2::warmup_circularity

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
<pre>(defvar x (mvec 1 0 2))
(vec-set! x 1 x)
(vec-len x)</pre>
</td>
<td>
<pre>let x = [ 1, 0, 2 ];
x[1] = x;
console.log(x.length);</pre>
</td>
<td>
<pre>x = [1, 0, 2]
x[1] = x
print(len(x))</pre>
</td>
</tr>
</table>

## vectors2::circularity_and_alias

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
<pre>(defvar v (mpair 10 7))
(set-left! v v)
(set-right! v 42)
(right (left (left v)))</pre>
</td>
<td>
<pre>let v = [ 10, 7 ];
console.log(v[0]=v);
console.log(v[1]=42);
console.log(v[0][0][1]);</pre>
</td>
<td>
<pre>v = [ 10, 7 ]
v[0] = v
v[1] = 42
print(((v[0])[0])[1])</pre>
</td>
</tr>
</table>

## lambda1::smol_quiz_var_as_arg

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

## lambda1::smol_quiz_seemingly_alias_a_var

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

## lambda1::smol_quiz_aliasing_mvec_in_mvec

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
<pre>(defvar x (mvec 1 7 3))
(defvar pr (mpair x x))
(vec-set! (right pr) 0 100)
pr</pre>
</td>
<td>
<pre>let x = [ 1, 7, 3 ];
let pr = [ x, x ];
pr[1][0] = 100;
console.log(pr);</pre>
</td>
<td>
<pre>x = [1, 7, 3]
pr = [ x, x ]
pr[1][0] = 100
print(pr)</pre>
</td>
</tr>
</table>

## lambda1::smol_quiz_circularity

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

## lambda1::warmup_hof

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
<pre>(deffun (get) 42)
(defvar f get)
(defvar g f)
(g)</pre>
</td>
<td>
<pre>function get() {
  return 42;
}
let f = get;
let g = f;
console.log(g());</pre>
</td>
<td>
<pre>def get():
    return 42
f = get
g = f
print(g())</pre>
</td>
</tr>
</table>

## lambda1::fun_as_parameter

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
<pre>(deffun (twice f x)
  (f (f x)))
(deffun (double x)
  (+ x x))
(twice double 1)</pre>
</td>
<td>
<pre>function twice(f, x) {
  return f(f(x));
}
function double(x) {
  return x + x;
}
console.log(twice(double, 1));</pre>
</td>
<td>
<pre>def twice(f, x):
    return f(f(x))
def double(x):
    return x + x
print(twice(double, 1))</pre>
</td>
</tr>
</table>

## lambda1::fun_as_output

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
<pre>(deffun (add1 x) (+ x 1))
(deffun (g) add1)
(defvar f (g))
(f 100)</pre>
</td>
<td>
<pre>function add1(x) {
  return x + 1;
}
function g() {
  return add1;
}
let f = g();
console.log(f(100));</pre>
</td>
<td>
<pre>def add1(x):
    return x + 1
def g():
    return add1
f = g()
print(f(100))</pre>
</td>
</tr>
</table>

## lambda1::fun_in_vectors

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
<pre>(deffun (add1 n)
  (+ n 1))
(defvar v (mvec add1))
((vec-ref v 0) 2)</pre>
</td>
<td>
<pre>function add1(n) {
  return n + 1;
}
let v = [ add1 ];
console.log(v[0](2));</pre>
</td>
<td>
<pre>def add1(n):
    return n + 1
v = [add1]
print(v[0](2))</pre>
</td>
</tr>
</table>

## lambda2::read_local1

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
<pre>(deffun (make-getter)
  (defvar x 1)
  (deffun (get-x) x)
  get-x)
(defvar get-x (make-getter))
(get-x)</pre>
</td>
<td>
<pre>function makeGetter() {
  let x = 1;
  function getX() {
    return x;
  }
  return getX;
}
let getX = makeGetter();
console.log(getX());</pre>
</td>
<td>
<pre>def make_getter():
    x = 1
    def get_x():
        return x
    return get_x
get_x = make_getter()
print(get_x())</pre>
</td>
</tr>
</table>

## lambda2::read_local2

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
<pre>(deffun (make-getter x)
  (deffun (get-x) x)
  get-x)
(defvar get-a (make-getter 1))
(defvar get-b (make-getter 2))
(get-a)
(get-b)</pre>
</td>
<td>
<pre>function makeGetter(x) {
  function getX() {
    return x;
  }
  return getX;
}
let getA = makeGetter(1);
let getB = makeGetter(2);
console.log(getA());
console.log(getB());</pre>
</td>
<td>
<pre>def make_getter(x):
    def get_x():
        return x
    return get_x
get_a = make_getter(1)
get_b = make_getter(2)
print(get_a())
print(get_b())</pre>
</td>
</tr>
</table>

## lambda2::fun_ref_env

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
<pre>(deffun (make-addy y)
  (deffun (addy x)
    (+ x y))
  addy)
(defvar f (make-addy 10))
(defvar g (make-addy 50))
(f 2)
(g 2)</pre>
</td>
<td>
<pre>function makeAddy(y) {
  function addy(x) {
    return x + y;
  }
  return addy;
}
let f = makeAddy(10);
let g = makeAddy(50);
console.log(f(2));
console.log(g(2));</pre>
</td>
<td>
<pre>def make_addy(y):
    def addy(x):
        return x + y
    return addy
f = make_addy(10)
g = make_addy(50)
print(f(2))
print(g(2))</pre>
</td>
</tr>
</table>

## lambda2::state

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
(deffun (make-f)
  (deffun (addx y)
    (+ x y))
  addx)
(defvar f (make-f))
(set! x 2)
(f x)</pre>
</td>
<td>
<pre>let x = 1;
function makeF() {
  function addx(y) {
    return x + y;
  }
  return addx;
}
let f = makeF();
x = 2;
console.log(f(x));</pre>
</td>
<td>
<pre>x = 1
def make_f():
    def addx(y):
        return x + y
    return addx
f = make_f()
x = 2
print(f(x))</pre>
</td>
</tr>
</table>

## lambda2::counter

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
<pre>(deffun (make-counter count)
  (deffun (counter)
    (set! count (+ count 1))
    count)
  counter)
(defvar f (make-counter 0))
(defvar g (make-counter 0))

(f)
(f)
(g)</pre>
</td>
<td>
<pre>function makeCounter(count) {
  function counter() {
    count = count + 1;
    return count;
  }
  return counter;
}
let f = makeCounter(0);
let g = makeCounter(0);
console.log(f());
console.log(f());
console.log(g());</pre>
</td>
<td>
<pre>def make_counter(count):
    def counter():
        nonlocal count
        count = count + 1
        return count
    return counter
f = make_counter(0)
g = make_counter(0)
print(f())
print(f())
print(g())</pre>
</td>
</tr>
</table>

## lambda2::syntax_pitfall

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

## lambda3::curry_lambda

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
(defvar x 0)
((f 2) 1)</pre>
</td>
<td>
<pre>function f(x) {
  return function (y) {
    return x + y;
  };
}
let x = 0;
console.log(f(2)(1));</pre>
</td>
<td>
<pre>def f(x):
    return lambda y: x + y
x = 0
print(f(2)(1))</pre>
</td>
</tr>
</table>

## lambda3::lambda_remembers_env

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

## lambda3::counter_lambda

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
<pre>(deffun (make-counter count)
  (lambda ()
    (set! count (+ count 1))
    count))
(defvar f (make-counter 0))
(defvar g (make-counter 0))

(f)
(f)
(g)</pre>
</td>
<td>
<pre>function makeCounter(count) {
  return function () {
    count = count + 1;
    return count;
  };
}
let f = makeCounter(0);
let g = makeCounter(0);
console.log(f());
console.log(f());
console.log(g());</pre>
</td>
<td>
<pre>def make_counter(count):
    return lambda: ("WARNING: the translation might be inaccurate", (count := count + 1, count)[-1])[-1]
f = make_counter(0)
g = make_counter(0)
print(f())
print(f())
print(g())</pre>
</td>
</tr>
</table>
