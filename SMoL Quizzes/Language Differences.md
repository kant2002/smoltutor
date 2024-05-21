# Language Differences

<p>This file explains the differences between <strong>the SMoL
implementation</strong> (which is also the SMoL used in SMoL Quizzes)
and the language as presented in the paper (hereafter, <em>the Paper
SMoL</em>).</p>
<h2 id="the-smol-implementation-contains-more-language-constructs">The
SMoL implementation contains more language constructs</h2>
<p>In the paper, we leave out the following constructs because they are
irrelevant to any programs that we present in the paper:</p>
<ul>
<li><code>let*</code> and <code>letrec</code>, which mean the same thing
as in Racket.</li>
</ul>
<p>We leave out the following constructs because they are irrelevant to
any misconceptions that we present in the paper:</p>
<ul>
<li>lists operators: <code>empty</code>, <code>cons</code>,
<code>empty?</code>, and <code>append</code></li>
<li>higher-order functions: <code>filter</code>, <code>map</code>,
<code>foldl</code>, <code>foldr</code></li>
<li>string concatenation: <code>++</code></li>
<li>equality: <code>equal?</code>, which test for structural
equality</li>
<li>logic: <code>and</code>, <code>or</code>, and <code>not</code></li>
<li>immutable vectors: <code>ivec</code>, <code>pair</code>, and
<code>ipair</code> (these operators work like their
<code>m</code>-version but create immutable vectors)</li>
<li>testing: <code>test</code></li>
<li>debugging: <code>spy</code>, which prints a value with debugging
information</li>
<li>predicates: <code>zero?</code></li>
</ul>
<h2 id="the-smol-implementation-has-three-language-levels">The SMoL
implementation has three language levels</h2>
<p>The SMoL implementation having three levels (i.e.,
<code>smol/fun</code>, <code>smol/state</code>, and
<code>smol/fun</code>) as explained in the paper. These levels
correspond to the three quizzes.</p>
<h2 id="the-smol-implementation-permits-more-shadowing">The SMoL
implementation permits more shadowing</h2>
<p>The Paper SMoL does not specify whether local variables defined in a
function body reside in the same environment as the function parameters.
For example, the behavior of the following program is unspecified</p>
<pre><code>(deffun (f x)
  (defvar x 1)
  x)
(f 0)</code></pre>
<p>The program could either error (because <code>x</code> is defined
twice in the same environment) or produce <code>1</code> (because the
local <code>x</code> shadows the parameter <code>x</code>). The SMoL
implementation assumes the shadowing behavior.</p>
