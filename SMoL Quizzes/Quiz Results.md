## Quiz 1

<h3 id="arithmetic-operators">arithmetic operators</h3>
<pre><code>(deffun (f o) (o 1 1))
(f +)</code></pre>
<ul>
<li>(.61 = 80/131) <code>2</code></li>
<li>(.20 = 26/131) <code>Error</code> [FunNotVal]</li>
<li>(.19 = 25/131) <code>Syntax error</code></li>
</ul>
<h3 id="as-condition">0 as condition</h3>
<pre><code>(if 0 #t #f)</code></pre>
<ul>
<li>(.47 = 62/131) <code>#f</code></li>
<li>(.46 = 60/131) <code>#t</code></li>
<li>(.05 = 7/131) <code>Other: Error</code></li>
<li>(.01 = 1/131) <code>Other: #f</code></li>
<li>(.01 = 1/131) <code>Other: I don't know</code></li>
</ul>
<h3 id="redeclare-var-using-defvar">redeclare var using defvar</h3>
<pre><code>(defvar x 0)
(defvar y x)
(defvar x 2)
x
y</code></pre>
<ul>
<li>(.59 = 77/131) <code>2; 0</code> [DefOrSet, NestedDef]</li>
<li>(.32 = 42/131) <code>Error</code></li>
<li>(.04 = 5/131) <code>Other: 2; 2</code></li>
<li>(.03 = 4/131) <code>Nothing is printed</code></li>
<li>(.02 = 3/131) <code>0; 0</code></li>
</ul>
<h3 id="expose-local-defvar">expose local defvar</h3>
<pre><code>(defvar x 42)
(deffun (create)
  (defvar y 42)
  y)
(create)
(equal? x y)</code></pre>
<ul>
<li>(.65 = 85/131) <code>Error</code></li>
<li>(.29 = 38/131) <code>42; #t</code> [FlatEnv]</li>
<li>(.05 = 6/131) <code>Other: 42; Error</code></li>
<li>(.01 = 1/131) <code>Other: #t</code></li>
<li>(.01 = 1/131) <code>Other: I don't know</code></li>
</ul>
<h3 id="pair">pair?</h3>
<pre><code>(pair? (pair 1 2))
(pair? (ivec 1 2))
(pair? &#39;#(1 2))
(pair? &#39;(1 2))</code></pre>
<ul>
<li>(.44 = 57/131) <code>#t; #t; #t; #f</code></li>
<li>(.27 = 35/131) <code>#t; #t; #t; #t</code></li>
<li>(.14 = 18/131) <code>#t; #f; #t; #f</code></li>
<li>(.06 = 8/131) <code>Other: #t; #f; #f; #t</code></li>
<li>(.03 = 4/131) <code>Other: #t; #t; #f; #f</code></li>
<li>(.02 = 3/131) <code>Other: #t; #f; #f; #f</code></li>
<li>(.02 = 2/131) <code>Other: #t; #t; #f; #t</code></li>
<li>(.02 = 2/131) <code>Other: I don't know</code></li>
<li>(.01 = 1/131) <code>Other: Error</code></li>
<li>(.01 = 1/131) <code>Other: Error; #f; #f; #t</code></li>
</ul>
<h3 id="let-and-let">let* and let</h3>
<pre><code>(let* ([v 1]
       [w (+ v 2)]
       [y (* w w)])
  (let ([v 3]
        [y (* v w)])
    y))</code></pre>
<ul>
<li>(.51 = 67/131) <code>9</code></li>
<li>(.33 = 43/131) <code>Other: 3</code></li>
<li>(.13 = 17/131) <code>27</code></li>
<li>(.02 = 2/131) <code>Other: Error</code></li>
<li>(.01 = 1/131) <code>Other: 15</code></li>
<li>(.01 = 1/131) <code>Other: 81</code></li>
</ul>
<h3 id="defvar-and-let">defvar and let</h3>
<pre><code>(defvar x 3)
(defvar y (let ([y 6] [x 5]) x))
(* x y)</code></pre>
<ul>
<li>(.77 = 101/131) <code>Other: 15</code></li>
<li>(.09 = 12/131) <code>9</code></li>
<li>(.08 = 11/131) <code>25</code> [FlatEnv]</li>
<li>(.02 = 3/131) <code>Other: 30</code></li>
<li>(.02 = 2/131) <code>Other: Error</code></li>
<li>(.01 = 1/131) <code>Other: 18</code></li>
<li>(.01 = 1/131) <code>Other: 90</code></li>
</ul>
<h3 id="fun-id-equals-to-arg-id">fun-id equals to arg-id</h3>
<pre><code>(deffun (f f) f)
(f 5)</code></pre>
<ul>
<li>(.53 = 70/131) <code>5</code></li>
<li>(.46 = 60/131) <code>Error</code></li>
<li>(.01 = 1/131) <code>Other: 5</code></li>
</ul>
<h3 id="scoping-rule-of-let">scoping rule of let</h3>
<pre><code>(let ([x 4]
      [y (+ x 10)])
  y)</code></pre>
<ul>
<li>(.51 = 67/131) <code>14</code></li>
<li>(.48 = 63/131) <code>Error</code></li>
<li>(.01 = 1/131) <code>Other: Nothing is printed</code></li>
</ul>
<h3 id="the-right-component-of-ivec">the right component of ivec</h3>
<pre><code>(right (ivec 1 2 3))</code></pre>
<ul>
<li>(.77 = 101/131) <code>Error</code></li>
<li>(.13 = 17/131) <code>2</code></li>
<li>(.05 = 7/131) <code>Other: 3</code></li>
<li>(.02 = 3/131) <code>Other: I don't know</code></li>
<li>(.01 = 1/131) <code>Other: #'(2 3)</code></li>
<li>(.01 = 1/131) <code>Other: 6</code></li>
<li>(.01 = 1/131) <code>Other: Nothing is printed</code></li>
</ul>
<h3 id="identifiers">identifiers</h3>
<pre><code>(defvar x 5)
(deffun (reassign var_name new_val)
  (defvar var_name new_val)
  (pair var_name x))
(reassign x 6)
x</code></pre>
<ul>
<li>(.53 = 70/131) <code>'#(6 5); 5</code> [DefOrSet, NestedDef]</li>
<li>(.20 = 26/131) <code>Error</code></li>
<li>(.11 = 15/131) <code>'#(6 6); 5</code></li>
<li>(.11 = 15/131) <code>'#(6 6); 6</code></li>
<li>(.02 = 2/131) <code>Nothing is printed</code></li>
<li>(.01 = 1/131) <code>Other: (5 6)</code></li>
<li>(.01 = 1/131) <code>Other: 6</code></li>
<li>(.01 = 1/131) <code>Other: I don't know</code></li>
</ul>
<h3 id="defvar-deffun-and-let">defvar, deffun, and let</h3>
<pre><code>(defvar a 1)
(deffun (what-is-a) a)
(let ([a 2])
  (ivec
   (what-is-a)
   a))</code></pre>
<ul>
<li>(.82 = 108/131) <code>‘#(1 2)</code></li>
<li>(.15 = 20/131) <code>‘#(2 2)</code></li>
<li>(.01 = 1/131) <code>Other: '#(1 1)</code></li>
<li>(.01 = 1/131) <code>Other: I don't know</code></li>
<li>(.01 = 1/131) <code>Other: Nothing is printed</code></li>
</ul>
<h3 id="syntax-pitfall">syntax pitfall</h3>
<pre><code>(deffun (f a b) a + b)
(f 5 10)</code></pre>
<ul>
<li>(.50 = 65/131) <code>15</code></li>
<li>(.37 = 48/131) <code>Error</code> [FunNotVal]</li>
<li>(.11 = 15/131) <code>Other: 10</code></li>
<li>(.02 = 2/131) <code>5</code></li>
<li>(.01 = 1/131) <code>Other: 5; 10</code></li>
</ul>
<h2 id="quiz-2">Quiz 2</h2>
<h3 id="circularity">circularity</h3>
<pre><code>(defvar x (mvec 2 3))
(set-right! x x)
(set-left! x x)
x</code></pre>
<ul>
<li>(.50 = 51/102) <code>'#(#(2 #(2 3)) #(2 3))</code>
[StructsCopyStructs]</li>
<li>(.29 = 30/102)
<code>x='#(x x) or something similar. Both (left x) and (right x) are x itself.</code></li>
<li>(.16 = 16/102) <code>Error</code> [NoCircularity]</li>
<li>(.01 = 1/102) <code>Other: #(#(2 3) #(2 3))</code></li>
<li>(.01 = 1/102) <code>Other: '#(#(2 3) #(2 3))</code></li>
<li>(.01 = 1/102) <code>Other: (2 (2 3) (2 (2 3)))</code></li>
<li>(.01 = 1/102) <code>Other: I don't know</code></li>
<li>(.01 = 1/102) <code>Other: Error</code> [NoCircularity]</li>
</ul>
<h3 id="eval-order">eval order</h3>
<pre><code>(defvar x 0)
(ivec x (begin (set! x 1) x) x)</code></pre>
<ul>
<li>(.71 = 68/96) <code>'#(0 1 1)</code></li>
<li>(.18 = 17/96) <code>'#(0 1 0)</code></li>
<li>(.10 = 10/96) <code>'#(1 1 1)</code></li>
<li>(.01 = 1/96) <code>Other: Error</code></li>
</ul>
<h3 id="mvec-as-arg">mvec as arg</h3>
<pre><code>(defvar x (mvec 1 2))
(deffun (f x)
  (vset! x 0 0))
(f x)
x</code></pre>
<ul>
<li>(.87 = 86/99) <code>'#(0 2)</code></li>
<li>(.08 = 8/99) <code>'#(1 2)</code> [CallsCopyStructs]</li>
<li>(.02 = 2/99) <code>Other: '#(0 0)</code></li>
<li>(.02 = 2/99) <code>Other: Error</code></li>
<li>(.01 = 1/99) <code>Other: Nothing is printed</code></li>
</ul>
<h3 id="var-as-arg">var as arg</h3>
<pre><code>(defvar x 12)
(deffun (f x)
  (set! x 0))
(f x)
x</code></pre>
<ul>
<li>(.65 = 65/100) <code>12</code></li>
<li>(.31 = 31/100) <code>0</code> [CallByRef, FlatEnv]</li>
<li>(.02 = 2/100) <code>Other: Error</code></li>
<li>(.01 = 1/100) <code>Other: 123</code></li>
<li>(.01 = 1/100) <code>Other: Nothing is printed</code></li>
</ul>
<h3 id="seemly-aliasing-a-var">seemly aliasing a var</h3>
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
<li>(.59 = 59/100) <code>Other: 5; 7</code></li>
<li>(.27 = 27/100) <code>6; 7</code> [CallByRef, FlatEnv]</li>
<li>(.11 = 11/100) <code>5; 5</code> [DeepClosure, DefOrSet]</li>
<li>(.02 = 2/100) <code>Other: Error</code></li>
<li>(.01 = 1/100) <code>Other: 5; 6</code></li>
</ul>
<h3 id="mutable-var-in-vec">mutable var in vec</h3>
<pre><code>(defvar x 3)
(defvar v (mvec 1 2 x))
(set! x 4)
v
x</code></pre>
<ul>
<li>(.84 = 81/96) <code>'#(1 2 3); 4</code></li>
<li>(.14 = 13/96) <code>'#(1 2 4); 4</code> [StructByRef]</li>
<li>(.01 = 1/96) <code>Other: '#(1 2 3); 3</code></li>
<li>(.01 = 1/96) <code>Other: Error</code></li>
</ul>
<h3 id="aliasing-mvec-in-mvec">aliasing mvec in mvec</h3>
<pre><code>(defvar v (mvec 1 2 3 4))
(defvar vv (mvec v v))(vset! (vref vv 1) 0 100)
vv</code></pre>
<ul>
<li>(.62 = 61/99) <code>'#(#(100 2 3 4) #(100 2 3 4))</code></li>
<li>(.26 = 26/99) <code>'#(#(1 2 3 4) #(100 2 3 4))</code>
[DefsCopyStructs, StructsCopyStructs]</li>
<li>(.06 = 6/99) <code>Error</code></li>
<li>(.04 = 4/99) <code>'#(#(1 2 3 4) #(1 2 3 4))</code></li>
<li>(.01 = 1/99) <code>Other: '#(#(0 2 3 4) #(100 2 3 4))</code></li>
<li>(.01 = 1/99) <code>Other: #(#(1 2 3 4) #(0 100))</code></li>
</ul>
<h3 id="vset-in-let">vset! in let</h3>
<pre><code>(defvar x (mvec 123))
(let ([y x])
  (vset! y 0 10))
x</code></pre>
<ul>
<li>(.59 = 55/94) <code>'#(10)</code></li>
<li>(.36 = 34/94) <code>'#(123)</code> [DefsCopyStructs]</li>
<li>(.01 = 1/94) <code>Other: '#(0 1 1)</code></li>
<li>(.01 = 1/94) <code>Other: '#(0 10)</code></li>
<li>(.01 = 1/94) <code>Other: '#(1023)</code></li>
<li>(.01 = 1/94) <code>Other: I don't know</code></li>
<li>(.01 = 1/94) <code>Other: Error</code></li>
</ul>
<h3 id="set-in-let">set! in let</h3>
<pre><code>(defvar x 123)
(let ([y x])
  (set! y 10))
x</code></pre>
<ul>
<li>(.85 = 75/88) <code>123</code></li>
<li>(.14 = 12/88) <code>10</code> [DefByRef]</li>
<li>(.01 = 1/88) <code>Other: '#(1 2 3); 4</code></li>
</ul>
<h3 id="seemingly-aliasing-a-var-again">seemingly aliasing a var
again</h3>
<pre><code>(defvar x 10)
(deffun (f y z)
  (set! x z)
  y)
(f x 20)
x</code></pre>
<ul>
<li>(.88 = 84/96) <code>10; 20</code></li>
<li>(.09 = 9/96) <code>20; 20</code> [CallByRef]</li>
<li>(.02 = 2/96) <code>Other: 10; 10</code> [DeepClosure, DefOrSet]</li>
<li>(.01 = 1/96) <code>Other: Error</code> [IsolatedFun]</li>
</ul>
<h2 id="quiz-3">Quiz 3</h2>
<h3 id="fun-returns-lambda">fun returns lambda</h3>
<pre><code>(deffun (f x)
  (lambda (y) (+ x y)))
((f 2) 1)</code></pre>
<ul>
<li>(.82 = 84/102) <code>3</code></li>
<li>(.17 = 17/102) <code>Error</code> [FunNotVal, IsolatedFun]</li>
<li>(.01 = 1/102) <code>Other: #&lt;procedure&gt;</code></li>
</ul>
<h3 id="filter-gt">filter gt</h3>
<pre><code>(filter (lambda (n) (&gt; 3 n)) &#39;(1 2 3 4 5))</code></pre>
<ul>
<li>(.75 = 76/102) <code>‘(1 2)</code></li>
<li>(.22 = 22/102) <code>‘(4 5)</code></li>
<li>(.01 = 1/102) <code>Other: '(0 1)</code></li>
<li>(.01 = 1/102) <code>Other: '(1 2 3)</code></li>
<li>(.01 = 1/102) <code>Other: '(3 4 5)</code></li>
<li>(.01 = 1/102) <code>Other: Error</code></li>
</ul>
<h3 id="fun-and-state-14">fun and state 1/4</h3>
<pre><code>(defvar x 1)
(defvar f
  (lambda (y)
    (+ x y)))
(set! x 2)
(f x)</code></pre>
<ul>
<li>(.74 = 75/102) <code>4</code></li>
<li>(.21 = 21/102) <code>3</code> [DeepClosure]</li>
<li>(.06 = 6/102) <code>Other: Error</code> [IsolatedFun]</li>
</ul>
<h3 id="fun-and-state-24">fun and state 2/4</h3>
<pre><code>(defvar x 1)
(deffun (f y)
  (+ x y))
(set! x 2)
(f x)</code></pre>
<ul>
<li>(.87 = 89/102) <code>4</code></li>
<li>(.10 = 10/102) <code>3</code> [DeepClosure]</li>
<li>(.03 = 3/102) <code>Other: Error</code> [IsolatedFun]</li>
</ul>
<h3 id="fun-and-state-34">fun and state 3/4</h3>
<pre><code>(defvar x 1)
(defvar f
  (lambda (y)
    (+ x y)))
(let ([x 2])
  (f x))</code></pre>
<ul>
<li>(.78 = 80/102) <code>3</code></li>
<li>(.13 = 13/102) <code>4</code> [FlatEnv]</li>
<li>(.06 = 6/102) <code>Other: Error</code> [IsolatedFun]</li>
<li>(.02 = 2/102) <code>Other: 2</code></li>
<li>(.01 = 1/102) <code>Other: #&lt;procedure&gt;</code></li>
</ul>
<h3 id="fun-and-state-44">fun and state 4/4</h3>
<pre><code>(defvar x 1)
(deffun (f y)
  (+ x y))
(let ([x 2])
  (f x))</code></pre>
<ul>
<li>(.89 = 91/102) <code>3</code></li>
<li>(.09 = 9/102) <code>4</code> [FlatEnv]</li>
<li>(.02 = 2/102) <code>Other: Error</code> [IsolatedFun]</li>
</ul>
<h3 id="eval-order-1">eval order</h3>
<pre><code>(deffun (f x) (+ x 1))
(deffun (new-f x) (* x x))
(f (begin
     (set! f new-f)
     10))</code></pre>
<ul>
<li>(.42 = 43/102) <code>Other: 11</code></li>
<li>(.30 = 31/102) <code>100</code></li>
<li>(.25 = 25/102) <code>Error</code> [FunNotVal]</li>
<li>(.01 = 1/102) <code>Other: 1</code></li>
<li>(.01 = 1/102) <code>Other: 101</code></li>
<li>(.01 = 1/102) <code>Other: 121</code></li>
</ul>
<h3 id="counter">Counter</h3>
<pre><code>(deffun (make-counter)
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
(g)</code></pre>
<ul>
<li>(.62 = 63/102) <code>1; 1; 2; 3; 2</code></li>
<li>(.34 = 35/102) <code>1; 1; 1; 1; 1</code> [DeepClosure]</li>
<li>(.01 = 1/102) <code>1; 1; 2; 3; 4</code></li>
<li>(.01 = 1/102)
<code>Other: #&lt;procedure:f&gt;; #&lt;procedure:g&gt;; #&lt;procedure:f&gt;; #&lt;procedure:f&gt;; #&lt;procedure:g&gt;</code></li>
<li>(.01 = 1/102) <code>Other: 1; 1; 1; 2; 1</code></li>
<li>(.01 = 1/102) <code>Other: Error</code> [DefOrSet, IsolatedFun]</li>
</ul>
<h3 id="hof-set">hof + set!</h3>
<pre><code>(defvar y 3)
(+ ((lambda (x) (set! y 0) (+ x y)) 1)
   y)</code></pre>
<ul>
<li>(.70 = 71/102) <code>Other: 1</code></li>
<li>(.18 = 18/102) <code>4</code> [DeepClosure, DefOrSet]</li>
<li>(.10 = 10/102) <code>Error</code> [FunNotVal, IsolatedFun]</li>
<li>(.02 = 2/102) <code>Other: 2</code></li>
<li>(.01 = 1/102) <code>7</code></li>
</ul>
<h3 id="filter">filter</h3>
<pre><code>(defvar l (list (ivec) (ivec 1) (ivec 2 3)))
(filter (lambda (x) (vlen x)) l)</code></pre>
<ul>
<li>(.51 = 52/102) <code>'(#() #(1) #(2 3))</code></li>
<li>(.24 = 24/102) <code>Error</code></li>
<li>(.16 = 16/102) <code>'(#(1) #(2 3))</code></li>
<li>(.07 = 7/102) <code>‘(0 1 2)</code></li>
<li>(.01 = 1/102) <code>Other: '(#() #(2 3))</code></li>
<li>(.01 = 1/102) <code>Other: '()</code></li>
<li>(.01 = 1/102) <code>Other: I don't know</code></li>
</ul>
<h3 id="eq-fun-fun-13">eq? fun fun 1/3</h3>
<pre><code>(eq? (λ (x) (+ x x))
     (λ (x) (+ x x)))</code></pre>
<ul>
<li>(.73 = 74/102) <code>#f</code></li>
<li>(.16 = 16/102) <code>#t</code></li>
<li>(.12 = 12/102) <code>Other: Error</code></li>
</ul>
<h3 id="eq-fun-fun-23">eq? fun fun 2/3</h3>
<pre><code>(deffun (f x) (+ x x))
(deffun (g x) (+ x x))
(eq? f g)</code></pre>
<ul>
<li>(.80 = 82/102) <code>#f</code></li>
<li>(.11 = 11/102) <code>Other: Error</code> [FunNotVal]</li>
<li>(.09 = 9/102) <code>#t</code></li>
</ul>
<h3 id="eq-fun-fun-33">eq? fun fun 3/3</h3>
<pre><code>(deffun (f x) (+ x x))
(deffun (g) f)
(eq? f (g))</code></pre>
<ul>
<li>(.77 = 79/102) <code>#t</code></li>
<li>(.15 = 15/102) <code>#f</code></li>
<li>(.08 = 8/102) <code>Other: Error</code> [FunNotVal,
IsolatedFun]</li>
</ul>
<h3 id="equal-fun-fun">equal? fun fun</h3>
<pre><code>(deffun (f) (lambda () 1))
(equal? (f) (f))</code></pre>
<ul>
<li>(.50 = 51/102) <code>#t</code></li>
<li>(.40 = 41/102) <code>#f</code></li>
<li>(.10 = 10/102) <code>Other: Error</code></li>
</ul>
