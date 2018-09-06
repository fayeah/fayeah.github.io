---
title: 作为前端，如何配合实现SSO
layout: default
categories: sso
permalink: /:categories/
---

## 作为前端，如何配合实现SSO

以往做项目都是从半路加入，像登录认证、framework的选择等等都已经做好了。我一般是作为业务开发的角色，在已有的架子里填充血肉，实现一个又一个功能模块。这次有机会选择项目的framework，从0开始做起，个人感觉还是比较幸运的。  

这段时间有机会跟后端同学pair一起实现SSO的功能。wikipedia对SSO的解释如下：

> *单点登录（英语：Single sign-on，缩写为 SSO），又译为单一签入，一种对于许多相互关连，但是又是各自独立的软件系统，提供访问控制的属性。当拥有这项属性时，当用户登录时，就可以获取所有系统的访问权限，不用对每个单一系统都逐一登录。这项功能通常是以轻型目录访问协议（LDAP）来实现，在服务器上会将用户信息存储到LDAP数据库中。相同的，单一注销（single sign-off）就是指，只需要单一的注销动作，就可以结束对于多个系统的访问权限。*  
 
**从粗略估点到spike再到ready for dev**  

  在inception的时候我们已经得知做SSO是要与一个叫做ADFS的平台集成的，这也是客户已经在使用的平台。但是作为乙方，我们以前并没有使用过该平台，所以当时在做粗略估点（T-shirt Size）的时候还是给了一定的buffer来做这件事情。不至于后面真的到开发的时候加班加点写代码。这同时也体现了敏捷的好处。

**第三方系统的集成**  

  当然跟ADFS继承的spike我并没有参与其中，但是每天大家的更新我可以了解到相关的进度。我们的后端开发的小伙伴还是非常给力的，因为上一个迭代outlook的集成也是他一个人从头到尾完成了的。在毕业的第一年我也做过后端开发，做过跟salesforce的集成，深知跟第三方平台的集成是非常痛苦的一件事情。得需要这个平台的测试环境，该平台的API如何使用，需要做大量的调研工作，还要寻找使用API的最正确的方式，不仅仅是可以工作就好了。但是在一个多星期左右的时间，他就完成了这么一件事情，还是挺不容易的。有了神一样的队友，我们的生活当然会变得非常美好。  

 **实现方式的选择**  

  虽然后端得调研工作已经完成了，但是当我们真正开始做story卡的时候，前后端通讯的解决方案我们并没有达成一致。ADFS通过发送给它的token来识别是否可以进行下一步操作，还是应该跳到登陆页面。  

  讨论了不下三次，我们始终达不成一致。期间我们讨论过用url带参数的方式来传递token，也想过在前端的每个api request的header加上token，等待，这些方式都不能满足我们最好的实践。url传参数有安全性问题，在api的header里面依然没有办法实现后端给到前端token。  

  实际上ADFS最终会把token放到cookie里面去，所以理论上，当后端尝试在browser上发送要跳转到web应用的请求的时候带上这个token，前端就可以从browser里面拿到并在后面的每个request里面带上这个token即可。而前端可以用angular里面的authGuard来避免可能页面渲染了一半才能跳转到登陆页的现象，该方法会在每一个路由去checkLogin的状态。  
  
  于是我们的实现基本上就成形了。在用户第一次尝试访问web应用的时候，前端会去call authGuard所用到的checkLogin API，后端代码发现没有token，于是会返回一个401的error信息。前端会跳转到一个相对路径，这个路径就是让用户登陆的路径，涉及到一个基础知识`location.href`。当用户成功登陆之后会跳到`/`页面，这里有一个需求，希望用户能跳到之前想要跳到的页面。这里我们也想过几种实现，其中最简单的办法就是前端来把之前的url存到localStorage里面，如果成功登陆再从localStorage取出并清空localStorage。至此，SSO的登陆基本就实现了。  

  当然中间也是遇到了一些坑，比如前端cookie依赖的选择，angular里面我们最终选择了[`ngx-cookie`](https://github.com/salemdar/ngx-cookie#readme)，对单元测试以及angular本身的框架也是契合的。以及其中有一个403的需求。当用户可以登陆但是不能访问该web应用时，我们需要跳转到403页面。最开始大架构的时候没有考虑到这一点，所以当时的router只有一级，因为header和navigation bar都是静态元素。当加入了403之后，我们需要引入children router，并且需要把child router放到一个component里面，因为一个template并不能放两个`<router-outlet>`。  

  ```
    const appRoutes: Routes = [
    {
      path: '',
      component: ContainerComponent,
      children: [
        {
          path: 'router1',
          loadChildren: './feature1/feature1.module#Feature1Module',
          canActivate: [AuthGuard],
        },
        {
          path: 'router2',
          loadChildren: './feature2/feature2.module#Feature2Module',
          canActivate: [AuthGuard],
        },
        {
          path: 'router3',
          loadChildren: './feature3/feature3.module#Feature3Module',
          canActivate: [AuthGuard],
        }
        { path: '', pathMatch: 'full', redirectTo: '/router1' },
      ],
    },
    { path: '403', component: 403Component},
    { path: '**', pathMatch: 'full', redirectTo: '/router1' },
  ];
  ```


**你考虑全面里么？**   

  本以为已经做的差不多了，可以结束SSO的开发了。但是，事情并没有结束。  

- 以前需求里面涉及到用户的数据，包括取数据的方式，都需要做改动。还好以前在做feature的时候考虑到了这一点，只要在call api的时候稍微改一下就好了。  
- 附件下载，如果当时讨论的结果是在header里面加token，那么下载并实现不了，因为`window.location`只是浏览器的行为，没办法自定义header信息。  
- 前面提到的403。  
- 存储current的url。  

总而言之，还是学到不少东西的。以前也做angular，但是并没有像这次一样从头开始跟，很多东西还是失去了学习的机会。感恩有大家的肯定，让我在挑战新的尝试的时候给予的鼓励。同时也让我相信，原来很多看似不可能的事情是可以做到的。只不过，还有很长的路要走。  
