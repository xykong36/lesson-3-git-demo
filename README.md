# 周五聚餐吃什么？

lesson-3-git-demo · Git 入门课的课堂跟练仓库

这周五，Alice、Bob、Carol 三个人要一起聚餐，可是吃什么还没定。三个人都往这个仓库里交东西，顺便亲手走一遍 Git：先写名片报口味，再互相留言认识一下，然后为吃什么吵一架（冲突），最后翻一翻流水账，看看这顿饭是怎么定下来的。

不用提前懂任何编程，照着下面一步一步敲就行。

## 目录

- [先搞懂两件事](#先搞懂两件事)
- [整节课只记五个字](#整节课只记五个字)
- [课前准备（上课前做完）](#课前准备上课前做完)
- [角色分配](#角色分配)
- [第 0 轮：找到你的本子](#第-0-轮找到你的本子)
- [第 1 轮：写名片报口味](#第-1-轮写名片报口味)
- [第 2 轮：给别人的名片留言](#第-2-轮给别人的名片留言)
- [第 3 轮：周五聚餐吃什么（冲突）](#第-3-轮周五聚餐吃什么冲突)
- [第 4 轮：翻流水账](#第-4-轮翻流水账)
- [常见翻车](#常见翻车)
- [最后一句](#最后一句)

## 先搞懂两件事

**Git 是你手里的本子，GitHub 上的仓库是大家共用的那一份聚餐计划。**

- Git 装在你自己电脑上，没网也能存档。每存一次（`commit`），本子上就多一条带签名、带时间的记录。
- GitHub 在网上，这个仓库就是三个人共用的那一份。大家把自己本子上的内容传上去（`push`），也从上面把别人新传的拿回来（`pull`）。

你电脑上一共有四个地方：

| 地方 | 是什么 | 怎么过去 |
|---|---|---|
| 草稿纸 | 你正在改的文件 | 直接改、保存 |
| 待交区 | 挑好这次要交的 | `git add .` |
| 我的本子 | 签名记下一笔 | `git commit -m "…"` |
| GitHub 上的仓库 | 大家共用的那一份，谁都看得到 | `git push` |

反过来，`git pull` 是把 GitHub 上别人新传的，拿回你的本子和草稿纸。

## 整节课只记五个字

**拉、改、加、存、推**

| 口诀 | 命令 | 意思 |
|---|---|---|
| 拉 | `git pull` | 把 GitHub 上的最新版拿回来 |
| 改 | 改文件，保存 | 在草稿纸上改 |
| 加 | `git add .` | 放进待交区 |
| 存 | `git commit -m "…"` | 签名记进本子 |
| 推 | `git push` | 传到 GitHub 上，大家都能看到 |

`git add .` 的那个点，意思是“当前文件夹里所有改过的”。今天全都用点就行。

## 课前准备（上课前做完）

这一步最容易出问题，一定要在上课前做完。卡住了就找老师。

### 1. 装 Git 和 VS Code

- Git：Mac 在终端里敲 `git --version`，没装会提示你安装；Windows 去 <https://git-scm.com> 下载安装。
- VS Code：<https://code.visualstudio.com>
- GitHub 命令行工具 gh：<https://cli.github.com>
- 注册一个 GitHub 账号，把用户名发给老师。

### 2. 接受老师的协作者邀请

这个仓库是公开的，**谁都能 clone（抄一份）下来，但只有协作者才能 push（传到 GitHub 上）**。就像聚餐群：谁都能看到大家定了吃什么，但只有进了群的人才能发言。

老师会用你的 GitHub 账号发邀请，去邮箱里点 **Accept**（或者打开 <https://github.com/xykong36/lesson-3-git-demo/invitations>）。不接受邀请，到第 1 轮 push 时会看到 `Permission denied` 或 403。

### 3. 告诉 Git 你是谁，顺手配好几个开关

打开终端，一行一行敲：

```bash
# 身份：用你自己的名字，git log 里会显示
git config --global user.name "Alice"          # 换成你的角色名或真名
git config --global user.email "你的邮箱"

# 避免 pull 时的“分叉”提示和弹出编辑器
git config --global pull.rebase false
git config --global core.editor "code --wait"
echo 'export GIT_MERGE_AUTOEDIT=no' >> ~/.zshrc   # Windows：setx GIT_MERGE_AUTOEDIT no
```

### 4. 登录 GitHub

```bash
gh auth login
```

跟着提示走，选 **HTTPS**，再选**用浏览器登录**，最省事。

### 5. 把仓库抄一份到你电脑上

```bash
cd ~ && git clone https://github.com/xykong36/lesson-3-git-demo.git
```

这会在你的家目录里多出一个 `lesson-3-git-demo` 文件夹，这就是你的本子。

### 6. 用 VS Code 打开它

VS Code 菜单 **文件 → 打开文件夹**，选家目录下的 `lesson-3-git-demo`。再用菜单 **终端 → 新建终端** 打开终端，敲一下 `git pull`，能跑通就准备好了。

## 角色分配

每人认一个角色，整节课都按自己的角色来。

| 角色 | 第 1 轮改 | 第 2 轮给谁留言 | 第 3 轮想吃 |
|---|---|---|---|
| Alice | 名片-Alice.md | Bob | 火锅 |
| Bob | 名片-Bob.md | Carol | 烤肉 |
| Carol | 名片-Carol.md | Alice | 日料 |

仓库里一共就这几个文件：三张名片（`名片-Alice.md`、`名片-Bob.md`、`名片-Carol.md`），加上一份 `周五聚餐.md`，里面写着“我们决定吃：待定”。

下面的例子都用 Alice 来写。你是 Bob 或 Carol，就把名字和食物换成你自己的。

## 第 0 轮：找到你的本子

**老师说**：“打开终端，敲 `cd ~/lesson-3-git-demo`，再敲 `git status`。看到 working tree clean 的举手。”

```bash
cd ~/lesson-3-git-demo
git status
```

**你会看到**：

```
On branch main
Your branch is up to date with 'origin/main'.

nothing to commit, working tree clean
```

**这说明**：你的本子和 GitHub 上的仓库一模一样，草稿纸上也没有没交的东西。

如果看到 `No such file or directory` 或 `not a git repository`，多半是没进对文件夹，举手找老师。

## 第 1 轮：写名片报口味

约饭之前，先让大家知道你爱吃什么。这一轮走完一遍五字口诀，并且第一次被拒绝。

**1. 拉**

```bash
git pull
```

会看到 `Already up to date.`，意思是 GitHub 上没有你还没拿到的新东西。

**2. 改**

打开**你自己的**名片（Alice 打开 `名片-Alice.md`），把“我最爱吃”“最近在看”两行填上，**保存**（Mac 按 Cmd+S，Windows 按 Ctrl+S）。然后看一眼：

```bash
git status
```

文件名是**红色**的：你在草稿纸上改了，但还没放进待交区。

**3. 加**

```bash
git add .
git status
```

文件名变成**绿色**了：已经放进待交区。

**4. 存**

```bash
git commit -m "Alice 填好了名片"
```

现在你的本子里有了这一笔，但 GitHub 上还没有，别人还看不到你爱吃什么。

**5. 推：等老师喊“三、二、一”，三个人一起推！**

```bash
git push
```

只有一个人会成功。另外两个人会看到：

```
To https://github.com/xykong36/lesson-3-git-demo.git
 ! [rejected]        main -> main (fetch first)
error: failed to push some refs to 'https://github.com/xykong36/lesson-3-git-demo.git'
hint: Updates were rejected because the remote
hint: contains work that you do not have locally.
```

**这说明**：你没做错任何事。你本子上的内容是在旧版本上写的，GitHub 上的仓库已经被别人更新过了。Git 不让你直接盖上去，否则别人刚填好的名片就被你覆盖了。

**怎么办：先拉再推。**

```bash
git pull
git push
```

`git pull` 时会看到 `Merge made by the 'ort' strategy.`，说明 Git 已经把别人的名片和你的合在一起了。再 `git push` 就能传上去。第三个人可能又被拒一次，没关系，再拉一次、再推一次。

老师刷新 GitHub 页面，三张名片都在，三个人爱吃什么一目了然。

## 第 2 轮：给别人的名片留言

一起吃饭前，先互相认识一下。这一轮体验“别人的改动，经过 GitHub，到了我这里”。

**1. 拉**

```bash
git pull
```

**2. 改**：Alice 给 Bob、Bob 给 Carol、Carol 给 Alice。打开**对方的**名片，在“别人眼中的我”下面写一句第一印象，签上你的名字，保存。

**3. 加、存**

```bash
git add .
git commit -m "Alice 给 Bob 留言"
```

**4. 推**

```bash
git push
```

这次老师不喊一起推。被拒了？你已经知道怎么办了：先 `git pull`，再 `git push`。

**5. 都推上去了，再拉一次，打开你自己的名片**

```bash
git pull
```

**你会看到**：你自己一个字没改，但你的名片里多了别人写给你的话。

**这说明**：这就是协作。三个人同时在改，但改的是**不同的文件**，Git 自己就能合在一起，谁也不用等谁。

**6. 看一眼流水账**

```bash
git log --oneline
```

最上面是最新的，每一条都有签名。按 `q` 退出。

## 第 3 轮：周五聚餐吃什么（冲突）

终于要定吃什么了。这一轮要故意吵一架。

**1. 拉**

```bash
git pull
```

**2. 改**：打开 `周五聚餐.md`，把“待定”改成你想吃的（Alice 写火锅、Bob 写烤肉、Carol 写日料）。**不许和别人商量**。保存。

```
# 周五聚餐
我们决定吃：火锅
```

**3. 加、存**

```bash
git add .
git commit -m "Alice 想吃火锅"
```

**4. 推：老师喊“三、二、一，一起推！”**

```bash
git push
```

一人成功，两人被拒（`! [rejected]`，和第 1 轮一样）。

**5. 被拒的人：拉**

```bash
git pull
```

这次看到的不一样了：

```
Auto-merging 周五聚餐.md
CONFLICT (content): Merge conflict in 周五聚餐.md
Automatic merge failed; fix conflicts and then commit the result.
```

**这说明**：上一轮 Git 自己就合好了，这一轮为什么不行？因为你们改的是**同一个文件的同一行**。一边说火锅，一边说烤肉，Git 不知道听谁的。Git 不替你们点菜，它把两个版本都摆在你面前，让人来商量。

**6. 打开 `周五聚餐.md`，看懂三行符号**

```
# 周五聚餐
<<<<<<< HEAD
我们决定吃：火锅
=======
我们决定吃：烤肉
>>>>>>> 7e3b1c9
```

| 符号 | 意思 |
|---|---|
| `<<<<<<< HEAD` | 从这里开始，是**你自己的**版本 |
| `=======` | 分隔线：上面是你的，下面是 GitHub 上别人的 |
| `>>>>>>> 7e3b1c9` | 到这里结束，上面这段是**GitHub 上别人的**版本（后面那串字母数字每次都不一样，不用管） |

**7. 商量、删符号**

- **商量**：和对方真的商量一下，改成一行，比如 `我们决定吃：火锅配烤肉`。
- **删符号**：把 `<<<<<<<`、`=======`、`>>>>>>>` 这三行整行删掉，保存。

改完应该长这样：

```
# 周五聚餐
我们决定吃：火锅配烤肉
```

VS Code 里也可以点冲突上方的“保留双方更改”，再手动整理成一行。

**8. 再加、存、推**

```bash
git add .
git commit -m "商量好了：火锅配烤肉"
git push
```

**9. 第三个人**：再拉一次，你会再冲突一次（你的日料 vs 刚商量好的火锅配烤肉）。这次自己解决，另外两个人只看不帮。步骤一样：商量、删符号、加、存、推。

到这里，周五吃什么终于定下来了。

> 冲突不是错误，是 Git 在问你：你们商量好了吗？

## 第 4 轮：翻流水账

饭定好了，回头看看这顿饭是怎么一步步定下来的。

**1. 拉最新的，看分叉和汇合**

```bash
git pull
git log --oneline --graph
```

分叉的地方就是“两个人同时改”，汇合的地方就是“合并”。按 `q` 退出。

**2. 看你的名片被谁改过**

```bash
git log -p 名片-Alice.md
```

谁、什么时候、改了哪几个字，全都记着。按 `q` 退出。

**3. 看投影**：老师会在 VS Code 的 Git Graph 里展示，三个人的提交一目了然。

## 常见翻车

| 你看到的 | 原因 | 怎么办 |
|---|---|---|
| `nothing to commit` | 文件没保存 | Cmd+S / Ctrl+S 保存，再 `git add .`、`git commit` |
| 弹出 vim，一堆 `~` 的界面 | `GIT_MERGE_AUTOEDIT` 没生效 | 按 `Esc`，输入 `:wq` 回车；课后补配置 |
| `hint: You have divergent branches…` | 没配 `pull.rebase false` | `git config --global pull.rebase false`，再 `git pull` |
| `Permission denied` / 403 | 没接受协作者邀请，或没登录 | 先看同桌操作，课后处理（接受邀请、`gh auth login`） |
| `Author identity unknown` | 没告诉 Git 你是谁 | `git config --global user.name "Alice"`，再配 `user.email` |
| 忘删冲突符号就提交了 | 没关系 | 打开文件删掉，再加、存、推一次 |
| 解决冲突后 commit 时弹编辑器 | 没带说明 | 用 `git commit -m "..."` 带上说明就不会弹 |
| 冲突时慌了，想重来 | 没关系 | `git merge --abort` 回到冲突前，然后重新 `git pull` |

## 最后一句

GitHub 上仓库里的每一次修改都有签名、有时间，也都能找回来。以后用 AI 帮你改文件也一样：**让 AI 大胆改之前，先 commit。**
