# 周五聚餐吃什么？

lesson-3-git-demo · Git 入门课的课堂跟练仓库

每人认领一个角色（Alice / Bob / Carol），整节课都用这个角色名完成练习。你们组的任务是：**一起决定周五聚餐吃什么**。GitHub 上的这个仓库，就是**我们组的聚餐公告栏**：大家往上面贴名片、贴聚餐意见，最后定出一张聚餐公告。一路上会依次完成三件事：填写名片、互相留言、协商聚餐，最后回顾提交历史。

不用提前懂任何编程，**也不用自己动手跑命令**：你在 WorkBuddy 或 Codex 里用大白话告诉 AI 要做什么，AI 去执行 Git 命令，你看结果就行。

> **详细步骤看课上发的《lesson3 Git 实操指南》**。每一轮怎么做、每条命令是什么意思、会看到什么输出，都以指南为准。这份 README 只放打开仓库时需要知道的几件事。指南里说的「公告栏」，就是 GitHub 上的这个仓库，也就是我们组的聚餐公告栏。

## 仓库里有什么

公告栏上一共贴着这几样东西：

| 文件 | 用在哪一轮 | 内容 |
|---|---|---|
| `名片-Alice.md`、`名片-Bob.md`、`名片-Carol.md` | 第 1 轮写自己的名片，第 2 轮给别人的名片留言 | 我最爱吃、最近在看、别人眼中的我 |
| `周五聚餐.md` | 第 3 轮协商周五聚餐 | 我们决定吃：待定 |

## 角色分配

Alice / Bob / Carol 只是角色名，谁扮演都可以。指南里选好你的角色，命令和示例会自动换成你的。

| 角色 | 第 1 轮改 | 第 2 轮给谁留言 | 第 3 轮想吃 |
|---|---|---|---|
| Alice | 名片-Alice.md | Bob | 火锅 |
| Bob | 名片-Bob.md | Carol | 烤肉 |
| Carol | 名片-Carol.md | Alice | 日料 |

## 怎么让 AI 帮你做

整节课只记五个字：**拉、改、加、存、推**。「拉」是看看公告栏上别人贴了什么，「推」是把你的想法贴到聚餐公告栏上。

指南里每一步都给了「方式一：直接对 AI 说」，那句话可以直接复制，发给 WorkBuddy 或 Codex，AI 会替你执行对应的 Git 命令。选用方式一就行，**你不用自己跑命令**。

## 课前准备（指南里没有，上课前做完）

卡住了就找老师。

1. **注册 GitHub，接受协作者邀请。** 把 GitHub 用户名发给老师，老师发邀请后去邮箱点 **Accept**（或打开 <https://github.com/xykong36/lesson-3-git-demo/invitations>）。这个仓库谁都能 clone，但只有协作者才能 push；不接受邀请，第 1 轮推送时会看到 `Permission denied` 或 403。
2. **让 AI 检查 Git 和 gh。** 对 AI 说：「帮我看看电脑上装没装 Git 和 GitHub 的 gh 工具，没装就帮我装上。」
3. **登录 GitHub。** 对 AI 说：「帮我登录 GitHub。」AI 会执行 `gh auth login`，一般会弹出浏览器让你点确认。
4. **告诉 Git 你是谁，顺手配好两个开关。** 把下面这段发给 AI，让它帮你执行（用户名换成你的角色名或真名）：

   ```bash
   git config --global user.name "Alice"
   git config --global user.email "你的邮箱"
   git config --global pull.rebase false
   echo 'export GIT_MERGE_AUTOEDIT=no' >> ~/.zshrc   # Windows：setx GIT_MERGE_AUTOEDIT no
   ```

课上第 0 轮会让 AI 把仓库克隆到本地。之后在 WorkBuddy 或 Codex 里打开 `lesson-3-git-demo` 文件夹，每一步都在这个文件夹里跟 AI 说。

## 常见翻车

`rejected` 和 `CONFLICT` 怎么处理，指南里每一轮都写了。下面是指南里没有的情况：

| 你看到的 | 原因 | 对 AI 说 |
|---|---|---|
| `nothing to commit` | 文件没保存 | 「帮我确认文件已经保存了，再放进待交区，然后提交。」 |
| AI 卡住不动，或者提示在等编辑器 | 提交时没带说明 | 「刚才的命令在等编辑器，帮我退出，然后用 `git commit -m` 带上说明重新提交。」 |
| `hint: You have divergent branches…` | 没配 `pull.rebase false` | 「帮我执行 `git config --global pull.rebase false`，再拉一次。」 |
| `Permission denied` / 403 | 没接受协作者邀请，或没登录 | 先看同桌操作，课后接受邀请，再对 AI 说「帮我登录 GitHub」。 |
| `Author identity unknown` | 没告诉 Git 你是谁 | 「帮我把 Git 的用户名设成 Alice，邮箱设成……」（换成你的角色名） |
| 忘删冲突标记就提交了 | 没关系 | 「帮我把 `周五聚餐.md` 里剩下的冲突标记删掉，再加、存、推一次。」 |
| 冲突时慌了，想重来 | 没关系 | 「帮我执行 `git merge --abort` 回到冲突前，然后重新拉一次。」 |

## 最后一句

每一次提交都记录了作者和时间，都能追溯和恢复。以后用 AI 帮你改文件也一样：**让 AI 大胆改之前，先 commit。**
