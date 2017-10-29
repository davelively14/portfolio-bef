---
layout: portfolio
title: "BlocToDo"
img: portfolio/bloc-todo/bloc-todo-cover.png # Image for homepage
page-img: portfolio/bloc-todo/bloc-todo-page-img.png # Image for landing page
date: 2017-03-25 00:00:00 +0500
description: API for a basic to-do list application # Add post description (optional)
tag: [Rails, Ruby, JSON, API]
icons: [icon-ruby-on-rails, icon-postgres]
weight: 31
---

![](https://github.com/favicon.ico) &nbsp;&nbsp;<a href="https://github.com/davelively14/bloc-todo/" target="\_blank">View on GitHub</a>

## Overview

To-do lists should be simple, while remaining flexible to use. It's one thing to have a physically limited stack of papers in your pocket. It's quite another to have a list that works easily on your Android, and your spouse's iPad, and your Windows computer (and any command line, worldwide).

Apps like Todo.txt go a long way towards solving this problem by creating a simple API that any programmer can easily navigate and extend. Like Todo.txt, this app is easy to control from the command line via curl commands or the browser. This API can support other platforms and allow programmers to build on this tool.

In this example, with a valid username and password, a user can list all users via this curl command:

```
$ curl -X PUT -u username:password http://localhost:3000/api/users/
```
<br>
Will return the following JSON object:
```json
[
  {"id":1,"username":"dlively","num_lists":2},
  {"id":2,"username":"username","num_lists":7},
  {"id":3,"username":"MelaraHetherspoon","num_lists":0},
  {"id":4,"username":"EdwynStark","num_lists":5},
  {"id":5,"username":"AlyssaArryn","num_lists":5},
  {"id":6,"username":"MarlonManderly","num_lists":6},
  {"id":7,"username":"Sterling","num_lists":0}
]
```

## Tech Stack

<a href="http://rubyonrails.org/" target="\_blank"><i class="icon-ruby-on-rails" style="font-size:4em;"></i></a> Rails is used for user management via static page frontend. It was also used as the API to handle received events from registered applications.
<br>
<br>
<a href="https://www.postgresql.org/" target="\_blank"><i class="icon-postgres" style="font-size:4em;"></i></a> PostgreSQL for the database layer.
