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

- 


### dev应该关注哪些  

整个inception时间两周，team做了非常多的事情，我不可能把每一个细节都展现出来。我更在乎dev需要关注哪些，以及在下一次inception里面如何做的更好一些。 

- **提问**。首先，开发肯定是几乎全程都参加的，除了几个meeting需要技术和业务的分开来进行。不论是客户在介绍还是UX在介绍的时候，多注意思考，考虑周到一些，提出一些有意义的问题，帮助理清上下文，这个是非常重要的。  

- **果断并自信**。在inception结束的前两天会让开发进行粗略估点，这个估点当然也要考虑全面，关键是在估的时候要表现的更加自信和果断，不至于给别人一种不专业的感觉。  

- 

