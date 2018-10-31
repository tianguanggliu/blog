---
title: material
title_cn: material中hammerjs无效
keywords: material滑动无效 angular material 滑动无效 hammer 无效
date: 2018-10-31 09:02:10
tags:
    - Material
    - Angular
categories: Angular
description: material hammer 无效
img: http://pgtoq1cmw.bkt.clouddn.com/blog/article/covers/angular-material-banner.jpg
---
### 技术问题
> [Angular Material](https://material.angular.io/ "Angular Material") Material Design components for Angular, 最近项目中用到 ** Angular Material ** 按照官网 [guides](https://material.angular.io/guides) 完成后发现手势相关的组件无效！！

### 解决问题

首先按照官方指导引入 hammerjs, 然后在app.module中加入如下代码即可

```javascript
import { GestureConfig} from '@angular/material';
import { BrowserModule, HAMMER_GESTURE_CONFIG} from '@angular/platform-browser';

@NgModule({
  declarations: [...],
  imports: [...],
  providers: [{ provide: HAMMER_GESTURE_CONFIG, useClass: GestureConfig }],
  bootstrap: [...]
})
```
希望我的分享能解决您遇到的问题！！！