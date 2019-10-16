---
title: fiddler修改请求
date: 2019-10-16 14:12:52
tags: [fiddler]
categories: fiddler
---
业务系统中发现功能问题，通过F12工具查看后，发现某个请求状态码是403并且请求方法是OPTIONS.
{% asset_img 400请求.png This is an image %}
<!--more-->
此种情况下，判断可能是没有指定请求方式的问题导致403，用fiddler进行抓包，抓到这个403请求，右键选择replay->reissue and edit
{% asset_img fiddler修改.png This is an image %}
将请求方式修改为GET,并点击run to completion
{% asset_img fiddler修改请求.png This is an image %}
{% asset_img fiddler请求结果.png This is an image %}