---
title: Git Strategy
layout: default
categories: git-strategy
permalink: /:categories/
---

## Git Strategy

我本人从毕业到现在也大大小小经历了不少的项目，那么基于CI、CD的git策略在不同的项目也有所有不同，后面就围绕git策略来发表一下我个人的看法。
首先，给出一张标准的git flow图，具体项目都会有所差别，大体上应该如此：  

![git-flow]({{ "/assets/git/7-steps.png" | absolute_url }})  

简单解释一下，master代码的每次提交都会触发CI/CD，团队能够看到CI/CD的健康情况；每次开发在coding之前都需要拉取最新代码，并merge到自己的分支，在写完代码之后，本地构建测试等通过之后，再一次拉取master最新代码，merge到本地分支，解决冲突，并再次拉取最新代码，之后分支代码merge回master代码，至此，确保CI/CD的健康。   
CI/CD健康的重要性不再赘述，后面我着重讲述一下我自己实际情况，我说的以下情况都是基于已经发布过的，后面需要持续发布的，因为第一次release之前所有代码都可以在master上开发，这无可置疑。  

## CASE 1:   

开发在分支上coding，这个分支是团队统一的该迭代所使用的分支名字，保证每个人在同一个分支上，都能获取最新的代码，及时拉取master的代码，因为master上面有可能是有hot fix；在即将release的前几天，团队被告知该分支应该被code freeeze，保证测试不被最新的代码影响。此时，有owner负责将分支merge回master，跑uat环境，准备release，与此同时，开发在新的分支上做下一个迭代的故事卡，以此类推。需要注意的是，release当天要在release的那个commit上打tag，以标记此次release的准确版本。   

## CASE 2:   
所
有开发在master上进行，在release前几天code freeze，开发在developer分支上，也是所有人在同一个分支，进行开发。这个时候会有一个问题，我们需要一个pipeline去跑developer分支的代码，否则，一堆的新代码都没有跑过，这不符合敏捷实践，也不能保证代码质量。同时，也是实时将master代码merge到developer分支，在解除code freeze之后便可以将分支代码merge回master，继续新一轮的release。这个项目release没有打tag。使用了togggle。  

可以看到，两个项目最明显的区别是一个在分支上开发，而另一个是在master上开发。CASE 2在master开发的原因是，客户需要每做完一个story，就去做validation，所以需要保证uat的feature在测试后是最新的，那么这个时候在分支上开发是没有意义的。而CASE 1是在一段时间之后uat的新feature才会被客户测试到，那么这个时候分支策略是比较理想的，因为这个项目是一个月一次release，时间间隔比较久，如果长时间在master开发，而一值没有release，有可能会导致不同release的代码会在同一时间上线，增加测试成本，以及后面新feature上线的风险。   

总的来看，那种策略都各有优势，最重要的是，每一个开发成员都需要尽自己最大的努力去写最高质量的代码，最大程度地减少风险。