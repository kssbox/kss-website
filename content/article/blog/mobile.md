---
title: 移动端适配原理与实战(share)
date: 2024-03-15 
---


- 目标
    - 理解移动端适配原理与工程化方案、理解常用像素概念、理解视口概念
- 什么是适配
    
    可以在不同屏幕的尺寸、分辨率和显示比例中，展示合适的界面内容、布局与交互。
    
    - 适配方案
        
        响应式设计（Responsive Design）
        
        媒体查询、rem、viewport
        
        流式布局（Fluid Layout）
        
        百分比
        
        固定布局（Fixed Layout）：
        
- 移动端适配原理与代码案例
    - 百分比
    - 媒体查询
    - rem
    - viewport
    - 搭配 webpack 方案
    - 高 dpr 屏幕的 1px 实现
- 像素与像素之间的关系
    - 分类
        - 设备像素（device pixels）、设备分辨率、物理像素
            - 硬件层面，制造的时候决定。
        - 设备独立像素（Device Independent Pixels）、逻辑分辨率、逻辑像素、
            - 操作系统层面，可以通过设置分辨率或放大缩小调整。
            
            ```jsx
            window.screen.width
            ```
            
        - css像素
            - 浏览器层面，像素数量不可变，但是大小可变。
    - 关系
        - 设备像素比（devicePixelRatio）由设备独立像素 除以 设备像素获得
        
        ```jsx
        window.devicePixelRatio
        ```
        
        - 设备独立像素放大缩小的影响
            - 当 dip 变大时，dpr 变小，同时 1px 所对应的 dp 变少，视觉上变小。
        - 浏览器放大缩小的影响
            - 元素的css像素数量不会改变，改变的只是每个css像素的大小。只不过每个css像素的宽度和高度变为原来的两倍。如果原本元素宽度为128个设备独立像素，那么缩放200%以后元素宽度为256个设备独立像素（css像素宽度始终是128）。
- 视口
    - 布局适口（layout viewport）
        
        ```jsx
        document.documentElement.clientWidth
        ```
        
    - 可视视口（visual viewport）
        
        ```jsx
        window.innerWidth;
        ```
        
    - 完美视口
        - 布局视口与可视视口 1:1。
        - 由html 源标签设置
            - 屏幕宽度自适应调整。网页内容将以设备屏幕的实际宽度为基准自适应调整，避免了默认的缩放行为。
            - 不设置移动设备上的浏览器会以一个较大的视口宽度（通常是980像素）进行呈现网页。
            - 当写上meta标签后，width=device-width,使css像素与设备独立像素链接了起来。iphone的像素比为2，则1CSS像素(设备独立像素占据了 2*2个物理像素)
        
        ```html
        <meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1, user-scalable=no">
        ```
        
        - 在移动端中（PC端没这种情况），元素过大，会出现可视视口大于布局视口的情况。如在 375 的 iphon12中定义宽度为 500 的元素

[代码](https://github.com/KevinBrother/share/tree/develop/mobile-adapt-share)