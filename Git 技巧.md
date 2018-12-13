
<strong style="display:block;font-size:22px;margin:22px 0 10px">创建和使用git ssh key</strong>
<p>首先设置git的user name和email：</p>
<pre class="prettyprint"><code>git config --global user.name "xxx"
git config --global user.email "xxx@gmail.com"</code></pre>
<p>查看git配置：</p>
<pre class="prettyprint"><code>git config --list</code></pre>
<p><strong>然后生成SHH密匙：</strong></p>
<p>查看是否已经有了ssh密钥：<code>cd ~/.ssh</code><br />
如果没有密钥则不会有此文件夹，有则备份删除<br />
生存密钥：</p>
<pre class="prettyprint"><code>ssh-keygen -t rsa -C "xxx@gmail.com"</code></pre>
<p>按3个回车，密码为空这里一般不使用密钥。<br />
最后得到了两个文件：<code>id_rsa</code>和<code>id_rsa.pub</code><br />
<strong>注意：</strong>密匙生成就不要改了，如果已经生成到<code>~/.ssh</code>文件夹下去找。</p>
<strong style="display:block;font-size:22px;margin:22px 0 10px">git变更项目地址</strong>
<pre class="prettyprint"><code>git remote set-url origin git@192.168.6.70:res_dev_group/test.git
git remote -v</code></pre>
<p>查看某个文件的修改历史</p>
<pre class="prettyprint"><code>git log --pretty=oneline 文件名 # 显示修改历史
git show 356f6def9d3fb7f3b9032ff5aa4b9110d4cca87e # 查看更改</code></pre>
<strong style="display:block;font-size:22px;margin:22px 0 10px">git push 时报错 warning: push.default is unset;</strong>
<p>'<code>matching</code>'参数是 Git 1.x 的默认行为，其意是如果你执行 git push 但没有指定分支，它将 push 所有你本地的分支到远程仓库中对应匹配的分支。而 Git 2.x 默认的是 simple，意味着执行 git push 没有指定分支时，只有当前分支会被 push 到你使用 git pull 获取的代码。</p>
<p>根据提示，修改git push的行为:</p>
<pre class="prettyprint"><code>git config --global push.default matching</code></pre>
<p>再次执行git push 得到解决。</p>
<strong style="display:block;font-size:22px;margin:22px 0 10px">git submodule的使用拉子项目代码</strong>
<p>开发过程中，经常会有一些通用的部分希望抽取出来做成一个公共库来提供给别的工程来使用，而公共代码库的版本管理是个麻烦的事情。今天无意中发现了git的<code>git submodule</code>命令，之前的问题迎刃而解了。</p>
<ul>
<li>添加</li>
</ul>
<p>为当前工程添加submodule，命令如下：</p>
<pre class="prettyprint"><code>git submodule add 仓库地址 路径</code></pre>
<p>其中，仓库地址是指子模块仓库地址，路径指将子模块放置在当前工程下的路径。<br />
<strong>注意：</strong>路径不能以 / 结尾（会造成修改不生效）、不能是现有工程已有的目录（不能順利 Clone）</p>
<p>命令执行完成，会在当前工程根路径下生成一个名为“.gitmodules”的文件，其中记录了子模块的信息。添加完成以后，再将子模块所在的文件夹添加到工程中即可。</p>
<ul>
<li>删除</li>
</ul>
<p>submodule的删除稍微麻烦点：首先，要在“<code>.gitmodules</code>”文件中删除相应配置信息。然后，执行<code>git rm –cached</code>命令将子模块所在的文件从git中删除。</p>
<ul>
<li>下载的工程带有submodule</li>
</ul>
<p>当使用<code>git clone</code>下来的工程中带有submodule时，初始的时候，submodule的内容并不会自动下载下来的，此时，只需执行如下命令：</p>
<pre class="prettyprint"><code>git submodule update --init --recursive</code></pre>
<p>即可将子模块内容下载下来后工程才不会缺少相应的文件。</p>
<strong style="display:block;font-size:22px;margin:22px 0 10px">git add文件取消</strong>
<p>在git的一般使用中，如果发现错误的将不想提交的文件add进入index之后，想回退取消，则可以使用命令：<code>git reset HEAD &lt;file&gt;...</code>，同时<code>git add</code>完毕之后，git也会做相应的提示。</p>
<blockquote>
<p><a href="http://blog.csdn.net/yaoming168/article/details/38777763" target="_blank">http://blog.csdn.net/yaoming168/article/details/38777763</a></p>
</blockquote>
<strong style="display:block;font-size:22px;margin:22px 0 10px">git删除文件</strong>
<ul>
<li>删除文件跟踪并且删除文件系统中的文件file1<code>git rm file1</code></li>
<li>提交刚才的删除动作，之后git不再管理该文件<code>git commit</code></li>
<li>删除文件跟踪但不删除文件系统中的文件<code>file1git rm --cached file1</code></li>
<li>提交刚才的删除动作，之后git不再管理该文件。但是文件系统中还是有file1。<code>git commit</code></li>
</ul>
<strong style="display:block;font-size:22px;margin:22px 0 10px">版本回退</strong>
<ul>
<li>版本回退用于线上系统出现问题后恢复旧版本的操作。</li>
<li>回退到的版本<code>git reset --hard 248cba8e77231601d1189e3576dc096c8986ae51</code></li>
<li>回退的是所有文件，如果后悔回退可以git pull就可以了。</li>
</ul>
<strong style="display:block;font-size:22px;margin:22px 0 10px">历史版本对比</strong>
<ul>
<li>查看日志<code>git log</code></li>
<li>查看某一历史版本的提交内容<code>git show 4ebd4bbc3ed321d01484a4ed206f18ce2ebde5ca</code>，这里能看到版本的详细修改代码。</li>
<li>对比不同版本<code>git diff c0f28a2ec490236caa13dec0e8ea826583b49b7a2e476412c34a63b213b735e5a6d90cd05b014c33</code></li>
</ul>
<blockquote>
<p><a href="http://blog.csdn.net/lxlzhn/article/details/9356473" target="_blank">http://blog.csdn.net/lxlzhn/article/details/9356473</a></p>
</blockquote>
<strong style="display:block;font-size:22px;margin:22px 0 10px">分支的意义与管理</strong>
<ul>
<li>创建分支可以避免提交代码后对主分支的影响，同时也使你有了相对独立的开发环境。分支具有很重要的意义。</li>
<li>创建并切换分支，提交代码后才能在其它机器拉分支代码<code>git checkout -b new_branch</code></li>
<li>查看当前分支<code>git branch</code></li>
<li>切换到master分支<code>git checkout master</code></li>
<li>合并分支到当前分支<code>git merge new_branch</code>，合并分支的操作是从<code>new_branch</code>合并到master分支，当前环境在master分支。</li>
<li>删除分支<code>git branch -d new_branch</code></li>
</ul>
<strong style="display:block;font-size:22px;margin:22px 0 10px">git冲突文件编辑</strong>
<p>冲突文件冲突的地方如下面这样</p>
<pre class="prettyprint"><code>a123
&lt;&lt;&lt;&lt;&lt;&lt;&lt; HEAD
b789
=======
b45678910
&gt;&gt;&gt;&gt;&gt;&gt;&gt; 6853e5ff961e684d3a6c02d4d06183b5ff330dcc
c</code></pre>
<p>冲突标记&lt;&lt;&lt;&lt;&lt;&lt;&lt; （7个&lt;）与=======之间的内容是我的修改，=======与&gt;&gt;&gt;&gt;&gt;&gt;&gt;之间的内容是别人的修改。<br />
此时，还没有任何其它垃圾文件产生，你需要把代码合并好后重新走一遍代码提交流程就好了。</p>
<strong style="display:block;font-size:22px;margin:22px 0 10px">不顺利的代码提交流程</strong>
<ul>
<li>在<code>git push</code>后出现错误可能是因为其他人提交了代码，而使你的本地代码库版本不是最新。</li>
<li>这时你需要先<code>git pull</code>代码后，检查是否有文件冲突。</li>
<li>没有文件冲突的话需要重新走一遍代码提交流程<code>add —&gt; commit —&gt; push</code>。</li>
<li>解决文件冲突在后面说。</li>
</ul>
<strong style="display:block;font-size:22px;margin:22px 0 10px">git顺利的提交代码流程</strong>
<ul>
<li>查看修改的文件<code>git status</code>；</li>
<li>为了谨慎检查一下代码<code>git diff</code>；</li>
<li>添加修改的文件<code>git add dirname1/filename1.py dirname2/filenam2.py</code>，新加的文件也是直接add就好了；</li>
<li>添加修改的日志<code>git commit -m "fixed:</code>修改了上传文件的逻辑&quot;；</li>
<li>提交代码<code>git push</code>，如果提交失败的可能原因是本地代码库版本不是最新。</li>
</ul>
<strong style="display:block;font-size:22px;margin:22px 0 10px">理解github的pull request</strong>
<p>有一个仓库，叫Repo A。你如果要往里贡献代码，首先要Fork这个Repo，于是在你的Github账号下有了一个Repo A2,。然后你在这个A2下工作，Commit，push等。然后你希望原始仓库Repo A合并你的工作，你可以在Github上发起一个Pull Request，意思是请求Repo A的所有者从你的A2合并分支。如果被审核通过并正式合并，这样你就为项目A做贡献了。</p>
<blockquote>
<p><a href="http://zhidao.baidu.com/question/1669154493305991627.html" target="_blank">http://zhidao.baidu.com/question/1669154493305991627.html</a></p>
</blockquote>
<strong style="display:block;font-size:22px;margin:22px 0 10px">一些错误处理</strong>
<p>&quot;pathspec 'branch' did not match any file(s) known to git.&quot;错误</p>
<pre class="prettyprint"><code>git checkout master
git pull
git checkout new_branch</code></pre>
<p>使用git提交比较大的文件的时候可能会出现这个错误</p>
<pre class="prettyprint"><code>error: RPC failed; result=22, HTTP code = 411
fatal: The remote end hung up unexpectedly
fatal: The remote end hung up unexpectedly
Everything up-to-date</code></pre>
<p>这样的话首先改一下git的传输字节限制</p>
<pre class="prettyprint"><code>git config http.postBuffer 524288000</code></pre>
<p>然后这时候在传输或许会出现另一个错误</p>
<pre class="prettyprint"><code>error: RPC failed; result=22, HTTP code = 413
fatal: The remote end hung up unexpectedly
fatal: The remote end hung up unexpectedly
Everything up-to-date</code></pre>
<p>这两个错误看上去相似，一个是411，一个是413</p>
<p>下面这个错误添加一下密钥就可以了</p>
<ul>
<li>首先<code>key-keygen</code> 生成密钥</li>
<li>然后把生成的密钥复制到git中自己的账号下的相应位置</li>
</ul>
<pre class="prettyprint"><code>git push ssh://192.168.64.250/eccp.git branch</code></pre>