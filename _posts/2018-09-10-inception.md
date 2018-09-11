---
title: Inception是如何run的
layout: default
categories: inception
permalink: /:categories/
---

## Inception是如何run的  

我们7月份刚刚做过一次inception，对我的影响非常大，也确实学到不少的东西，这里分享出来。  

### What & Why

> *Inception是由Luke Barrett(管理TW欧洲，2014在车祸中丧生) and Marc(“《Agile Experience Design》”)在2004年左右初始提出的
Jonathan Rasmusson (author of The Agile Samurai) and Jeff Patton (author of User Story Mapping) both worked at ThoughtWorks
2011正式整理完成，改名Inception.*  

因为inception的周期一般是几个星期，但是Martinfowler为了快速看到他刚出生的宝宝，即创建了lean inception。  

变化让交付变得困难（客户改了又改），所以需要拥抱变化，快速验证，消除假设，达成一致
帮助我们启动200+的项目。

在项目之初  

来自客户的困户：  
    1.我有一个想法，想跟老板申请预算做这个项目，我得拿个东西show给他  
    2.我知道自己要啥，要做这样一个东西，但交给你们会做成什么样，我心里没谱  
    3.我不知道需要花多少钱，拿到什么样的东西，也不知道什么时候会拿到  

交付团队：  
    1.这个项目背景是啥？，这些业务需求是如何确定下来的？  
    2.业务需求的优先级是什么？ 他们负责人最关注的是什么？  
    3.客户环境下，技术上风险在哪儿？ 客户还需要跟哪些系统集成？  

对于长期的项目可能需要每三个月做一次inception，来验证各方对需求的理解是正确的。  

涉及到一个非常重要的概念，MVP(Minimum Viable Product):  
> *a simple version of a product that is given to users in order to validate the key business assumptions.*  

![inception-mvp]({{ "/assets/inception/mvp.png" | absolute_url }})  

### 参与的人员  

开发（developers）, 产品经理/项目经理（product managers）, 设计师（designers）, 需求分析是（business analysts）, 客户的stakeholder）,要使用该产品的用户（user），等等。不同的项目可能参加的人是不一样的。

### 准备Agenda  

在正式开始之前，必然要做些准备，比如agenda，即每天每个时间段要做哪些excersise，做哪些workshop，由哪些人来facilitate等等，agenda由PM起草，内部沟通讨论，呈现给客户，然后再根据客户的建议做一些修改，最终定稿。这个过程我印象中持续了三周，因为我们整个team加上客户有时差的关系，沟通成本非常大。实际上这个时候考虑的东西也很多，比如supplies，participants以及技术相关的等等。  

### 从始至终都应该关注的  

- **Glossary & Vocabulary**。专业的词汇，不论是业务上的词汇还是集成系统的词汇，都应该从始至终都有所记录，并且应该每天都要有owner去整理。  

- **Parking Lot**。在整个inception的讨论或是workshop过程当中，难免会碰撞出有价值的idea，但是没有必要在MVP就做的，我们就需要随时讲这些内容放在parking lot里面，方便今后跟踪。  

- **RAID**。Risks, Assumptions, Issues, Decisions。在开发这个产品时，有哪些风险，比如时差可能进度变慢，比如集成的系统环境没办法及时ready；有哪些需求的实现需要假设，比如使用了该产品可以替换掉某些应用；有哪些问题还没有解决的，需要哪些人来协助解决的；过程中做了哪些决定，比如该产品只在某个地方使用，只给6个人使用等。  

### dev应该关注哪些  

整个inception时间两周，team做了非常多的事情，我不可能把每一个细节都展现出来。我更在乎dev需要关注哪些，以及在下一次inception里面如何做的更好一些。 

- **提问**。首先，开发肯定是几乎全程都参加的，除了几个meeting需要技术和业务的分开来进行。不论是客户在介绍还是UX在介绍的时候，多注意思考，考虑周到一些，提出一些有意义的问题，帮助理清上下文，这个是非常重要的。  

- **果断并自信**。在inception结束的前两天会让开发进行粗略估点，这个估点当然也要考虑全面，关键是在估的时候要表现的更加自信和果断，不至于给别人一种不专业的感觉。  

- **Archetecture**。有一天的时间是我们负责展开workshop，但是需要甲方的IT部门协作来构成我们要做的应用的技术架构。因为这个时候乙方的了解是相对较少的，这个时候我们只是一个owner，帮助该产品绘制完整的技术架构图。其中包括使用到的第三方的系统，要特别注意某个系统的某个专家是谁，在真正开发的时候不至于不知道应该找谁去合作，一样的，还是要多提问。 最后形成system context。

- **CFR**。Cross-Functional Requirements。当然业务需求是非常重要的，我们同时也要兼顾除了业务之外的一些偏技术方向的，需要effort来做的事情。举个列子，performance，一个应用的性能不是说做好了业务就能实现的，这个是需要长期的观察并enhance的。完整的CFR：

![inception-cfr-1]({{ "/assets/inception/cfr-1.png" | absolute_url }})  
![inception-cfr-2]({{ "/assets/inception/cfr-2.png" | absolute_url }})  

- **VPN**。安全是非常重要的一方面，所以在开发客户项目的同时，所有的操作都应该在VPN环境下进行，比如gitlab的提交，查看看板等等，但是一般都会有性能问题。以及包括各种账号来进行登陆验证，甚至需要客户给开发团队配置客户的电脑来方便各种活动的进行。  

- **Path to Production**。从开发的角度，应用是如何一步一步从开发到上线，到给真实的用户使用的。  
![inception-path-to-production]({{ "/assets/inception/path-to-production.png" | absolute_url }})  

- **设计展示**。作为前端开发，一定要关注这个环节，因为设计决定了后面的开发实现。这个难度比较大，一方面要考虑是否契合业务，另外一方面要考虑设计是否合理，对用户来说是否友好，要考虑极端情况，还要考虑可能发生的错误情况。但是这个展示并非非常细节的展示，有些问题可以问，有些细节的不影响大的方向的则不需要提问，否则显的太不专业。  

- **ways of working**。由于多方协作以及remote造成的时差，需要密切关注各种会议如何进行，找合适的时间进行，regular的进行，保证大家的上下文始终一致。同时也包括日常的敏捷实践，定义好某个feature是否ready的标准等。  

- **估点**。估点活动一般是放在快要结束的时候，即业务和user journey已经完成，需要开发在一起估点，最后根据这些点来确认我们要上线的时间要完成哪些功能，非常考验开发的经验和专业度，是否能从业务中嗅到风险，是否能根据前期所有的workshop的上下文中找到合理的业务需求，是否能提出关键性的问题，是否能说服大家你的观点是正确的，是否能准确快速地给出答案。最后一个活动非常有意思，有3～5轮测试，每一轮测试会问开发在一个星期内是否能完成，这时候我们是基于3对pair来做的，最后从这几轮中得到平均的点数，那么这个点数就是我们一个星期内可以完成的点数。以后的每一个迭代也会根据这个点数来把故事卡从backlog里面拖到ready for dev。话说我那个时候太怂了，总觉得会给团队埋坑，一直怀疑自己估点是否真的准确。事实来看，是非常准确的。项目做到现在，除了UX在block，其他的一切非常顺利，包括我们每一张卡没有delay，包括大家对tech的熟悉度也是按照正常的节奏来的。  

7月份的inception我到现在都记忆犹新，确实从中成长了很多，当然也从我们PM和BA小姐姐身上学到了很多，她们考虑问题非常全面，英文非常好，无障碍沟通，我呢，就是发现自己想的太少，总觉得很多事情不是开发该管的就不关注了，这个观念是非常不正确的，总要学会面对各种问题，而不只是技术方面的。当然，英文还是要持续提高才好。这也是我第一次参加inception，表现确实不理想，当发现即便是tech lead表现也没有想象中的那么好的时候，我个人心里还是稍微安慰了一点，但是，不能让别人瞧不起的啊，特别是外国友人，所以即便非常专业，没有表现出来，那也是不专业的。期待下次可以做的更好。

<hr />

1. [https://www.zybuluo.com/zhongjianxin/note/833520](https://www.zybuluo.com/zhongjianxin/note/833520);
2. [https://martinfowler.com/articles/lean-inception/](https://martinfowler.com/articles/lean-inception/);
3. [https://content.pivotal.io/blog/inception-knowing-what-to-build-and-where-you-should-start](https://content.pivotal.io/blog/inception-knowing-what-to-build-and-where-you-should-start);