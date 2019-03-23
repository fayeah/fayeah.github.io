---
title: Project Assessment
layout: default
categories: project-assessment
permalink: /:categories/
---

## Project Assessment    

对于敏捷项目的健康度的评估，是一个非常high level的非常全面的评估，然而我这里重点关注项目中开发这一领域的评估。Fendy是在ThoughtWorks工作十几年的非常有经验的开发，他来主导这次的评估，还带了一个另外一个在公司待了十几年的女性开发小虫，我觉得她人太好了，喜欢。这次内部评估的导火索是客户的vendor看了前端代码，本想参考一下前端的测试，但是发现我们ignore了很多测试在sonar里面，影响测试覆盖率的数据。甚至都捅到了MD胡凯那里，为了更好地准备后面客户对我们的评估，有了这次我们自己的评估，并采取相应的措施。    


### Workflow:     
Fendy和小虫分别找项目中经验比较多的开发进行谈话，我是跟小虫谈，主要谈到了项目的整体结构为什么这么设计，测试为什么这么搭建和配置，以及我本人也说了很多自己的困惑的点，包括项目中的分享，个人对前端的专注还是同时更多地了解后端，前端的单元测试是否应该测试dom，等等。 谈的过程非常开心，也没有什么压力，也没有感受到斥责或是怎样的。       

### Assessment Result Sharing:    

最后是Fendy给我们分享result，最开始的重点在于，**我们不是from bad to good， 而是from good to the best**。总之是做的更好。这个文档总结的非常地完善，我觉得应该记录下来，有机会我也可以去应用。    

这里我只记录格式：

title: {{project name}} Technical Assessment    
prepared by: {{name}}  {{email}}    
date:  {{result generated date}}    
note: For internal consumption and distribution within {{company name}} only This report contains commercially sensitive information    
table of contents:     
  Executive Summary: what we did, what we found, what we recommend    
  Background/Context: what trigger this assessment    
  Stakeholders: DP, DA, etc    
  Communication Plan: what time communicate with whom    
  Findings - Risks / Gaps:    
  Finds - Existing Mitigation Factors: what we did very well for now    
  Recommendations: what kind of actions we should do to make technical much better    

总结一下，客观来讲，确实前端做的没有那么尽如人意。
1. 我作为这个项目从开始到现在的lead，么有对angular的决策的能力，tech anchor的作用在我这里不能体现，这个我也跟小虫聊过，想要一个专家，但是做不到每个项目都有一个专家，自己可以多参加session，workshop等活动来提高自己；    
2. 测试覆盖率虽然有delivery pressure等压力，但是我本人还是么有要求特别严格，最后的建议是达到95%；    
3. 重大的决定并没有record到adr里面去，比如我们ignore一些测试是非常大的决定，应该在adr记录ignore 哪些测试，为什么要ignore，这个决定的时间，参与讨论的人员等待；    
4. 所有线上的bug都是前端的！！这个是我已知的，因为我本人经常性地做refactor工作，那么项目越来越大，代码越来越复杂，在单元测试覆盖率很低的情况下refactor，这个risk还是挺大的。也是我要改进的，一方面加测试，一方面小步refactor；    
5. sonar的安全扫描ignore了很多文件，是对自己地项目要求不严格的结果吧。     

事情已经发生，我们也只能根据建议去做。另外我对自己的要求还是不够严格，或者说是不够全面，对接上层不够紧密，对上层对我们的要求理解不透彻，不然从一开始就应该是更好的。    
