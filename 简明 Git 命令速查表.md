<strong style="display:block;font-size:22px;margin:22px 0 10px">创建</strong>
<p>复制一个已创建的仓库:</p>
<pre class="prettyprint"><code>$ git clone ssh://user@domain.com/repo.git</code></pre>
<p>创建一个新的本地仓库:</p>
<pre class="prettyprint"><code>$ git init</code></pre>
<strong style="display:block;font-size:22px;margin:22px 0 10px">本地修改</strong>
<p>显示工作路径下已修改的文件：</p>
<pre class="prettyprint"><code>$ git status</code></pre>
<p>显示与上次提交版本文件的不同：</p>
<pre class="prettyprint"><code>$ git diff</code></pre>
<p>把当前所有修改添加到下次提交中：</p>
<pre class="prettyprint"><code>$ git add</code></pre>
<p>把对某个文件的修改添加到下次提交中：</p>
<pre class="prettyprint"><code>$ git add -p &lt;file&gt;</code></pre>
<p>提交本地的所有修改：</p>
<pre class="prettyprint"><code>$ git commit -a</code></pre>
<p>提交之前已标记的变化：</p>
<pre class="prettyprint"><code>$ git commit</code></pre>
<p>附加消息提交：</p>
<pre class="prettyprint"><code>$ git commit -m 'message here'</code></pre>
<p>提交，并将提交时间设置为之前的某个日期:</p>
<pre class="prettyprint"><code>git commit --date="`date --date='n day ago'`" -am "Commit Message"</code></pre>
<p>修改上次提交</p>
<p>请勿修改已发布的提交记录!</p>
<pre class="prettyprint"><code>$ git commit --amend</code></pre>
<p>把当前分支中未提交的修改移动到其他分支</p>
<pre class="prettyprint"><code>git stash
git checkout branch2
git stash pop</code></pre>
<strong style="display:block;font-size:22px;margin:22px 0 10px">搜索</strong>
<p>从当前目录的所有文件中查找文本内容：</p>
<pre class="prettyprint"><code>$ git grep "Hello"</code></pre>
<p>在某一版本中搜索文本：</p>
<pre class="prettyprint"><code>$ git grep "Hello" v2.5</code></pre>
<strong style="display:block;font-size:22px;margin:22px 0 10px">提交历史</strong>
<p>从最新提交开始，显示所有的提交记录（显示hash， 作者信息，提交的标题和时间）：</p>
<pre class="prettyprint"><code>$ git log</code></pre>
<p>显示所有提交（仅显示提交的hash和message）：</p>
<pre class="prettyprint"><code>$ git log --oneline</code></pre>
<p>显示某个用户的所有提交：</p>
<pre class="prettyprint"><code>$ git log --author="username"</code></pre>
<p>显示某个文件的所有修改：</p>
<pre class="prettyprint"><code>$ git log -p &lt;file&gt;</code></pre>
<p>谁，在什么时间，修改了文件的什么内容：</p>
<pre class="prettyprint"><code>$ git blame &lt;file&gt;</code></pre>
<strong style="display:block;font-size:22px;margin:22px 0 10px">分支与标签</strong>
<p>列出所有的分支：</p>
<pre class="prettyprint"><code>$ git branch</code></pre>
<p>切换分支：</p>
<pre class="prettyprint"><code>$ git checkout &lt;branch&gt;</code></pre>
<p>创建并切换到新分支:</p>
<pre class="prettyprint"><code>$ git checkout -b &lt;branch&gt;</code></pre>
<p>基于当前分支创建新分支：</p>
<pre class="prettyprint"><code>$ git branch &lt;new-branch&gt;</code></pre>
<p>基于远程分支创建新的可追溯的分支：</p>
<pre class="prettyprint"><code>$ git branch --track &lt;new-branch&gt; &lt;remote-branch&gt;</code></pre>
<p>删除本地分支:</p>
<pre class="prettyprint"><code>$ git branch -d &lt;branch&gt;</code></pre>
<p>给当前版本打标签：</p>
<pre class="prettyprint"><code>$ git tag &lt;tag-name&gt;</code></pre>
<strong style="display:block;font-size:22px;margin:22px 0 10px">更新与发布</strong>
<p>列出当前配置的远程端：</p>
<pre class="prettyprint"><code>$ git remote -v</code></pre>
<p>显示远程端的信息：</p>
<pre class="prettyprint"><code>$ git remote show &lt;remote&gt;</code></pre>
<p>添加新的远程端：</p>
<pre class="prettyprint"><code>$ git remote add &lt;remote&gt; &lt;url&gt;</code></pre>
<p>下载远程端版本，但不合并到HEAD中：</p>
<pre class="prettyprint"><code>$ git fetch &lt;remote&gt;</code></pre>
<p>下载远程端版本，并自动与HEAD版本合并：</p>
<pre class="prettyprint"><code>$ git remote pull &lt;remote&gt; &lt;url&gt;</code></pre>
<p>将远程端版本合并到本地版本中：</p>
<pre class="prettyprint"><code>$ git pull origin master</code></pre>
<p>将本地版本发布到远程端：</p>
<pre class="prettyprint"><code>$ git push remote &lt;remote&gt; &lt;branch&gt;</code></pre>
<p>删除远程端分支：</p>
<pre class="prettyprint"><code>$ git push &lt;remote&gt; :&lt;branch&gt; (since Git v1.5.0)
or
git push &lt;remote&gt; --delete &lt;branch&gt; (since Git v1.7.0)</code></pre>
<p>发布标签:</p>
<pre class="prettyprint"><code>$ git push --tags</code></pre>
<strong style="display:block;font-size:22px;margin:22px 0 10px">合并与重置</strong>
<p>将分支合并到当前HEAD中：</p>
<pre class="prettyprint"><code>$ git merge &lt;branch&gt;</code></pre>
<p>将当前HEAD版本重置到分支中:</p>
<p>请勿重置已发布的提交!</p>
<pre class="prettyprint"><code>$ git rebase &lt;branch&gt;</code></pre>
<p>退出重置:</p>
<pre class="prettyprint"><code>$ git rebase --abort</code></pre>
<p>解决冲突后继续重置：</p>
<pre class="prettyprint"><code>$ git rebase --continue</code></pre>
<p>使用配置好的merge tool 解决冲突：</p>
<pre class="prettyprint"><code>$ git mergetool</code></pre>
<p>在编辑器中手动解决冲突后，标记文件为已解决冲突</p>
<pre class="prettyprint"><code>$ git add &lt;resolved-file&gt;</code></pre>
<pre class="prettyprint"><code>$ git rm &lt;resolved-file&gt;</code></pre>
<strong style="display:block;font-size:22px;margin:22px 0 10px">撤销</strong>
<p>放弃工作目录下的所有修改：</p>
<pre class="prettyprint"><code>$ git reset --hard HEAD</code></pre>
<p>移除缓存区的所有文件（i.e. 撤销上次<code>git add</code>）:</p>
<pre class="prettyprint"><code>$ git reset HEAD</code></pre>
<p>放弃某个文件的所有本地修改：</p>
<pre class="prettyprint"><code>$ git checkout HEAD &lt;file&gt;</code></pre>
<p>重置一个提交（通过创建一个截然不同的新提交）</p>
<pre class="prettyprint"><code>$ git revert &lt;commit&gt;</code></pre>
<p>将HEAD重置到指定的版本，并抛弃该版本之后的所有修改：</p>
<pre class="prettyprint"><code>$ git reset --hard &lt;commit&gt;</code></pre>
<p>将HEAD重置到上一次提交的版本，并将之后的修改标记为未添加到缓存区的修改：</p>
<pre class="prettyprint"><code>$ git reset &lt;commit&gt;</code></pre>
<p>将HEAD重置到上一次提交的版本，并保留未提交的本地修改：</p>
<pre class="prettyprint"><code>$ git reset --keep &lt;commit&gt;</code></pre>