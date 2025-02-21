---
layout: post
title:  "Git上的三種工作流程"
author: bowen
categories: [ Software Development ]
image: assets/images/software_developmenrt/multiple_flow_on_git/gitflow_1.jpg
---

此篇介紹Git的三種工作流程，建議對Git有簡單了解再閱讀此篇。若要找git 指令，請另尋別篇。

註：此篇是參考很多大大的教學，筆者釐清完後，再加入一些筆者觀點所產生的文章，若要參考來源，文章最後面有連結。

文章段落：

* Git flow
* Github Flow
* Gitlab flow
* Gitlab vs Github
* Git flow vs Github flow vs Gitlab flow

## 工作流程

開發團隊雖然有了Git的版本控制，還是會遇到問題，branch太多，開發團隊的每個人對於分支的認知不同，故有了好幾個flow種類

* GitFlow
* Github flow
* GitLab flow

注意，Github flow和Git flow是完全不同的流程。

---

### GitFlow

緣由：一個開發團隊可能有好幾個branch，但每個人對於分支的認知不同，造成每次commit到不同分支，大家也不知道合併要回到誰，若是都合併到master，一定會出大問題，故有了GitFlow去規範使用者。

目的：主要是規範一個工作流程，使開發團隊遵守branch的commit規則，讓最後合併時不容易出問題，並且簡化整個流程圖，讓開發團隊不必自己研發一個新的流程。

流程圖：

![gitflow_1]({{ site.baseurl }}/assets/images/software_developmenrt/multiple_flow_on_git/gitflow_1.jpg)
[https://gitbook.tw/chapters/gitflow/why-need-git-flow.html](https://gitbook.tw/chapters/gitflow/why-need-git-flow.html)

#### Master
主要呈現給客戶的產品版本，確保每個版本都要可以執行，這個分支的來源只能從別的分支合併過來，開發者不會直接commit到這個分支，因為是穩定版，通常會在這分支上有版本編號。

#### Develop
這個分支 是所有開發的基礎分支，當要新增功能時，會新增feature分支，開發完後再合併回Develop。

#### Hotfix
當master有Bug時，會緊急產生hotfix的分支修復，修完後再合併回master，也同時會合併到develop分支，為何要合併到Develop呢?因為不這樣做，當develop就會有此bug。

#### Release
當認為 Develop 分支夠成熟了，就可以把 Develop 分支合併到 Release分支，在這邊進行算是上線前的最後測試。測試完成後，Release 分支將會同時合併到 Master 以及 Develop這兩個分支上。Master 分支是上線版本，而合併回 Develop 分支的目的，是因為可能在 Release，分支上還會測到並修正一些問題，所以需要跟 Develop 分支同步，免得之後的版本又再度出現同樣的問題。

#### Feature
當要開始新增功能的時候，就是使用 Feature 分支的時候了。Feature 分支都是從 Develop 分支來的，完成之後會再併回 Develop 分支。

容易遭遇的問題：多個feature合併時容易遇到衝突，故features branch的功能最好切越小越好，並且縮短開發時程，降低衝突機率。

註：實際跑過Gitflow，再看這篇，指出gitflow奇怪的地方
[https://blog.hellojcc.tw/the-flaw-of-git-flow/](https://blog.hellojcc.tw/the-flaw-of-git-flow/)

--- 

### GitHub flow
緣由：因為Git flow太過於複雜，故又推出了GitHub flow去簡化流程

示意圖
![github_flow]({{ site.baseurl }}/assets/images/software_developmenrt/multiple_flow_on_git/github_flow_1.jpg)
[https://medium.com/@lf2lf2111/三種版控流程-29c82f5d4469](https://medium.com/@lf2lf2111/三種版控流程-29c82f5d4469)

流程如下:

* 創建分支 (Create a branch) (fork也可以)
* 提交修改 (Add commits)
* 開啟 PR (Open a Pull Request)
* 代碼審核 (Discuss and review your code)
* 部屬 (Deploy)，先測試是否有bug，測試完畢後再進行下一步
* 合併 (Merge)

GitHub flow下只有兩種分支，第一個是master，其餘的都是branch，而branch命名應該要有敘述性（例如：userInfo、getAllUser），在branch準備merge時，需要發起pull request，再pull request上傳，管理者一定要測試完此brnach沒有問題，再與master合併。

簡單的說，由管理者來負責做分支的合併，其餘的開發者只需專心開發branch就好，但是開發者在commit時，務必要撰寫清楚，讓大家知道你在做甚麼，且管理者才知道如何合併，多一個人力去做合併的動作。

就好比大家一開始碰git時的方法，但多了一個人去專門負責合併工作，且master是隨時可以上線的情況。

很多Github 的開源專案都是採取Github flow形式
Commit:

就是一般的commit
pull request：

當開發者要合併branch到master時，需要發出pull request，此pull request有好幾個功能

1. 通知大家要合併回master
2. 若遇到問題，可以在pull request裡談，讓大家知道你的需求。
3. 請管理者來合併此branch
4. 留下合併的紀錄

(等同Gitlab flow的merge request）

## Master:

所有的master分支都是可以部署上線的

Q1:

你可能會想問為什麼要fork?怎麼不直接開個branch?

A1:

Github flow一開始是發源於開源專案，故開源專案的作者不會輕易給任何人，故想要協同開發的工程師，會先fork此開源專案的副本到工程師的電腦開發，開發完後再發出pull request給作者，作者看完後覺得ok，才會合併回主線。

--- 

### GitLab Flow

由來：想多改善Github flow的弱點，但依舊保持簡單的優勢

示意圖:

![gitlab_flow]({{ site.baseurl }}/assets/images/software_developmenrt/multiple_flow_on_git/gitlab_flow_1.jpg)

[https://medium.com/@lf2lf2111/三種版控流程-29c82f5d4469](https://medium.com/@lf2lf2111/三種版控流程-29c82f5d4469)

Gitlab Flow的最主要原則為上游優先(upstream first)，

只存在一個分支master，其他的branch都是下游，當下游出問題時，需要先開個分支，修完bug後合併回Master，再從master往出問題的下游合併，此做法是擔心開發者在下游修完bug，就忘了合併回master，造成後續的分支又遇到同樣的bug。

GitLab Flow分成兩種情形應付不同的開發流程

1. 持續發布
2. 版本發布

#### 持續發布

持續發布的專案，建議在多出一個分支，為預發分支pre-production。

每個環境(如開發環境,預發環境,測試環境…等)都會有對應的分支。如下圖，開發環境為master分支，預發環境為pre-production分支,生產環境為production
![gitlab_flow_2]({{ site.baseurl }}/assets/images/software_developmenrt/multiple_flow_on_git/gitlab_flow_2.jpg)

[https://medium.com/@lf2lf2111/三種版控流程-29c82f5d4469](https://medium.com/@lf2lf2111/三種版控流程-29c82f5d4469)

由上圖來舉例，如果生產環境(production)發生錯誤，則要建一個新分支修改完後合併到最上游的開發分支(master)(此時就是Upstream first)，且經過測試，再繼續往pre-production branch，要經過測試沒問題後才能夠在往下合併到生產環境。

#### 版本發布

在 GitLab Flow中，對於版本發布的項目，建議每一個穩定的版本都要從master分支拉出來創建一個新分支，比如下圖的2–3-stable、2–4-stable(release分支)。

根據對應的release branch在創建一個修復分支，修補bug後，一樣要照著上游優先規則，先合併到master分支，確認沒問題過後，才能夠合併到release分支，並且要更新版本號。

![gitlab_flow_3]({{ site.baseurl }}/assets/images/software_developmenrt/multiple_flow_on_git/gitlab_flow_3.jpg)

[https://medium.com/@lf2lf2111/三種版控流程-29c82f5d4469](https://medium.com/@lf2lf2111/三種版控流程-29c82f5d4469)

#### Production branch：

用來幫助團隊明確知道目前正式上線的程式碼是哪一個版本。因此團隊可以按著開發步調持續地推進開發工作，開發進度依然按照 Github Flow 的做法，由 feature branch 合併至 master branch。當程式要正式上線時，才根據要交付的範圍，從 master branch 合併至 production branch，同時在 production branch 即可搭配 GitLab CI 功能觸發CI Job — production deploy。

#### Environment branch：

GitLab Flow 建議你除了多增加 production branch 對應正式環境之外，你也可以根據不同的部署環境額外建立對應的branch。例如也許你的正式環境是一個龐大的分散式架構，因此在部署到正式環境之前，為了避免出現預期之外的問題，還需要先在和正式環境類似但規模較小的 pre-production 環境進行測試與驗證；在此情境下，你不妨就增加一個 pre-production branch 對應pre-production 環境。同理，也許今天某公司可能需要定期展示最新功能給投資人觀看，需要一個環境會定期部署最新版本的程式，GitLab Flow 建議即可增加一個 vc branch 來管理它。

#### Release branch：

如果你的程式並非是直接部署於某個環境，而是直接對外發佈（release），那麼 GitLab Flow 的作法是不一定要建立 production branch，而是改為根據每次的 release 建立對應的 release branch。

這麽做的目的在於讓 master branch 能夠持續地穩健前進，而 release 出去的分支既能保持當下版本在功能上是獨立stable 的狀態，又能適度的跟隨 master 修補程式漏洞。

根據上面的內容，我們可以了解到 GitLab Flow 保留了 feature branch 與 master branch，使得開發團隊能專注於開發工作。同時額外新增的 production、environment 及 release branch，再搭配 GitLab 的 CI、merge request、issue tracking、Environment等功能，將能幫助開發工作和交付部署工作之間能做出適度的切分，避免相互影響。

實際例子
![reality_case]({{ site.baseurl }}/assets/images/software_developmenrt/multiple_flow_on_git/reality_case_1.jpg)
[https://www.slideshare.net/viniciusban/gitlab-flow?next_slideshow=1](
https://www.slideshare.net/viniciusban/gitlab-flow?next_slideshow=1)

上游優先，開發完後一律回master，master穩定時發一個stable branch，當stable branch遇到bug，緊急開一個hotfix分支，把bug修完後，同時回到stable和master，

#### Merge Request

工程師開發完成後，如果要把電腦上最新版本的程式碼上傳回 專案的主要 Repo，就必須對 專案的主要 Repo 發送一個 合併請求，請 專案的主要 Repo 管理員進行程式合併。

當合併請求發送出去後，專案的主要 Repo 管理員可以在管理頁面上看見你的合併請求，這時管理員會進行一次 Code Review，管理員覺得程式沒問題，就會將工程師的程式合併回主線。

(等同Github flow的pull request)

--- 

### Gitlab的產品生態系

idea→issue→plan→code→commit→test→review→staging→production→feedback

其中plan→feedback都跟工程師比較息息相關

程式碼寫完，要進行test(CI/CD) ，再進行code review，順利merge完後會自動部署到staging或production like的環境，再次驗證是否順利，最後再丟到production的環境。


--- 

## Gitlab vs Github

兩個都是建立在Git的系統，一樣都有網頁版，是兩個完全不同的公司在維護

差別:

1. privacy repositories

Github的privacy repositories要付費，而Gitlab則是提供無限量的privacy repositories，

故在2019年時，Github也提供三人團隊以內的無限量privacy repositories，2020年Github才改成每個人都可以創建privacy repositories，不論團隊大小都可以，而repositories的大小是500MB，Gitlab的repositories的大小是10GB

2. CI/CD

Gitlab有內建CI/CD 可以跑，而Github後來才居上，導入jenkins和circleCI

一開始Gitlab提供CI/CD的優勢，拉到很多使用者，但現今Github也把此差距拉平

--- 

## Git flow vs GitHub flow vs GitLab flow

三者的關係：Git flow先出現，因過於複雜，產生出GitHub flow，但過於簡單，GitLab flow再補充。

#### Git flow

Git flow的優點是分支狀態系統化、清晰可控，缺點是相對複雜，需要頻繁切換分支，而且不利於CI/CD。如果在版本快速迭代的專案中，是幾乎用不到Hotfix 和 Release 分支的，因為合併到master後如果有bug就直接修復且發布下個版本了，如果還使用這兩個分支，需要合併回develop 和master分支，但實際上開發者很常忘記合併回這兩個主分支。

#### GitHub flow

GitHub flow則適合項目是”持續發布”類型，比Git flow簡單，適合CD/CI，缺點由於master為最新代碼，但是準發布版本不一定是用最新代碼，或是有固定時間才發布更新的項目，就會有影響(例如:發布ios APP時會審核master時，但審核期間如果有新版本推上會造成審核延遲)。如果只有一個master主分支就會不夠用。所以還得另外再建一個新分支來維護。所以又發展出了Gitlab flow。

#### Gitlab flow

是 Git flow 與 Github flow 的綜合。結合了兩者的優點，有開發環境上的彈性又有單一主分支的方便。master的分支不夠，於是增加了一個 prodution 分支，專門用來發布版本。

這三種工作流程的都有一個共同點，都是”功能驅動式開發”（Feature-driven development）。以需求為開發的起點，先有需求才有以上那些分之，且開發完後該分枝就會被合併到主分支然後刪除。

此文參考資料：

1. [https://medium.com/@lf2lf2111/三種版控流程-29c82f5d4469](https://medium.com/@lf2lf2111/三種版控流程-29c82f5d4469)

2. [https://drprincess.github.io/2017/12/26/Git三大特色之WorkFlow(工作流)/](https://drprincess.github.io/2017/12/26/Git三大特色之WorkFlow(工作流)/)

3. [https://gitbook.tw/chapters/gitflow/why-need-git-flow.html](https://gitbook.tw/chapters/gitflow/why-need-git-flow.html)

4. [https://backlog.com/git-tutorial/tw/stepup/stepup3_2.html](https://backlog.com/git-tutorial/tw/stepup/stepup3_2.html)

5. [https://blog.hellojcc.tw/the-flaw-of-git-flow/](https://blog.hellojcc.tw/the-flaw-of-git-flow/)

6. [https://blog.darkthread.net/blog/git-branching-strategies/](https://blog.darkthread.net/blog/git-branching-strategies/)

7. [https://awdr74100.github.io/2020-05-11-git-githubflow/](https://awdr74100.github.io/2020-05-11-git-githubflow/)

8. [https://docs.gitlab.com/ee/topics/gitlab_flow.html](https://docs.gitlab.com/ee/topics/gitlab_flow.html)