---
layout: post
title: AR Implementation in Navigation System
tags: Augmented Reality, Navigation, iOS
date: 2016-05-31
excerpt_separator: <!--more-->
---

<img src="/images/fulls/AR.jpg" class="fit image">
2016 is the initial year of Virtual Reality. Influenced by the trends, many technical companies devote themselves to the revolution of traditional interaction. Accompanied with the spring of smart devices, data management, data retrieval and algorithm are all enhanced in a stable pace. In another part, with the popularization of smart phones, the cost of technology in life become lower and lower. According to these points, the paper uses the combination of the technology of Augmented Reality and iOS development to realize a simple Augmented Reality on iPhone platform...

<!--more-->

# AR Implementation in Navigation System #
<script type="text/javascript" src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=default"></script>

Tags: Augmented Reality, Navigation, iOS


## Intro ##

Through the analysis of demand of current applications and the thought of application area of Augmented Reality, the paper aims at the combination of navigation systems and Augmented Reality. The application based on iOS platform and it can be run on many types of iPhone. The technical proposal mainly contains information retrieval and processing of map, data management of local hardware, merging algorithm of Augmented Reality and searching function. In addition, MOVE design pattern are used in system to improve the quality of source code.

In iOS design part, the system uses the co-processing of data at local device and the server. In view design, the system rewrites the method drawRect to accomplish customized user interface. Apache server is used at the server side and JSON is used as the carrier of transferred data, which has a relatively high efficiency. In Augmented Reality part, the system use Monitor-Based proposal and Location-Based merging algorithm. The system test shows the design reach the standard of accuracy.


## Merging Algorithm ##

In order to merge the virtual mark label into the real environment from the camera. The system need to caculate \\( (x,y) \\) in device screen based on target location, user location and the posture of device. The simple formula is \\( (xInScreen,yInScreen)=f(userLocation,targetLocation,infoPosture) \\). Every location contains a latitude info and a longitude info.
Look the diagram for calculation.

　　　![Caculation Diagram](http://ww3.sinaimg.cn/large/6e302d8bgw1f4f1ng6k89j20ar0b63z2.jpg)

**According to formiula of trihedral angle.**

$$ \cos(c) = \cos(90-Latitude\_B)\times\cos(90-latitude\_A)+\sin(90-Latitude\_B)\times\sin(90-Latitude\_A)\times\cos(Longitude\_B-Longitude\_A) $$

$$ \sin(c)=\sqrt{1-\cos^2(c)} $$

$$ \frac{a}{\sin(A)}=\frac{b}{\sin(B)}=\frac{c}{\sin(C)} $$

**The direction angle calculation formula.**

$$ A=\arcsin\frac{\sin(90-Latitude\_B)\times\sin(Longitude\_B-Longitude\_A)}{\sin(c)} $$

**X in Screen.**

　　　![X Caculation](http://ww2.sinaimg.cn/large/6e302d8bgw1f4f1tradpbj20g50bmmxc.jpg)

$$ \frac{width}{2\times\tan(\frac{\omega}{2})}=\frac{\frac{width}{2}-tw}{\tan(H-TH)} $$

$$ tw=\frac{1}{2}\times(width-\frac{width\times\tan(H-TH)}{\tan(\frac{\omega}{2})}) $$

**Y in Screen.**

　　　![Y Calculation](http://ww2.sinaimg.cn/large/6e302d8bgw1f4f1u8qozej20la0cf74l.jpg)

$$ th=\frac{1}{2}\times(height-\frac{height\times GravityX}{\tan(\frac{\omega}{2})\times GravityY}) $$

**Implementation Result**
After setting up APP, the interface shows the effect of merging algorithms.

　　　![Result](http://ww4.sinaimg.cn/large/6e302d8bgw1f4f24jrkf7j20bo0len07.jpg)

　　　![Result](http://ww3.sinaimg.cn/large/6e302d8bgw1f4f25kw9kwj20bo0leq68.jpg)


## FOLLOW UP ##

The merging algorithm based on **CLLocation** and **CMMotion**. Data from hardware is needed to pre-process before using. For instance, when the device in a horizontal posture, the data should be modified before calculation.

***
