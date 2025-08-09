---
title: 'Paper Earth'

date: 2022-01-15T11:00:00-07:00
lastmod: 2022-01-15T11:00:00-07:00

draft: ture


categories:
  - 项目集
tags:
  - UnrealEngine4
  - 2d横版
---

## 基本信息
游戏类型：单人2D横版游戏  
引擎： UnrealEngine4  
运行平台： PC Windows(64-bit)  
素材参考: https://maaot.itch.io/fungal-grotto  
音乐和音效参考: https://www.bensound.com/   https://freesound.org/  
<!--more-->
[下载](/download/WindowsNoEditor.zip)
{{< video src="paper_earth.mp4" width="600" >}}

## 简介
Paper Earth 讲述了在地球被二向箔击中的漫长时间后，地球上进化出了可以适应二维世界的生物与生态系统系统，他们有的来自于三维动物的二维化，保有了大部分本来的特征与习性；有的是几种动物的组合，在二维化时被强行组合在了一起，机缘巧合之下进化成了二维世界中的物种。为了抵御失去太阳的严寒，高等的二维动物大多进化出了外壳将自己进行保护，坚硬的外壳很难在抵御严寒的同时也起到很好的保护作用。人类在二维化的最后时间段，建立了有一定几率可以使人类成功二维化的石棺，在地下建立了避难所，希望能为人类保留文明的种子。主角是成功的二维化人类，但是失去了人类时期的记忆，故事从他从石棺中醒来开始。

## 灵感来源
### 背景灵感
游戏背景的灵感来源于科幻小说三体。《三体》是刘慈欣创作的系列长篇科幻小说，讲述了地球人类文明和三体文明的信息交流、生死搏杀及两个文明在宇宙中的兴衰历程。在三体3中，地球文明受到了来自歌者文明维度打击，整个太阳系被二维化，书中有这样的描写：“这是一个死的世界，一张死的画。这个场面是那么的悲壮，真的悲壮！”

这样的场景是令我震撼的，但同样这样的解决也让我感到悲壮与感伤，因此我产生了描述二维化之后的世界，人类也许找到了生存的契机，生物也幸存下来发生了进化，而这样的世界没有书中描述的那样绝望，这也是我想表达的主题绝境之下也会有希望萌芽。

### 美术灵感
美术风格的灵感来源于《空洞骑士》。《空洞骑士》是一款2D动作冒险游戏，开发者是来自澳大利亚的一个只有三个人的小团队Team Cherry，2017年2月25日发售在PC平台。

空洞骑士色调和叙事结构，使我认识到了暗淡的色调对于孤独氛围的渲染作用，以及对于后末世世界下的主题表达作用，以及碎片化叙事所带来的不同体验与潜力。因此在美术风格整体基调上对《空洞骑士》进行了借鉴。

### 角色设计灵感
角色设计主要来源于《风之旅人》和《光·遇》。《风之旅人》是由Thatgamecompany开发制作的PSN游戏，《光·遇》是由游戏制作人陈星汉及其团队Thatgamecompany开发的社交冒险游戏，两作的主要角色都具有斗篷元素，因此我对其进行了参考。

武器的设计参考了唐刀中的横刀，唐刀是指唐代的刀，横刀无装饰，为普通兵士所佩带的战斗用刀。

## 游戏操作
**移动方式：**  
W 向上, S 向下, A 向左, D 向右, space 跳跃, shift 冲刺.

**攻击模式：**  
普通攻击：Q 向前劈砍  
特殊攻击：F 蓄力向前挥出一段剑气，对路径上的敌人造成范围伤害

**幽灵操作：**  
G 召唤一个量子幽灵并替换操作角色  
设定：(1) 移动: 悬浮模式, W 向上, S 向下, A 向左, D 向右, space 跳跃  (2) 存在时间具有时间限制，并且召唤存在cd

## 关卡设计
![](/images/paper_earth/guanka.png)
​
## 代码
### 地面动画
​首先通过is Falling判断玩家角色是否在空中，如果是则进入SkyAnimation模块，如果不是，则进入GroundAnimation模块，其次判断是否在冲刺，是则播放冲刺动画，不是则判断是否在攻击，是则判断是普通攻击还是特殊攻击，不是则通过Get Velocity判断玩家是否在行走，是则播放行走动画，不是则播放待机动画
![](/images/paper_earth/groundanimation.png)

### 幽灵控制
幽灵存在的时间设置为10秒，通过检测countdown是否小于0判断幽灵的行为，若大于0则播放幽灵行动动画，检测触发时间，若小于等于0则将摄像机视角调整为玩家视角后，销毁幽灵对象
![](/images/paper_earth/ghosthandle.png)

### 特殊攻击
specialattack通过F键盘事件触发，首先长按播放蓄力动画，其次播放攻击动画，并通过SpawnActor生成bullet对象，并对接触到的敌人造成伤害
![](/images/paper_earth/specialattack.png)
​
### 飞行敌人
飞行的敌人可以在地图内随意飞行，因此不需要加碰撞检测。通过检测enemy自身与玩家的角色的距离，若小于1000时，enemy朝玩家位置移动，在距离小于100时，对玩家产生30大小的伤害
![](/images/paper_earth/enemy.png)

### 空中动画
如果玩家判断为空中，判断是否在冲刺，是则播放冲刺动画，不是则判断是否在攻击，是则播放攻击动画，不是则播放下落动画
![](/images/paper_earth/skyanimation.png)

## 2D动画素材
<div style="display: flex; gap: 10px;">
  <!-- walk animation-->
  <div style="flex: 2;">
    <img src="/images/paper_earth/walk_animation.png" style="width: 100%; height: auto;" alt="行走动画">
    <figcaption style="text-align:center;">行走动画</figcaption>
  </div>

  <!-- bee animation + erinaceeaniae animation -->
  <div style="flex: 1; display: flex; flex-direction: column;">
    <img src="/images/paper_earth/bee_animation.png" style="width: 95%; height: auto;" alt="怪物1动画">
    <figcaption style="text-align:center;">怪物1动画</figcaption>
    <img src="/images/paper_earth/Erinaceeainae_animation.png" style="width: 95%; height: auto;" alt="怪物2动画">
    <figcaption style="text-align:center;">怪物2动画</figcaption>
  </div>
</div>

<!--stay animation + knife animation-->
<div style="display: flex;">
  <div style="flex: 2;">
    <img src="/images/paper_earth/stay_animation.png" style="width: 100%; height: auto;" alt="站立动画">
    <figcaption style="text-align:center;">站立动画</figcaption>
  </div>

  <div style="flex: 1;">
    <img src="/images/paper_earth/knife_animation.png" style="width: 100%; height: auto;" alt="召唤幽灵动画">
    <figcaption style="text-align:center;">召唤幽灵动画</figcaption>
  </div>
</div>

<!--attack2 sword animation + ghost animation-->
<div style="display: flex;">
  <div style="flex: 1;">
    <img src="/images/paper_earth/attack2_sword_animation.png" style="width: 100%; height: auto;" alt="剑气动画">
    <figcaption style="text-align:center;">剑气动画</figcaption>
  </div>

  <div style="flex: 2;">
    <img src="/images/paper_earth/ghost_animation.png" style="width: 100%; height: auto;" alt="幽灵动画">
    <figcaption style="text-align:center;">幽灵动画</figcaption>
  </div>
</div>

<!--attack1 sword animation + dash animation-->
<div style="display: flex;">
  <div style="flex: 1;">
    <img src="/images/paper_earth/attack1_sword_animation.png" style="width: 40%; height: auto; margin: 30px" alt="攻击特效">
    <figcaption style="text-align:center;">攻击特效</figcaption>
  </div>

  <div style="flex: 3;">
    <img src="/images/paper_earth/dash_animation.png" style="width: 100%; height: auto;" alt="冲刺动画">
    <figcaption style="text-align:center;">冲刺动画</figcaption>
  </div>
</div>

<!--attack1 animation + attack2 animation-->
<div style="display: flex;">
  <div style="flex: 1;">
    <img src="/images/paper_earth/attack1_animation.png" style="width: 100%; height: auto; margin: 20px" alt="普通攻击动画">
    <figcaption style="text-align:center;">普通攻击动画</figcaption>
  </div>

  <div style="flex: 2;">
    <img src="/images/paper_earth/attack2_animation.png" style="width: 100%; height: auto; margin: 20px" alt="特殊攻击动画">
    <figcaption style="text-align:center;">特殊攻击动画</figcaption>
  </div>
</div>

<!--jump animation-->
<div>
  <img src="/images/paper_earth/jump_animation.png" style="width: 85%; height: auto;" alt="跳跃动画">
  <figcaption style="text-align:center;">跳跃动画</figcaption>
</div>

## 未来计划
**boss1： 失败的同族**  
设定： 失败的二维人的聚合体，没有智慧，一切行为皆是为了遵循生存的欲望  
移动方式：上 下 左 右 跳跃 瞬移  
攻击方式：平砍 围绕自身的圆形攻击 围绕自身的环形攻击 大伤害直线攻击并伴有落石  

**boss2： 星火**  
设定：由灯灵汇聚形成的聚集体，在失去了太阳的照耀下，也足以照亮一方土地，已经进化出了外壳，具有一定的智慧  
移动方式：悬浮  
攻击方式：外壳未被击穿时，发生激光，并在接触时进行扣血，外壳击穿时，定时对角色所在的位置进行攻击  

**机制：外壳**  
怪物有外壳保护，只有在幽灵攻击并打破外壳后，才能对怪物造成伤害。
