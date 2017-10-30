<article class="markdown-body entry-content" itemprop="text"><p><strong>【本工具已经集成至前后端一体化MVC框架 <a href="https://github.com/myworld4059/Codekart">Codekart</a>，欢迎使用！】</strong></p>
<p><strong>【框架地址：<a href="https://github.com/myworld4059/Codekart/">https://github.com/myworld4059/Codekart/</a> 】</strong></p>
<h1><a href="#stepjs" aria-hidden="true" class="anchor" id="user-content-stepjs"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Step.js</h1>
<p>Node.js 控制流程工具，解决回调嵌套层次过多等问题。适用于读文件、查询数据库等回调函数相互依赖，或者分别获取内容最后组合数据返回等应用情景。</p>
<h3><a href="#example-使用示例" aria-hidden="true" class="anchor" id="user-content-example-使用示例"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Example 使用示例</h3>
<p>回调函数顺序依赖、依次执行。适用于下一个回调函数依赖于上一个函数执行的结果。</p>
<p>使用方法：<code>Step.Step(func,[func,[func,[...]]]);</code>，函数参数为任意数量的回调函数。也可以是一个类、函数数组或者它们的组合。</p>
<p>当上一个回调执行完成返回 非 <code>undefined</code>的结果时，或者在回调内部中调用<code>this.step()</code>时，表示这个回调执行完成，
并把其结果作为下一个回调的第一个参数，把所有执行结果按次序组成的的数组作为下一个回调的第二个参数。</p>
<p>示例代码：</p>
<div class="highlight highlight-source-js"><pre><span class="pl-k">var</span> Step <span class="pl-k">=</span> <span class="pl-c1">require</span>(<span class="pl-s"><span class="pl-pds">'</span>Step.js<span class="pl-pds">'</span></span>);

<span class="pl-smi">Step</span>.<span class="pl-en">Step</span>(<span class="pl-k">function</span>(<span class="pl-smi">result</span>,<span class="pl-smi">entire</span>){

  <span class="pl-en">console</span>.<span class="pl-c1">log</span>(result); <span class="pl-c"><span class="pl-c">//</span> undefined</span>
  <span class="pl-en">console</span>.<span class="pl-c1">log</span>(entire); <span class="pl-c"><span class="pl-c">//</span> []</span>
  <span class="pl-k">var</span> that <span class="pl-k">=</span><span class="pl-c1">this</span>;
  <span class="pl-c1">setTimeout</span>(<span class="pl-k">function</span>(){
    <span class="pl-smi">that</span>.<span class="pl-en">step</span>(<span class="pl-s"><span class="pl-pds">'</span>abc<span class="pl-pds">'</span></span>);
  },<span class="pl-c1">1000</span>);
  
},<span class="pl-k">function</span>(<span class="pl-smi">result</span>,<span class="pl-smi">entire</span>){

  <span class="pl-en">console</span>.<span class="pl-c1">log</span>(result); <span class="pl-c"><span class="pl-c">//</span> 'abc' </span>
  <span class="pl-en">console</span>.<span class="pl-c1">log</span>(entire); <span class="pl-c"><span class="pl-c">//</span> ['abc']  </span>
  <span class="pl-k">return</span> <span class="pl-c1">123</span>; <span class="pl-c"><span class="pl-c">//</span>return ::返回一个非undefined的值，和调用this.step();效果相同</span>
  <span class="pl-c"><span class="pl-c">/*</span>注意：如果未返回数据，或者未调用this.step()，将会中断回调的执行，后面的回调都不会执行！！！<span class="pl-c">*/</span></span>
  
},<span class="pl-k">function</span>(<span class="pl-smi">result</span>,<span class="pl-smi">entire</span>){
 
  <span class="pl-en">console</span>.<span class="pl-c1">log</span>(result); <span class="pl-c"><span class="pl-c">//</span> 'abc'  ::此值为上一个回调执行的结果</span>
  <span class="pl-en">console</span>.<span class="pl-c1">log</span>(entire); <span class="pl-c"><span class="pl-c">//</span> ['abc', 123]  ::此值为历史所有回调执行结果按次序组成的数组</span>
  <span class="pl-k">var</span> that<span class="pl-k">=</span><span class="pl-c1">this</span>;
  <span class="pl-c1">setTimeout</span>(<span class="pl-k">function</span>(){
    <span class="pl-smi">that</span>.<span class="pl-en">step</span>({abc<span class="pl-k">:</span><span class="pl-c1">123</span>});
    <span class="pl-en">console</span>.<span class="pl-c1">log</span>(<span class="pl-smi">that</span>.<span class="pl-c1">index</span>); <span class="pl-c"><span class="pl-c">//</span>that.index为一个整数，代表回调被调用的次序，而不是返回结果的次序。</span>
  },<span class="pl-c1">200</span>);
  
},<span class="pl-k">function</span>(<span class="pl-smi">result</span>,<span class="pl-smi">entire</span>){

  <span class="pl-en">console</span>.<span class="pl-c1">log</span>(result); <span class="pl-c"><span class="pl-c">//</span> {abc:123}</span>
  <span class="pl-en">console</span>.<span class="pl-c1">log</span>(entire); <span class="pl-c"><span class="pl-c">//</span> [ 'abc', 123, { abc: 123 } ]</span>
  
});</pre></div>
<p>组装回调函数的结果，此方法不同于上面的依赖串联执行，所有的回调是并行执行的，
只不过是在最后一个回调返回结果时，才调用最终处理函数。</p>
<p>使用方法：<code>Step.Assem(func,[func,[func,[...]]]);</code>，函数参数为任意数量的回调函数。也可以是一个类、函数数组或者它们的组合。</p>
<p>此方法的参数数量必须大于等于 2 个，函数才能被有效执行。</p>
<p>此方法传入的最后一个参数函数，将被作为最终的结果处理程序而不是单个获取数据的步骤。</p>
<p>示例代码：</p>
<div class="highlight highlight-source-js"><pre><span class="pl-k">var</span> Step <span class="pl-k">=</span> <span class="pl-c1">require</span>(<span class="pl-s"><span class="pl-pds">'</span>Step.js<span class="pl-pds">'</span></span>);

<span class="pl-smi">Step</span>.<span class="pl-en">Assem</span>(<span class="pl-k">function</span>(<span class="pl-smi">step</span>,<span class="pl-smi">index</span>){

  <span class="pl-k">var</span> that <span class="pl-k">=</span><span class="pl-c1">this</span>;
  <span class="pl-c1">setTimeout</span>(<span class="pl-k">function</span>(){
    <span class="pl-smi">that</span>.<span class="pl-en">step</span>(<span class="pl-s"><span class="pl-pds">'</span>abc<span class="pl-pds">'</span></span>); <span class="pl-c"><span class="pl-c">//</span>表示数据获取完毕</span>
  },<span class="pl-c1">1000</span>);
  
},<span class="pl-k">function</span>(){
  <span class="pl-k">return</span> <span class="pl-c1">123</span>; <span class="pl-c"><span class="pl-c">//</span>return ::返回一个非undefined的值，和调用this.step();效果相同</span>
  <span class="pl-c"><span class="pl-c">/*</span>注意：如果未返回数据，或者未调用this.step()，将会导致最终的数据处理程序不被调用！！！<span class="pl-c">*/</span></span>
  
},<span class="pl-k">function</span>(){
 
  <span class="pl-k">var</span> that<span class="pl-k">=</span><span class="pl-c1">this</span>;
  <span class="pl-c1">setTimeout</span>(<span class="pl-k">function</span>(){
    <span class="pl-smi">that</span>.<span class="pl-en">step</span>({abc<span class="pl-k">:</span><span class="pl-c1">123</span>});
    <span class="pl-en">console</span>.<span class="pl-c1">log</span>(<span class="pl-smi">that</span>.<span class="pl-c1">index</span>); <span class="pl-c"><span class="pl-c">//</span>that.index为一个整数，代表回调被调用的次序，而不是返回结果的次序。</span>
  },<span class="pl-c1">200</span>);
  
},<span class="pl-k">function</span>(<span class="pl-smi">result</span>){

  <span class="pl-en">console</span>.<span class="pl-c1">log</span>(result); <span class="pl-c"><span class="pl-c">//</span> [ 'abc', 123, { abc: 123 } ]</span>
  
});</pre></div>
<h3><a href="#api--doc" aria-hidden="true" class="anchor" id="user-content-api--doc"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>API &amp; DOC</h3>
<h4><a href="#stepfuncfuncfunc" aria-hidden="true" class="anchor" id="user-content-stepfuncfuncfunc"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Step(func,[func,[func,[...]]])</h4>
<p>步骤次序、回调依赖、依次执行处理。函数参数被依次执行</p>
<h4><a href="#assemfuncfuncfunc" aria-hidden="true" class="anchor" id="user-content-assemfuncfuncfunc"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Assem(func,func,[func,[...]])</h4>
<p>组装所有回调产生的结果，并把所有结果按调用次序组成数组，作为参数传给最后一个函数处理。</p>
<h4><a href="#作为参数的回调函数内部-this-" aria-hidden="true" class="anchor" id="user-content-作为参数的回调函数内部-this-"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>作为参数的回调函数内部 this ：</h4>
<h4><a href="#thisindex" aria-hidden="true" class="anchor" id="user-content-thisindex"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>this.index</h4>
<p>一个大于等于0的整数，表示这个函数被调用的次序，而不是返回结果的次序。</p>
<h4><a href="#thisstep" aria-hidden="true" class="anchor" id="user-content-thisstep"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>this.step()</h4>
<p>表示一个步骤执行完成，可以把获取的数据作为参数传递给它。</p>
<h4><a href="#thisstop" aria-hidden="true" class="anchor" id="user-content-thisstop"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>this.stop()</h4>
<p>终止所有步骤的执行。</p>
<h4><a href="#thisenddata" aria-hidden="true" class="anchor" id="user-content-thisenddata"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>this.end(data)</h4>
<p>跳到最后一步执行，data作为最后一个函数的第一个参数传入。</p>
<h2><a href="#许可证mit" aria-hidden="true" class="anchor" id="user-content-许可证mit"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>许可证（MIT）</h2>
<p>版权所有（c）2013 杨捷<a href="http://jojoin.com/user/1/">http://jojoin.com/user/1/</a></p>
<p>你可以随意使用并修改此模块的内容，但不能替换或修改作者的名称及主页。</p>
</article>
