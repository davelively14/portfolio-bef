---
layout: portfolio
title: "Bloc Chat"
img: portfolio/bloc-chat/bloc-chat-cover.png # Image for homepage
page-img: portfolio/bloc-chat/bloc-chat-page-img.png # Image for landing page
date: 2017-01-30 10:00:00 +0500
description: Realtime messaging with Firebase and AngularJS. # Add post description (optional)
tag: [AngularJS, Firebase]
icons: [icon-angular, icon-fire-alt, icon-grunt]
weight: 20
---

![](https://github.com/favicon.ico) &nbsp;&nbsp;<a href="https://github.com/davelively14/bloc-chat" target="\_blank">View on GitHub</a>

## Overview

A chat app that allows users to connect to various chat rooms and send messages. Using the AngularJS binding [AngularFire](https://github.com/firebase/angularfire), we store those messages remotely on a Firebase server. When users join a room, they have access to the messages.

<img src="{{site.baseurl}}/assets/img/portfolio/bloc-chat/bloc-chat-1.png" alt="Figure 1" style="width: 100%">
<small>**Figure 1.** *Creating a new user.*</small>

<img src="{{site.baseurl}}/assets/img/portfolio/bloc-chat/bloc-chat-2.png" alt="Figure 2" style="width: 100%">
<small>**Figure 2.** *Once logged in, our AngularJS app retrieves a list of available rooms from our Firebase.*</small>

<img src="{{site.baseurl}}/assets/img/portfolio/bloc-chat/bloc-chat-3.png" alt="Figure 3" style="width: 100%">
<small>**Figure 3.** *Click on a room and you can view and send messages.*</small>

## Tech Stack

<a href="https://angularjs.org/" target="\_blank"><i class="icon-angular" style="font-size:4em;"></i></a> AngularJS for our frontend user interface.
<br>
<br>
<a href="https://firebase.google.com/" target="\_blank"><i class="icon-fire-alt" style="font-size:4em;"></i></a> Use Google's Firebase as our database in the cloud.
<br>
<br>
<a href="https://gruntjs.com/" target="\_blank"><i class="icon-grunt" style="font-size:4em;"></i></a> Grunt is our JS task runner.
