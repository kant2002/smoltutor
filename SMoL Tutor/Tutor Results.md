## 1. scope1::warmup_defvar

<pre><code>(defvar x 1)
(defvar y (+ x 2))
x
y</code></pre>
<ul>
<li>(.98 = 99/101) <code>1 3</code></li>
<li>(.01 = 1/101) <code>1 2</code></li>
<li>(.01 = 1/101) <code>error</code></li>
</ul>

## 2. scope1::warmup_error
<pre><code>(defvar xyz 173)
abc</code></pre>
<ul>
<li>(.98 = 98/100) <code>error</code></li>
<li>(.01 = 1/100) <code>173</code></li>
<li>(.01 = 1/100) <code>possibly abc</code></li>
</ul>

## 3. scope1::warmup_fun
<pre><code>(deffun (sum x y z)
  (+ x (+ y z)))
(sum 2 1 3)</code></pre>
<ul>
<li>(.99 = 100/101) <code>6</code></li>
<li>(.01 = 1/101) <code>5</code></li>
</ul>

## 4. scope1::local_def_is_possible
<pre><code>(deffun (addy x)
  (defvar y 1)
  (+ x y))
(addy 2)</code></pre>
<ul>
<li>(.97 = 98/101) <code>3</code></li>
<li>(.03 = 3/101) <code>error</code></li>
</ul>

## 5. scope1::refer_global_is_possible
<pre><code>(defvar y 1)
(deffun (addy x)
  (+ x y))
(addy 2)</code></pre>
<ul>
<li>(.77 = 79/102) <code>3</code></li>
<li>(.23 = 23/102) <code>error</code> [IsolatedFun]</li>
</ul>

## 6. scope1::defs_are_recursive
<pre><code>(deffun (addy x)
  (+ x y))
(defvar y 1)
(addy 2)</code></pre>
<ul>
<li>(.67 = 68/101) <code>error</code> [DeepClosure, IsolatedFun,
NestedDef]</li>
<li>(.32 = 32/101) <code>3</code></li>
<li>(.01 = 1/101) <code>2</code></li>
</ul>

## 7. scope1::shadow_or_overwrite
<pre><code>(defvar y 100)
(deffun (addy x)
  (defvar y 200)
  (+ x y))
(addy 2)</code></pre>
<ul>
<li>(.91 = 92/101) <code>202</code></li>
<li>(.05 = 5/101) <code>102</code></li>
<li>(.04 = 4/101) <code>error</code></li>
</ul>

## 8. scope1::shadow_rather_than_overwrite
<pre><code>(defvar y 100)
(deffun (addy x)
  (defvar y 200)
  (+ x y))
(+ (addy 2) y)</code></pre>
<ul>
<li>(.93 = 95/102) <code>302</code></li>
<li>(.06 = 6/102) <code>402</code> [FlatEnv]</li>
<li>(.01 = 1/102) <code>error</code></li>
</ul>

## 9. scope1::error_when_refer_to_undefined
<pre><code>(deffun (addy x)
  (defvar y 200)
  (+ x y))
(+ (addy 2) y)</code></pre>
<ul>
<li>(.96 = 98/102) <code>error</code></li>
<li>(.04 = 4/102) <code>402</code> [FlatEnv]</li>
</ul>

## 10. scope1::what_is_x_1
<pre><code>(defvar x 1)
(deffun (main)
  (defvar x 2)
  (deffun (get-x) x)
  (get-x))

(main)</code></pre>
<ul>
<li>(.85 = 85/100) <code>2</code></li>
<li>(.09 = 9/100) <code>error</code> [IsolatedFun]</li>
<li>(.05 = 5/100) <code>1</code></li>
<li>(.01 = 1/100) <code>3</code></li>
</ul>

## 11. scope1::what_is_x_2
<pre><code>(defvar x 1)
(deffun (get-x) x)

(deffun (main)
  (defvar x 2)
  (get-x))
(main)</code></pre>
<ul>
<li>(.70 = 71/102) <code>1</code></li>
<li>(.29 = 30/102) <code>2</code> [FlatEnv]</li>
<li>(.01 = 1/102) <code>error</code> [IsolatedFun]</li>
</ul>

## 12. scope1::what_is_x_3
<pre><code>(defvar x 1)
(deffun (main)
  (defvar x 2)
  (get-x))
(deffun (get-x) x)

(main)</code></pre>
<ul>
<li>(.76 = 77/101) <code>1</code></li>
<li>(.14 = 14/101) <code>error</code> [DeepClosure, IsolatedFun,
NestedDef]</li>
<li>(.10 = 10/101) <code>2</code> [FlatEnv]</li>
</ul>

## 13. scope1::what_is_x_4
<pre><code>(defvar x 1)
(deffun (main)
  (deffun (get-x) x)
  (defvar x 2)
  (get-x))

(main)</code></pre>
<ul>
<li>(.92 = 93/101) <code>2</code></li>
<li>(.08 = 8/101) <code>1</code> [NestedDef]</li>
</ul>

## 14. scope1::define_twice_global
<pre><code>(defvar x 1)
(defvar x 2)
x</code></pre>
<ul>
<li>(.63 = 63/100) <code>2</code> [DefOrSet, NestedDef]</li>
<li>(.36 = 36/100) <code>error</code></li>
<li>(.01 = 1/100) <code>1</code></li>
</ul>

## 15. scope1::define_twice_arg
<pre><code>(deffun (f x x)
  (+ x x))
(f 1 2)</code></pre>
<ul>
<li>(.92 = 92/100) <code>error</code></li>
<li>(.07 = 7/100) <code>3</code></li>
<li>(.01 = 1/100) <code>2</code></li>
</ul>

## 16. scope2::warmup_error
<pre><code>(/ 1 0)</code></pre>
<ul>
<li>(.97 = 92/95) <code>error</code></li>
<li>(.02 = 2/95) <code>1</code></li>
<li>(.01 = 1/95) <code>0</code></li>
</ul>

## 17. scope2::defvar_binding_cause_evaluation
<pre><code>(defvar x (/ 1 0))
42</code></pre>
<ul>
<li>(.71 = 67/95) <code>error</code></li>
<li>(.29 = 28/95) <code>42</code> [Lazy]</li>
</ul>

## 18. scope2::funcall_binding_cause_evaluation
<pre><code>(deffun (f x)
  42)
(f (/ 1 0))</code></pre>
<ul>
<li>(.92 = 87/95) <code>error</code></li>
<li>(.08 = 8/95) <code>42</code> [Lazy]</li>
</ul>

## 19. scope2::good_order
<pre><code>(defvar x 1)
(defvar y (+ x 2))
x
y</code></pre>
<ul>
<li>(.99 = 93/94) <code>1 3</code></li>
<li>(.01 = 1/94) <code>error</code></li>
</ul>

## 20. scope2::bad_order
<pre><code>(defvar y (+ x 2))
(defvar x 1)
x
y</code></pre>
<ul>
<li>(.57 = 54/95) <code>1 3</code> [Lazy]</li>
<li>(.43 = 41/95) <code>error</code></li>
</ul>

## 21. scope2::order_and_funcall_warmup
<pre><code>(deffun (getx)
  x)
(defvar x 12)
(defvar y (getx))
y</code></pre>
<ul>
<li>(.76 = 72/95) <code>12</code></li>
<li>(.24 = 23/95) <code>error</code> [DeepClosure, IsolatedFun,
NestedDef]</li>
</ul>

## 22. scope2::order_and_funcall_1
<pre><code>(deffun (getx)
  x)
(defvar y (getx))
(defvar x 12)
y</code></pre>
<ul>
<li>(.63 = 60/95) <code>error</code></li>
<li>(.37 = 35/95) <code>12</code> [Lazy]</li>
</ul>

## 23. scope2::order_and_funcall_2
<pre><code>(defvar x 2)
(deffun (main)
  (deffun (getx)
    x)
  (defvar y (getx))
  (defvar x 3)
  y)

(main)</code></pre>
<ul>
<li>(.60 = 56/94) <code>2</code> [DefOrSet, NestedDef]</li>
<li>(.28 = 26/94) <code>error</code></li>
<li>(.13 = 12/94) <code>3</code> [Lazy]</li>
</ul>

## 24. mut-vars1::scope_review_1
<pre><code>(defvar x 0)
(defvar y x)
(defvar x 2)
x
y</code></pre>
<ul>
<li>(.86 = 78/91) <code>error</code></li>
<li>(.13 = 12/91) <code>2 0</code> [DefOrSet, NestedDef]</li>
<li>(.01 = 1/91) <code>2 2</code></li>
</ul>

## 25. mut-vars1::scope_review_2
<pre><code>(deffun (foo)
  y)
(defvar y 1)
(foo)</code></pre>
<ul>
<li>(.81 = 74/91) <code>1</code></li>
<li>(.19 = 17/91) <code>error</code> [DeepClosure, IsolatedFun,
NestedDef]</li>
</ul>

## 26. mut-vars1::scope_review_3
<pre><code>(defvar x 1)
(deffun (gety)
  (defvar y x)
  (defvar x 2)
  y)
(gety)</code></pre>
<ul>
<li>(.65 = 59/91) <code>error</code></li>
<li>(.30 = 27/91) <code>1</code> [DefOrSet, NestedDef]</li>
<li>(.05 = 5/91) <code>2</code> [Lazy]</li>
</ul>

## 27. mut-vars2::warmup_setbang
<pre><code>(defvar rent 100)
(set! rent (* 100 2))
rent</code></pre>
<ul>
<li>(.99 = 91/92) <code>200</code></li>
<li>(.01 = 1/92) <code>2000</code></li>
</ul>

## 28. mut-vars2::update_undefined
<pre><code>(set! foobar 2)
foobar</code></pre>
<ul>
<li>(.85 = 79/93) <code>error</code></li>
<li>(.15 = 14/93) <code>2</code> [DefOrSet]</li>
</ul>

## 29. mut-vars2::not_aliased_by_defvar_1
<pre><code>(defvar x 12)
(defvar y x)
(set! x 0)
x
y</code></pre>
<ul>
<li>(.85 = 79/93) <code>0 12</code></li>
<li>(.12 = 11/93) <code>0 0</code> [DefByRef]</li>
<li>(.02 = 2/93) <code>error</code></li>
<li>(.01 = 1/93) <code>depends on implementation</code></li>
</ul>

## 30. mut-vars2::not_aliased_by_defvar_2
<pre><code>(defvar m 40)
(defvar n m)
(set! n 22)
m
n</code></pre>
<ul>
<li>(.99 = 92/93) <code>40 22</code></li>
<li>(.01 = 1/93) <code>40 11</code></li>
</ul>

## 31. mut-vars2::not_aliased_by_defvar_3
<pre><code>(defvar x 1)
(defvar y (+ x 100))
(set! x 2)
x
y</code></pre>
<ul>
<li>(.99 = 92/93) <code>2 101</code></li>
<li>(.01 = 1/93) <code>2 102</code></li>
</ul>

## 32. mut-vars2::remote_update_possible
<pre><code>(defvar x 12)
(deffun (f)
  (set! x 0))
(f)
x</code></pre>
<ul>
<li>(.89 = 83/93) <code>0</code></li>
<li>(.05 = 5/93) <code>12</code> [DeepClosure, DefOrSet]</li>
<li>(.05 = 5/93) <code>error</code> [IsolatedFun]</li>
</ul>

## 33. mut-vars2::not_aliased_by_funarg_1
<pre><code>(defvar x 12)
(deffun (f x)
  (set! x 0))
(f x)
x</code></pre>
<ul>
<li>(.52 = 48/93) <code>12</code></li>
<li>(.41 = 38/93) <code>0</code> [CallByRef, FlatEnv]</li>
<li>(.08 = 7/93) <code>error</code></li>
</ul>

## 34. mut-vars2::funs_remember_vars_not_vals
<pre><code>(defvar x 1)
(deffun (getx)
  x)
(deffun (setx new-val)
  (set! x new-val))
(getx)
(setx 2)
(getx)</code></pre>
<ul>
<li>(.78 = 73/93) <code>1 2</code></li>
<li>(.20 = 19/93) <code>1 1</code> [DeepClosure, DefOrSet]</li>
<li>(.01 = 1/93) <code>1 2 1</code></li>
</ul>

## 35. mut-vars2::not_aliased_by_funarg_2
<pre><code>(defvar x 12)
(deffun (set-and-return y)
  (set! y 0)
  x)
(set-and-return x)</code></pre>
<ul>
<li>(.78 = 73/93) <code>12</code></li>
<li>(.11 = 10/93) <code>error</code> [IsolatedFun]</li>
<li>(.10 = 9/93) <code>0</code> [CallByRef]</li>
<li>(.01 = 1/93) <code>23</code></li>
</ul>

## 36. mut-vars2::not_aliased_by_funarg_3
<pre><code>(defvar x 12)
(deffun (set-and-return y)
  (set! x 0)
  y)
(set-and-return x)
x</code></pre>
<ul>
<li>(.80 = 74/92) <code>12 0</code></li>
<li>(.07 = 6/92) <code>12 12</code> [DeepClosure, DefOrSet]</li>
<li>(.07 = 6/92) <code>error</code> [IsolatedFun]</li>
<li>(.03 = 3/92) <code>0 0</code> [CallByRef]</li>
<li>(.03 = 3/92) <code>12</code></li>
</ul>

## 37. vectors1::warmup_mvec
<pre><code>(defvar n 3)
(deffun (f x)
  (+ x 1))
(mvec n (f n))</code></pre>
<ul>
<li>(.97 = 89/92) <code>#(3 4)</code></li>
<li>(.02 = 2/92) <code>error</code></li>
<li>(.01 = 1/92) <code>#(n (f n))</code></li>
</ul>

## 38. vectors1::vec_hetero
<pre><code>(mvec (mvec 1 2) 3)</code></pre>
<ul>
<li>(.96 = 88/92) <code>#(#(1 2) 3)</code></li>
<li>(.02 = 2/92) <code>error</code></li>
<li>(.01 = 1/92) <code>#(#(1 2) #(3))</code></li>
<li>(.01 = 1/92) <code>#(#(3 1) 2)</code></li>
</ul>

## 39. vectors1::vec_print
<pre><code>(mvec (mvec 123) (mvec 4 5))</code></pre>
<ul>
<li>(.91 = 84/92) <code>#(#(123) #(4 5))</code></li>
<li>(.05 = 5/92) <code>#('#(123) '#(4 5))</code></li>
<li>(.02 = 2/92) <code>error</code></li>
<li>(.01 = 1/92) <code>#('#(231) '#(4 5))</code></li>
</ul>

## 40. vectors1::warmup_veclen
<pre><code>(defvar v (mvec 1 2 3 4))
(vec-len v)</code></pre>
<ul>
<li>(.99 = 90/91) <code>4</code></li>
<li>(.01 = 1/91) <code>error</code></li>
</ul>

## 41. vectors1::veclen_nested
<pre><code>(vec-len (mvec 4 (mvec 5 6)))</code></pre>
<ul>
<li>(.95 = 86/91) <code>2</code></li>
<li>(.03 = 3/91) <code>3</code></li>
<li>(.01 = 1/91) <code>1</code></li>
<li>(.01 = 1/91) <code>error</code></li>
</ul>

## 42. vectors1::warmup_vecref
<pre><code>(defvar v (mvec (mvec 10 20) (mvec 30 40)))
(vec-ref (vec-ref v 1) 0)</code></pre>
<ul>
<li>(.81 = 74/91) <code>30</code></li>
<li>(.11 = 10/91) <code>10</code></li>
<li>(.04 = 4/91) <code>20</code></li>
<li>(.02 = 2/91) <code>error</code></li>
<li>(.01 = 1/91) <code>1</code></li>
</ul>

## 43. vectors1::warmup_vecset_1
<pre><code>(defvar x (mvec 2 3))
(vec-set! x 0 100)
x</code></pre>
<ul>
<li>(.87 = 79/91) <code>#(100 3)</code></li>
<li>(.13 = 12/91) <code>100 3</code></li>
</ul>

## 44. vectors1::warmup_vecset_2
<pre><code>(defvar x (mvec 2))
(vec-set! x 0 100)
x</code></pre>
<ul>
<li>(.97 = 88/91) <code>#(100)</code></li>
<li>(.03 = 3/91) <code>100</code></li>
</ul>

## 45. vectors1::mpairs_are_mvec
<pre><code>(defvar mv (mvec 4 5))
(left mv)</code></pre>
<ul>
<li>(.87 = 79/91) <code>4</code></li>
<li>(.13 = 12/91) <code>error</code></li>
</ul>

## 46. vectors1::vector_not_flatten
<pre><code>(defvar m (mvec 1 2))
(vec-set! m 1 (mvec 3 4))
(vec-ref m 2)</code></pre>
<ul>
<li>(.93 = 84/90) <code>error</code></li>
<li>(.02 = 2/90) <code>2</code></li>
<li>(.02 = 2/90) <code>4</code></li>
<li>(.01 = 1/90) <code>#(3 4)</code></li>
<li>(.01 = 1/90) <code>3</code></li>
</ul>

## 47. vectors2::alias_with_defvar
<pre><code>(defvar x (mvec 100))
(defvar y x)
(vec-set! x 0 200)
y</code></pre>
<ul>
<li>(.67 = 62/92) <code>#(100)</code> [DefsCopyStructs]</li>
<li>(.30 = 28/92) <code>#(200)</code></li>
<li>(.01 = 1/92) <code>#(300)</code></li>
<li>(.01 = 1/92) <code>error</code></li>
</ul>

## 48.
vectors2::alias_with_funcall
<pre><code>(defvar x (mvec 1 0))
(deffun (f y)
  (vec-set! y 0 173))
(f x)
x</code></pre>
<ul>
<li>(.90 = 83/92) <code>#(173 0)</code></li>
<li>(.10 = 9/92) <code>#(1 0)</code> [CallsCopyStructs]</li>
</ul>

## 49. vectors2::alias_var_in_mvec
<pre><code>(defvar x 3)
(defvar v (mvec 1 2 x))
(set! x 4)
v</code></pre>
<ul>
<li>(.67 = 62/92) <code>#(1 2 3)</code></li>
<li>(.24 = 22/92) <code>#(1 2 4)</code> [StructByRef]</li>
<li>(.09 = 8/92) <code>error</code></li>
</ul>

## 50. vectors2::alias_mvec_in_mvec
<pre><code>(defvar x (mvec 3))
(defvar v (mvec 1 2 x))
(vec-set! x 0 4)
v</code></pre>
<ul>
<li>(.84 = 77/92) <code>#(1 2 #(4))</code></li>
<li>(.14 = 13/92) <code>#(1 2 #(3))</code> [DefsCopyStructs,
StructsCopyStructs]</li>
<li>(.02 = 2/92) <code>error</code></li>
</ul>

## 51. vectors2::alias_mvec_in_mvec_trick
<pre><code>(defvar x (mvec 3))
(defvar v (mvec 1 2 x))
(set! x 4)
v</code></pre>
<ul>
<li>(.48 = 44/92) <code>error</code></li>
<li>(.43 = 40/92) <code>#(1 2 #(3))</code></li>
<li>(.08 = 7/92) <code>#(1 2 #(4))</code></li>
<li>(.01 = 1/92) <code>#(1 2 3)</code></li>
</ul>

## 52. vectors2::alias_mvec_in_mpair
<pre><code>(defvar v (mvec 1 2 3))
(defvar vv (mpair v v))
(vec-set! (right vv) 0 100)
(left vv)</code></pre>
<ul>
<li>(.80 = 74/92) <code>#(100 2 3)</code></li>
<li>(.18 = 17/92) <code>#(1 2 3)</code> [DefsCopyStructs]</li>
<li>(.01 = 1/92) <code>error</code></li>
</ul>

## 53. vectors2::warmup_circularity
<pre><code>(defvar x (mvec 1 0 2))
(vec-set! x 1 x)
(vec-len x)</code></pre>
<ul>
<li>(.76 = 70/92) <code>3</code></li>
<li>(.14 = 13/92) <code>error</code> [NoCircularity]</li>
<li>(.09 = 8/92) <code>run out of memory or time.</code></li>
<li>(.01 = 1/92) <code>+inf</code></li>
</ul>

## 54. vectors2::circularity_and_alias
<pre><code>(defvar v (mpair 10 7))
(set-left! v v)
(set-right! v 42)
(right (left (left v)))</code></pre>
<ul>
<li>(.60 = 55/92) <code>42</code></li>
<li>(.30 = 28/92) <code>error</code> [NoCircularity,
StructsCopyStructs]</li>
<li>(.07 = 6/92) <code>10</code></li>
<li>(.03 = 3/92) <code>7</code></li>
</ul>

## 55. lambda1::smol_quiz_var_as_arg
<pre><code>(defvar x 12)
(deffun (f x)
  (set! x 0))
(f x)
x</code></pre>
<ul>
<li>(.88 = 79/90) <code>12</code></li>
<li>(.12 = 11/90) <code>0</code> [CallByRef, FlatEnv]</li>
</ul>

## 56. lambda1::smol_quiz_seemingly_alias_a_var
<pre><code>(defvar x 5)
(deffun (set1 x y)
  (set! x y))
(deffun (set2 a y)
  (set! x y))
(set1 x 6)
x
(set2 x 7)
x</code></pre>
<ul>
<li>(.66 = 59/90) <code>5 7</code></li>
<li>(.24 = 22/90) <code>5 5</code> [DeepClosure, DefOrSet]</li>
<li>(.09 = 8/90) <code>6 7</code> [CallByRef, FlatEnv]</li>
<li>(.01 = 1/90) <code>error</code></li>
</ul>

## 57. lambda1::smol_quiz_aliasing_mvec_in_mvec
<pre><code>(defvar x (mvec 1 7 3))
(defvar pr (mpair x x))
(vec-set! (right pr) 0 100)
pr</code></pre>
<ul>
<li>(.93 = 84/90) <code>#(#(100 7 3) #(100 7 3))</code></li>
<li>(.07 = 6/90) <code>#(#(1 7 3) #(100 7 3))</code>
[DefsCopyStructs]</li>
</ul>

## 58. lambda1::smol_quiz_circularity
<pre><code>(defvar x (mvec 2 3))
(set-right! x x)
(set-left! x x)
x</code></pre>
<ul>
<li>(.63 = 57/90)
<code>#0='#(#0# #0#) ;; an mpair whose elements refer back to itself</code></li>
<li>(.23 = 21/90) <code>#(#(2 3) #(2 3))</code></li>
<li>(.08 = 7/90) <code>#(#(2 #(2 3)) #(2 3))</code>
[StructsCopyStructs]</li>
<li>(.06 = 5/90) <code>error</code> [NoCircularity]</li>
</ul>

## 59. lambda1::warmup_hof
<pre><code>(deffun (get) 42)
(defvar f get)
(defvar g f)
(g)</code></pre>
<ul>
<li>(.99 = 88/89) <code>42</code></li>
<li>(.01 = 1/89) <code>error</code> [FunNotVal]</li>
</ul>

## 60. lambda1::fun_as_parameter
<pre><code>(deffun (twice f x)
  (f (f x)))
(deffun (double x)
  (+ x x))
(twice double 1)</code></pre>
<ul>
<li>(.83 = 75/90) <code>4</code></li>
<li>(.11 = 10/90) <code>error</code> [FunNotVal]</li>
<li>(.04 = 4/90) <code>2</code></li>
<li>(.01 = 1/90) <code>8</code></li>
</ul>

## 61. lambda1::fun_as_output
<pre><code>(deffun (add1 x) (+ x 1))
(deffun (g) add1)
(defvar f (g))
(f 100)</code></pre>
<ul>
<li>(.71 = 64/90) <code>101</code></li>
<li>(.29 = 26/90) <code>error</code> [FunNotVal, IsolatedFun]</li>
</ul>

## 62. lambda1::fun_in_vectors
<pre><code>(deffun (add1 n)
  (+ n 1))
(defvar v (mvec add1))
((vec-ref v 0) 2)</code></pre>
<ul>
<li>(.78 = 70/90) <code>3</code></li>
<li>(.12 = 11/90) <code>error</code> [FunNotVal]</li>
<li>(.08 = 7/90) <code>2</code></li>
<li>(.02 = 2/90) <code>1</code></li>
</ul>

## 63. lambda2::read_local1
<pre><code>(deffun (make-getter)
  (defvar x 1)
  (deffun (get-x) x)
  get-x)
(defvar get-x (make-getter))
(get-x)</code></pre>
<ul>
<li>(.91 = 82/90) <code>1</code></li>
<li>(.09 = 8/90) <code>error</code> [FunNotVal, IsolatedFun]</li>
</ul>

## 64. lambda2::read_local2
<pre><code>(deffun (make-getter x)
  (deffun (get-x) x)
  get-x)
(defvar get-a (make-getter 1))
(defvar get-b (make-getter 2))
(get-a)
(get-b)</code></pre>
<ul>
<li>(1.00 = 89/89) <code>1 2</code></li>
</ul>

## 65. lambda2::fun_ref_env
<pre><code>(deffun (make-addy y)
  (deffun (addy x)
    (+ x y))
  addy)
(defvar f (make-addy 10))
(defvar g (make-addy 50))
(f 2)
(g 2)</code></pre>
<ul>
<li>(.74 = 66/89) <code>12 52</code></li>
<li>(.25 = 22/89) <code>error</code> [FunNotVal, IsolatedFun]</li>
<li>(.01 = 1/89) <code>12 12</code></li>
</ul>

## 66. lambda2::state
<pre><code>(defvar x 1)
(deffun (make-f)
  (deffun (addx y)
    (+ x y))
  addx)
(defvar f (make-f))
(set! x 2)
(f x)</code></pre>
<ul>
<li>(.50 = 45/90) <code>4</code></li>
<li>(.30 = 27/90) <code>3</code> [DeepClosure]</li>
<li>(.16 = 14/90) <code>error</code> [FunNotVal, IsolatedFun]</li>
<li>(.04 = 4/90) <code>2</code></li>
</ul>

## 67. lambda2::counter
<pre><code>(deffun (make-counter count)
  (deffun (counter)
    (set! count (+ count 1))
    count)
  counter)
(defvar f (make-counter 0))
(defvar g (make-counter 0))

(f)
(f)
(g)</code></pre>
<ul>
<li>(.77 = 69/90) <code>1 2 1</code></li>
<li>(.11 = 10/90) <code>1 2 3</code> [FlatEnv]</li>
<li>(.08 = 7/90) <code>1 1 1</code> [DeepClosure]</li>
<li>(.01 = 1/90) <code>1 1 2</code></li>
<li>(.01 = 1/90) <code>2 3 2</code></li>
<li>(.01 = 1/90) <code>3 1 2</code></li>
<li>(.01 = 1/90) <code>error</code> [DefOrSet, FunNotVal,
IsolatedFun]</li>
</ul>

## 68. lambda2::syntax_pitfall
<pre><code>(deffun (f a b) a + b)
(f 5 10)</code></pre>
<ul>
<li>(.58 = 52/90) <code>15</code></li>
<li>(.32 = 29/90) <code>error</code> [FunNotVal]</li>
<li>(.09 = 8/90) <code>10</code></li>
<li>(.01 = 1/90) <code>5 + 10</code></li>
</ul>

## 69. lambda3::curry_lambda
<pre><code>(deffun (f x)
  (lambda (y) (+ x y)))
(defvar x 0)
((f 2) 1)</code></pre>
<ul>
<li>(.94 = 85/90) <code>3</code></li>
<li>(.03 = 3/90) <code>error</code> [FunNotVal, IsolatedFun]</li>
<li>(.01 = 1/90) <code>1</code></li>
<li>(.01 = 1/90) <code>2</code></li>
</ul>

## 70. lambda3::lambda_remembers_env
<pre><code>(defvar x 1)
(defvar f
  (lambda (y)
    (+ x y)))
(set! x 2)
(f x)</code></pre>
<ul>
<li>(.86 = 77/90) <code>4</code></li>
<li>(.10 = 9/90) <code>3</code> [DeepClosure]</li>
<li>(.03 = 3/90) <code>error</code> [IsolatedFun]</li>
<li>(.01 = 1/90) <code>lambda</code></li>
</ul>

## 71. lambda3::counter_lambda
<pre><code>(deffun (make-counter count)
  (lambda ()
    (set! count (+ count 1))
    count))
(defvar f (make-counter 0))
(defvar g (make-counter 0))

(f)
(f)
(g)</code></pre>
<ul>
<li>(.99 = 89/90) <code>1 2 1</code></li>
<li>(.01 = 1/90) <code>1 2 3</code> [FlatEnv]</li>
</ul>
