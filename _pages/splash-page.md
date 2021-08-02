---
title: "等待完善... ..."
layout: splash
permalink: /splash-page/
date: 2021-07-31T11:48:41-04:00
header:
  overlay_color: "#000"
  overlay_filter: "0.5"
  overlay_image: /assets/images/unsplash-image-10.jpg
  actions:
    - label: "Learn More"
      url: "/photos/2019-08-12-tioman/"
  caption: "Photo credit: [**Unsplash**](https://unsplash.com)"
excerpt: "Travel to whererever is interesting."
intro: 
  - excerpt: "在追求自由的过程中，使奔放的灵魂得到释放。"
feature_row:
  - image_path: assets/images/night.jpeg
    alt: "placeholder image 1"
    title: "布达佩斯那一夜"
    excerpt: "站在布达城堡上一眼望去，尽是美景。"
  - image_path: /assets/images/chain-bridge.jpeg
    alt: "白天的链桥"
    title: "白天的链桥"
    excerpt: "看那蓝天，那白云，那灼热的太阳。"
    url: "/photos/2019-08-12-tioman/"
    btn_label: "Read More"
    btn_class: "btn--primary"
  - image_path: /assets/images/knight.jpeg
    title: "布达城堡里面军官的骑马演习"
    excerpt: "运气比较好，刚好遇到骑马演习，庄重，严肃。"
feature_row2:
  - image_path: /assets/images/shoes.jpeg
    alt: "placeholder image 2"
    title: "Placeholder Image Left Aligned"
    excerpt: '河边的鞋子，历史的痛。'
    url: "/photos/2019-08-12-tioman/"
    btn_label: "Read More"
    btn_class: "btn--primary"
feature_row3:
  - image_path: /assets/images/artist-1.jpeg
    alt: "placeholder image 2"
    title: "海边和小岛是最能让人放松的地方"
    excerpt: 'This is some sample content that goes here with **Markdown** formatting. Right aligned with `type="right"`'
    url: "/photos/2019-09-07-ubin/"
    btn_label: "Read More"
    btn_class: "btn--primary"
feature_row4:
  - image_path: /assets/images/singing.jpeg
    alt: "placeholder image 2"
    title: "Placeholder Image Center Aligned"
    excerpt: 'This is some sample content that goes here with **Markdown** formatting. Centered with `type="center"`'
    url: "#test-link"
    btn_label: "Read More"
    btn_class: "btn--primary"
feature_row5:
  - image_path: /assets/images/lingshan.jpeg
    alt: "Beijing 灵山"
    title: "Beijing 灵山"
    excerpt: 'This is some sample content that goes here with **Markdown** formatting. Centered with `type="center"`'
    url: "#test-link"
    btn_label: "Read More"
    btn_class: "btn--primary"
feature_row6:
  - image_path: /assets/video/wearings.mp4
    alt: "上班穿搭"
    title: "上班穿搭"
    excerpt: 'This is some sample content that goes here with **Markdown** formatting. Centered with `type="center"`'
    url: "#test-link"
    btn_label: "Read More"
    btn_class: "btn--primary"
---

{% include feature_row id="intro" type="center" %}

{% include feature_row %}

{% include feature_row id="feature_row2" type="left" %}

{% include feature_row id="feature_row3" type="right" %}

{% include feature_row id="feature_row4" type="center" %}

{% include feature_row id="feature_row5" type="left" %}

{% include feature_row id="feature_row6" type="right" %}
