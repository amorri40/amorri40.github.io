---
layout: post
title: "Interpreters101"
description: ""
category: [ComputerScience, Java, Android]
tags: []
---
{% include JB/setup %}

<div class="article-content entry-content" itemprop="articleBody">While watching "Google I/O 2008 - Dalvik Virtual Machine Internals" (<a href="http://www.youtube.com/watch?v=ptjedOZEXPM">http://www.youtube.com/watch?v=ptjedOZEXPM</a>) they demonstrated a great example of how a simple bytecode interpreter is implemented. Since I am&nbsp;fascinated&nbsp;by the inner workings of compilers and VM/interpreters I thought I would share the example here for anyone else that is interested.<br>
<br>
The first example is the simplest version, a simple for loop that loops over each byte and depending on the value of each byte it will execute a different command, this version is very portable as it doesn't use any low level assembly code, so this example can be compiled for many different platforms.<br>
<br>
<div class="gistLoad" data-id="2140090" id="gist-2140090"><br><link rel="stylesheet" href="https://assets-cdn.github.com/assets/gist-embed-08527ef2b62c06e4f818538458263d7d9e4bd82a210e7da0b973d9690adc8889.css"><div id="gist2140090" class="gist">
    <div class="gist-file">
      <div class="gist-data">
        <div class="js-gist-file-update-container js-task-list-container file-box">
  <div id="file-interpreter101_simple-cpp" class="file">


  <div itemprop="text" class="blob-wrapper data type-c">
      <table class="highlight tab-size js-file-line-container" data-tab-size="8">
      <tbody><tr>
        <td id="file-interpreter101_simple-cpp-L1" class="blob-num js-line-number" data-line-number="1"></td>
        <td id="file-interpreter101_simple-cpp-LC1" class="blob-code blob-code-inner js-file-line"><span class="pl-c"><span class="pl-c">/*</span></span></td>
      </tr>
      <tr>
        <td id="file-interpreter101_simple-cpp-L2" class="blob-num js-line-number" data-line-number="2"></td>
        <td id="file-interpreter101_simple-cpp-LC2" class="blob-code blob-code-inner js-file-line"><span class="pl-c">Google I/O 2008 - Dalvik Virtual Machine Internals</span></td>
      </tr>
      <tr>
        <td id="file-interpreter101_simple-cpp-L3" class="blob-num js-line-number" data-line-number="3"></td>
        <td id="file-interpreter101_simple-cpp-LC3" class="blob-code blob-code-inner js-file-line"><span class="pl-c">Interpreters 101, toy interpreter</span></td>
      </tr>
      <tr>
        <td id="file-interpreter101_simple-cpp-L4" class="blob-num js-line-number" data-line-number="4"></td>
        <td id="file-interpreter101_simple-cpp-LC4" class="blob-code blob-code-inner js-file-line"><span class="pl-c">This is a simple toy bytecode interpreter</span></td>
      </tr>
      <tr>
        <td id="file-interpreter101_simple-cpp-L5" class="blob-num js-line-number" data-line-number="5"></td>
        <td id="file-interpreter101_simple-cpp-LC5" class="blob-code blob-code-inner js-file-line"><span class="pl-c"><span class="pl-c">*/</span></span></td>
      </tr>
      <tr>
        <td id="file-interpreter101_simple-cpp-L6" class="blob-num js-line-number" data-line-number="6"></td>
        <td id="file-interpreter101_simple-cpp-LC6" class="blob-code blob-code-inner js-file-line">
</td>
      </tr>
      <tr>
        <td id="file-interpreter101_simple-cpp-L7" class="blob-num js-line-number" data-line-number="7"></td>
        <td id="file-interpreter101_simple-cpp-LC7" class="blob-code blob-code-inner js-file-line">#<span class="pl-k">include</span> <span class="pl-s"><span class="pl-pds">&lt;</span>cstdio<span class="pl-pds">&gt;</span></span></td>
      </tr>
      <tr>
        <td id="file-interpreter101_simple-cpp-L8" class="blob-num js-line-number" data-line-number="8"></td>
        <td id="file-interpreter101_simple-cpp-LC8" class="blob-code blob-code-inner js-file-line">
</td>
      </tr>
      <tr>
        <td id="file-interpreter101_simple-cpp-L9" class="blob-num js-line-number" data-line-number="9"></td>
        <td id="file-interpreter101_simple-cpp-LC9" class="blob-code blob-code-inner js-file-line"><span class="pl-k">static</span> <span class="pl-k">void</span> <span class="pl-en">interpreter</span>(<span class="pl-k">const</span> <span class="pl-k">char</span>* stringOfBytecode);</td>
      </tr>
      <tr>
        <td id="file-interpreter101_simple-cpp-L10" class="blob-num js-line-number" data-line-number="10"></td>
        <td id="file-interpreter101_simple-cpp-LC10" class="blob-code blob-code-inner js-file-line">
</td>
      </tr>
      <tr>
        <td id="file-interpreter101_simple-cpp-L11" class="blob-num js-line-number" data-line-number="11"></td>
        <td id="file-interpreter101_simple-cpp-LC11" class="blob-code blob-code-inner js-file-line"><span class="pl-k">int</span> <span class="pl-en">main</span>(<span class="pl-k">int</span> argc, <span class="pl-k">char</span> *argv[]) {</td>
      </tr>
      <tr>
        <td id="file-interpreter101_simple-cpp-L12" class="blob-num js-line-number" data-line-number="12"></td>
        <td id="file-interpreter101_simple-cpp-LC12" class="blob-code blob-code-inner js-file-line">	<span class="pl-c1">interpreter</span>(<span class="pl-s"><span class="pl-pds">"</span>abcbbbbde<span class="pl-pds">"</span></span>);</td>
      </tr>
      <tr>
        <td id="file-interpreter101_simple-cpp-L13" class="blob-num js-line-number" data-line-number="13"></td>
        <td id="file-interpreter101_simple-cpp-LC13" class="blob-code blob-code-inner js-file-line">}</td>
      </tr>
      <tr>
        <td id="file-interpreter101_simple-cpp-L14" class="blob-num js-line-number" data-line-number="14"></td>
        <td id="file-interpreter101_simple-cpp-LC14" class="blob-code blob-code-inner js-file-line">
</td>
      </tr>
      <tr>
        <td id="file-interpreter101_simple-cpp-L15" class="blob-num js-line-number" data-line-number="15"></td>
        <td id="file-interpreter101_simple-cpp-LC15" class="blob-code blob-code-inner js-file-line"><span class="pl-k">static</span> <span class="pl-k">void</span> <span class="pl-en">interpreter</span>(<span class="pl-k">const</span> <span class="pl-k">char</span>* stringOfBytecode) {</td>
      </tr>
      <tr>
        <td id="file-interpreter101_simple-cpp-L16" class="blob-num js-line-number" data-line-number="16"></td>
        <td id="file-interpreter101_simple-cpp-LC16" class="blob-code blob-code-inner js-file-line">	<span class="pl-k">for</span> (;;) {</td>
      </tr>
      <tr>
        <td id="file-interpreter101_simple-cpp-L17" class="blob-num js-line-number" data-line-number="17"></td>
        <td id="file-interpreter101_simple-cpp-LC17" class="blob-code blob-code-inner js-file-line">		<span class="pl-k">switch</span> (*(stringOfBytecode++)) {</td>
      </tr>
      <tr>
        <td id="file-interpreter101_simple-cpp-L18" class="blob-num js-line-number" data-line-number="18"></td>
        <td id="file-interpreter101_simple-cpp-LC18" class="blob-code blob-code-inner js-file-line">			<span class="pl-k">case</span> <span class="pl-s"><span class="pl-pds">'</span>a<span class="pl-pds">'</span></span>: <span class="pl-c1">printf</span>(<span class="pl-s"><span class="pl-pds">"</span>Hell<span class="pl-pds">"</span></span>); <span class="pl-k">break</span>;</td>
      </tr>
      <tr>
        <td id="file-interpreter101_simple-cpp-L19" class="blob-num js-line-number" data-line-number="19"></td>
        <td id="file-interpreter101_simple-cpp-LC19" class="blob-code blob-code-inner js-file-line">			<span class="pl-k">case</span> <span class="pl-s"><span class="pl-pds">'</span>b<span class="pl-pds">'</span></span>: <span class="pl-c1">printf</span>(<span class="pl-s"><span class="pl-pds">"</span>o<span class="pl-pds">"</span></span>); <span class="pl-k">break</span>;</td>
      </tr>
      <tr>
        <td id="file-interpreter101_simple-cpp-L20" class="blob-num js-line-number" data-line-number="20"></td>
        <td id="file-interpreter101_simple-cpp-LC20" class="blob-code blob-code-inner js-file-line">			<span class="pl-k">case</span> <span class="pl-s"><span class="pl-pds">'</span>c<span class="pl-pds">'</span></span>: <span class="pl-c1">printf</span>(<span class="pl-s"><span class="pl-pds">"</span> w<span class="pl-pds">"</span></span>); <span class="pl-k">break</span>;</td>
      </tr>
      <tr>
        <td id="file-interpreter101_simple-cpp-L21" class="blob-num js-line-number" data-line-number="21"></td>
        <td id="file-interpreter101_simple-cpp-LC21" class="blob-code blob-code-inner js-file-line">			<span class="pl-k">case</span> <span class="pl-s"><span class="pl-pds">'</span>d<span class="pl-pds">'</span></span>: <span class="pl-c1">printf</span>(<span class="pl-s"><span class="pl-pds">"</span>rld!<span class="pl-cce">\n</span><span class="pl-pds">"</span></span>); <span class="pl-k">break</span>;</td>
      </tr>
      <tr>
        <td id="file-interpreter101_simple-cpp-L22" class="blob-num js-line-number" data-line-number="22"></td>
        <td id="file-interpreter101_simple-cpp-LC22" class="blob-code blob-code-inner js-file-line">			<span class="pl-k">case</span> <span class="pl-s"><span class="pl-pds">'</span>e<span class="pl-pds">'</span></span>: <span class="pl-k">return</span>;</td>
      </tr>
      <tr>
        <td id="file-interpreter101_simple-cpp-L23" class="blob-num js-line-number" data-line-number="23"></td>
        <td id="file-interpreter101_simple-cpp-LC23" class="blob-code blob-code-inner js-file-line">		}</td>
      </tr>
      <tr>
        <td id="file-interpreter101_simple-cpp-L24" class="blob-num js-line-number" data-line-number="24"></td>
        <td id="file-interpreter101_simple-cpp-LC24" class="blob-code blob-code-inner js-file-line">	}</td>
      </tr>
      <tr>
        <td id="file-interpreter101_simple-cpp-L25" class="blob-num js-line-number" data-line-number="25"></td>
        <td id="file-interpreter101_simple-cpp-LC25" class="blob-code blob-code-inner js-file-line">	</td>
      </tr>
      <tr>
        <td id="file-interpreter101_simple-cpp-L26" class="blob-num js-line-number" data-line-number="26"></td>
        <td id="file-interpreter101_simple-cpp-LC26" class="blob-code blob-code-inner js-file-line">}</td>
      </tr>
</tbody></table>

  </div>

  </div>

</div>

      </div>
      <div class="gist-meta">
        <a href="https://gist.github.com/amorri40/2140090/raw/c2f39bb63b86939f0b2f11cc4d75949e08bc5707/Interpreter101_simple.cpp" style="float:right">view raw</a>
        <a href="https://gist.github.com/amorri40/2140090#file-interpreter101_simple-cpp">Interpreter101_simple.cpp</a>
        hosted with ❤ by <a href="https://github.com">GitHub</a>
      </div>
    </div>
</div>
</div>
<br>
The next example whos a much more efficient implementation: the gcc way! It removes a number of the branches required in the last example, so right after executing the op code code it can go staright into the enxt opcode! Rather than the first example where it had to branch to the end then to the next for loop iteration etc. So it is alot more efficient!<br>
<br>
<div class="gistLoad" data-id="2141678" id="gist-2141678"><br><link rel="stylesheet" href="https://assets-cdn.github.com/assets/gist-embed-08527ef2b62c06e4f818538458263d7d9e4bd82a210e7da0b973d9690adc8889.css"><div id="gist2141678" class="gist">
    <div class="gist-file">
      <div class="gist-data">
        <div class="js-gist-file-update-container js-task-list-container file-box">
  <div id="file-interpreters101_thegccway-cpp" class="file">


  <div itemprop="text" class="blob-wrapper data type-c">
      <table class="highlight tab-size js-file-line-container" data-tab-size="8">
      <tbody><tr>
        <td id="file-interpreters101_thegccway-cpp-L1" class="blob-num js-line-number" data-line-number="1"></td>
        <td id="file-interpreters101_thegccway-cpp-LC1" class="blob-code blob-code-inner js-file-line"><span class="pl-c"><span class="pl-c">/*</span></span></td>
      </tr>
      <tr>
        <td id="file-interpreters101_thegccway-cpp-L2" class="blob-num js-line-number" data-line-number="2"></td>
        <td id="file-interpreters101_thegccway-cpp-LC2" class="blob-code blob-code-inner js-file-line"><span class="pl-c">The gcc way</span></td>
      </tr>
      <tr>
        <td id="file-interpreters101_thegccway-cpp-L3" class="blob-num js-line-number" data-line-number="3"></td>
        <td id="file-interpreters101_thegccway-cpp-LC3" class="blob-code blob-code-inner js-file-line"><span class="pl-c"><span class="pl-c">*/</span></span></td>
      </tr>
      <tr>
        <td id="file-interpreters101_thegccway-cpp-L4" class="blob-num js-line-number" data-line-number="4"></td>
        <td id="file-interpreters101_thegccway-cpp-LC4" class="blob-code blob-code-inner js-file-line">#<span class="pl-k">define</span> <span class="pl-en">DISPATCH</span>() \</td>
      </tr>
      <tr>
        <td id="file-interpreters101_thegccway-cpp-L5" class="blob-num js-line-number" data-line-number="5"></td>
        <td id="file-interpreters101_thegccway-cpp-LC5" class="blob-code blob-code-inner js-file-line">   { <span class="pl-k">goto</span> *op_table[*((stringOfBytecode)++) - <span class="pl-s"><span class="pl-pds">'</span>a<span class="pl-pds">'</span></span>]; }</td>
      </tr>
      <tr>
        <td id="file-interpreters101_thegccway-cpp-L6" class="blob-num js-line-number" data-line-number="6"></td>
        <td id="file-interpreters101_thegccway-cpp-LC6" class="blob-code blob-code-inner js-file-line">
</td>
      </tr>
      <tr>
        <td id="file-interpreters101_thegccway-cpp-L7" class="blob-num js-line-number" data-line-number="7"></td>
        <td id="file-interpreters101_thegccway-cpp-LC7" class="blob-code blob-code-inner js-file-line"><span class="pl-k">static</span> <span class="pl-k">void</span> <span class="pl-en">interpreter_the_gcc_way</span>(<span class="pl-k">const</span> <span class="pl-k">char</span>* stringOfBytecode) {</td>
      </tr>
      <tr>
        <td id="file-interpreters101_thegccway-cpp-L8" class="blob-num js-line-number" data-line-number="8"></td>
        <td id="file-interpreters101_thegccway-cpp-LC8" class="blob-code blob-code-inner js-file-line">	<span class="pl-k">static</span> <span class="pl-k">void</span>* op_table[] = {</td>
      </tr>
      <tr>
        <td id="file-interpreters101_thegccway-cpp-L9" class="blob-num js-line-number" data-line-number="9"></td>
        <td id="file-interpreters101_thegccway-cpp-LC9" class="blob-code blob-code-inner js-file-line">		&amp;&amp;op_a, &amp;&amp;op_b, &amp;&amp;op_c, &amp;&amp;op_d, &amp;&amp;op_e</td>
      </tr>
      <tr>
        <td id="file-interpreters101_thegccway-cpp-L10" class="blob-num js-line-number" data-line-number="10"></td>
        <td id="file-interpreters101_thegccway-cpp-LC10" class="blob-code blob-code-inner js-file-line">	};</td>
      </tr>
      <tr>
        <td id="file-interpreters101_thegccway-cpp-L11" class="blob-num js-line-number" data-line-number="11"></td>
        <td id="file-interpreters101_thegccway-cpp-LC11" class="blob-code blob-code-inner js-file-line">	<span class="pl-c1">DISPATCH</span>();</td>
      </tr>
      <tr>
        <td id="file-interpreters101_thegccway-cpp-L12" class="blob-num js-line-number" data-line-number="12"></td>
        <td id="file-interpreters101_thegccway-cpp-LC12" class="blob-code blob-code-inner js-file-line">	op_a: <span class="pl-c1">printf</span>(<span class="pl-s"><span class="pl-pds">"</span>Hell<span class="pl-pds">"</span></span>); <span class="pl-c1">DISPATCH</span>();</td>
      </tr>
      <tr>
        <td id="file-interpreters101_thegccway-cpp-L13" class="blob-num js-line-number" data-line-number="13"></td>
        <td id="file-interpreters101_thegccway-cpp-LC13" class="blob-code blob-code-inner js-file-line">	op_b: <span class="pl-c1">printf</span>(<span class="pl-s"><span class="pl-pds">"</span>o<span class="pl-pds">"</span></span>); <span class="pl-c1">DISPATCH</span>();</td>
      </tr>
      <tr>
        <td id="file-interpreters101_thegccway-cpp-L14" class="blob-num js-line-number" data-line-number="14"></td>
        <td id="file-interpreters101_thegccway-cpp-LC14" class="blob-code blob-code-inner js-file-line">	op_c: <span class="pl-c1">printf</span>(<span class="pl-s"><span class="pl-pds">"</span> w<span class="pl-pds">"</span></span>); <span class="pl-c1">DISPATCH</span>();</td>
      </tr>
      <tr>
        <td id="file-interpreters101_thegccway-cpp-L15" class="blob-num js-line-number" data-line-number="15"></td>
        <td id="file-interpreters101_thegccway-cpp-LC15" class="blob-code blob-code-inner js-file-line">	op_d: <span class="pl-c1">printf</span>(<span class="pl-s"><span class="pl-pds">"</span>rld!<span class="pl-cce">\n</span><span class="pl-pds">"</span></span>); <span class="pl-c1">DISPATCH</span>();</td>
      </tr>
      <tr>
        <td id="file-interpreters101_thegccway-cpp-L16" class="blob-num js-line-number" data-line-number="16"></td>
        <td id="file-interpreters101_thegccway-cpp-LC16" class="blob-code blob-code-inner js-file-line">	op_e: <span class="pl-k">return</span>;</td>
      </tr>
      <tr>
        <td id="file-interpreters101_thegccway-cpp-L17" class="blob-num js-line-number" data-line-number="17"></td>
        <td id="file-interpreters101_thegccway-cpp-LC17" class="blob-code blob-code-inner js-file-line">}</td>
      </tr>
</tbody></table>

  </div>

  </div>

</div>

      </div>
      <div class="gist-meta">
        <a href="https://gist.github.com/amorri40/2141678/raw/d66065109ef4196520904a5084d2da9f8a12975e/Interpreters101_Thegccway.cpp" style="float:right">view raw</a>
        <a href="https://gist.github.com/amorri40/2141678#file-interpreters101_thegccway-cpp">Interpreters101_Thegccway.cpp</a>
        hosted with ❤ by <a href="https://github.com">GitHub</a>
      </div>
    </div>
</div>
</div>
<br>
There is also an assembly example which is even more efficient, since there are still come cases where humans can write more efficient assembly than compilers.<br>
<script src="https://raw.github.com/moski/gist-Blogger/master/public/gistLoader.js" type="text/javascript" gapi_processed="true">
</script></div>