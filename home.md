---
hide:
  - navigation
  - toc
---

# Algorithm Coding Interview

<div class="algo-hero" markdown="0">
  <div class="algo-hero__text">
    <div class="algo-hero__tag">// coding interview notes</div>
    <h1 class="algo-hero__title">Algorithm<br><span>Coding Interview</span></h1>
    <p class="algo-hero__desc">按数据结构与解题模式（pattern）整理的算法面试题。每题包含题目、思路与 Java 题解，先看模式总结，再刷对应题目。</p>
    <div class="algo-hero__stats">
      <div><b>112</b><span>道题</span></div>
      <div><b>7</b><span>大类</span></div>
      <div><b>Java</b><span>题解</span></div>
    </div>
    <div class="algo-hero__actions">
      <a class="algo-btn algo-btn--solid" href="_sections/s1/">开始刷题</a>
      <a class="algo-btn algo-btn--line" href="https://github.com/whicter/leetcode-java">GitHub</a>
    </div>
  </div>
  <div class="algo-code">
    <div class="algo-code__bar"><i></i><i></i><i></i><span>TwoPointers.java</span></div>
<pre class="algo-code__body"><code><span class="k">int</span> left = <span class="n">0</span>, right = nums.length - <span class="n">1</span>;
<span class="k">while</span> (left &lt; right) {
    <span class="k">int</span> sum = nums[left] + nums[right];
    <span class="k">if</span> (sum == target) {
        <span class="k">return new int</span>[]{left, right};
    } <span class="k">else if</span> (sum &lt; target) {
        left++;      <span class="c">// need a bigger sum</span>
    } <span class="k">else</span> {
        right--;     <span class="c">// need a smaller sum</span>
    }
}</code></pre>
  </div>
</div>

<div class="algo-section-head">
  <h2>Patterns</h2>
  <p>按模式选一类开始：每类先读总结页，再做题</p>
</div>

<!-- KB_MODULE_CARDS:tiles -->
