---
title: Logical Operations
date: 31-03-2022
private: false
---

<!DOCTYPE html>
<html>

<head>

<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=yes">
<title>rules</title>
</head>

<body>

<h2 id="toc_0">Inference Rules</h2>

<p><em>Basic rules</em>:</p>

<p><strong>mp</strong> </p>

<div><pre><code class="language-none">ϕ → ψ
ϕ
______
ψ</code></pre></div>

<h2 id="toc_1"></h2>

<p><strong>mt</strong> </p>

<div><pre><code class="language-none">ϕ → ψ
¬ψ
______
¬ϕ</code></pre></div>

<h2 id="toc_2"></h2>

<p><strong>dn</strong> </p>

<div><pre><code class="language-none">ϕ               ¬¬ϕ
______          ______
¬¬ϕ             ϕ</code></pre></div>

<p><strong>r</strong> </p>

<div><pre><code class="language-none">ϕ
______
ϕ</code></pre></div>

<p><strong>s</strong> </p>

<div><pre><code class="language-none">ϕ ∧ ψ               ϕ ∧ ψ
______              ______
ϕ                   ψ   </code></pre></div>

<h2 id="toc_3"></h2>

<p><strong>adj</strong> </p>

<div><pre><code class="language-none">ϕ                   ϕ
ψ                   ψ
______              ______
ϕ ∧ ψ               ψ ∧ ϕ   </code></pre></div>

<h2 id="toc_4"></h2>

<p><strong>add</strong> </p>

<div><pre><code class="language-none">ϕ                   ϕ
______              ______
ϕ ∨ ψ               ψ ∨ ϕ   </code></pre></div>

<h2 id="toc_5"></h2>

<p><strong>mtp</strong> </p>

<div><pre><code class="language-none">ϕ ∨ ψ               ϕ ∨ ψ
¬ψ                  ¬ϕ
______              ______
ϕ                   ψ   </code></pre></div>

<h2 id="toc_6"></h2>

<p><strong>cb</strong> </p>

<div><pre><code class="language-none">ϕ → ψ
ψ → ϕ
______
ϕ ↔ ψ                   </code></pre></div>

<h2 id="toc_7"></h2>

<p><strong>bc</strong> </p>

<div><pre><code class="language-none">ϕ ↔ ψ               ϕ ↔ ψ
______              ______
ϕ → ψ               ψ → ϕ   </code></pre></div>

<hr>

<hr>

<p><strong>ui</strong> </p>

<div><pre><code class="language-none">∀αϕα
______
ϕβ</code></pre></div>

<p><code>Provided that β is a name (or a variable) and ϕβ comes from ϕα by proper substitution of β for α.</code></p>

<h2 id="toc_8"></h2>

<p><strong>eg</strong> </p>

<div><pre><code class="language-none">ϕβ
______
∃αϕα</code></pre></div>

<p><code>Provided that α is a variable and ϕβ comes from ϕα by proper substitution of β for α.</code></p>

<h2 id="toc_9"></h2>

<p><strong>ei</strong> </p>

<div><pre><code class="language-none">∃αϕα
______
ϕβ</code></pre></div>

<p><code>Provided that β is a new variable and ϕβ comes from ϕα by proper substitution of β for α.</code></p>

<hr>

<hr>

<p><em>Derived rules</em>:</p>

<p><strong>nc</strong> (T40) </p>

<div><pre><code class="language-none">¬(ϕ → ψ)            ϕ ∧ ¬ψ
_________           _________
ϕ ∧ ¬ψ              ¬(ϕ → ψ)    </code></pre></div>

<h2 id="toc_10"></h2>

<p><strong>cdj</strong> (T45,T46) </p>

<div><pre><code class="language-none">ϕ → ψ               ¬ϕ ∨ ψ              ¬ϕ → ψ           ϕ ∨ ψ
_________           _________         _________         _________
¬ϕ ∨ ψ              ϕ → ψ               ϕ ∨ ψ            ¬ϕ → ψ</code></pre></div>

<h2 id="toc_11"></h2>

<p><strong>sc</strong> (T33,T49) </p>

<div><pre><code class="language-none">ϕ ∨ ψ
ϕ → χ               ϕ → χ
ψ → χ               ¬ϕ → χ  
_________           _________
χ                   χ</code></pre></div>

<h2 id="toc_12"></h2>

<p><strong>dm</strong> (T63-T66) </p>

<div><pre><code class="language-none">¬(ϕ ∧ ψ)        (¬ϕ ∨ ¬ψ)           (ϕ ∧ ψ)            ¬(¬ϕ ∨ ¬ψ)
_________________________________        ___________
 (¬ϕ ∨ ¬ψ)       ¬(ϕ ∧ ψ)           ¬(¬ϕ ∨ ¬ψ)         (ϕ ∧ ψ)

(ϕ ∨ ψ) ¬(ϕ ∨ ψ) ¬(¬ϕ ∧ ¬ψ) (¬ϕ ∧ ¬ψ)

---

¬(¬ϕ ∧ ¬ψ) (¬ϕ ∧ ¬ψ) (ϕ ∨ ψ) ¬(ϕ ∨ ψ)</code></pre></div>

<h2 id="toc_13"></h2>

<p><strong>nb</strong> (T90) </p>

<div><pre><code class="language-none">¬(ϕ ↔ ψ)            (ϕ ↔ ¬ψ)
_________           _________
(ϕ ↔ ¬ψ)            ¬(ϕ ↔ ψ)            </code></pre></div>

<hr>

<p><strong>qn</strong> (T203-T206)</p>

<div><pre><code class="language-none">¬∀xϕx           ¬∃xϕx            ∀xϕx           ∃xϕx
_________________________________    ___________
 ∃x¬ϕx          ∀x¬ϕx            ¬∃x¬ϕx         ¬∀x¬ϕx

¬∀x¬ϕx ¬∃x¬ϕx ∀x¬ϕx ∃x¬ϕx

---

∃xϕx ∀xϕx ¬∃xϕx ¬∀xϕx</code></pre></div>

<h2 id="toc_14"></h2>

<p><strong>av</strong> (T231-T232)</p>

<div><pre><code class="language-none">∀xϕx                    ∃xϕx
______________________
∀yϕy                    ∃yϕy</code></pre></div>

<p><code>Given the total proper substitution of y for x, and provided no variable capturing arises in ϕy.</code></p>

<h2 id="toc_15"></h2>

</body>

</html>
