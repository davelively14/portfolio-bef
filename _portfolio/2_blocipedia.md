---
layout: portfolio
title: "Blocipedia"
img: portfolio/blocipedia/blocipedia-cover.png # Image for homepage
page-img: portfolio/blocipedia/blocipedia-page-img.png # Image for landing page
date: 2017-07-28 10:00:00 +0500
description: User created markdown-based wikis. # Add post description (optional)
tag: [Rails, Ruby, REST]
icons: [icon-ruby-on-rails, icon-postgres, icon-bootstrap]
weight: 20
---

![](https://github.com/favicon.ico) &nbsp;&nbsp;<a href="https://github.com/davelively14/blocipedia" target="\_blank">View on GitHub</a>

## Overview

This application allows users to create public and private Markdown-based wikis using Ruby on Rails. We used Devise for user authentication, Pundit for authorization, Stripe for payment, and Redcarpet for rendering the Markdowns.  

<img src="{{site.baseurl}}/assets/img/portfolio/blocipedia/blocipedia-1.png" alt="Figure 1" style="width: 100%">
<small>**Figure 1.** *Main landing page. Users can create a new account or login to an existing account.*</small>

<img src="{{site.baseurl}}/assets/img/portfolio/blocipedia/blocipedia-2.png" alt="Figure 2" style="width: 100%">
<small>**Figure 2.** *After logging in or creating an account, users can view all public wikis or private wikis to which they have access.*</small>

<img src="{{site.baseurl}}/assets/img/portfolio/blocipedia/blocipedia-3.png" alt="Figure 3" style="width: 100%">
<small>**Figure 3.** *Users can create new wikis using Markdown.*</small>

<img src="{{site.baseurl}}/assets/img/portfolio/blocipedia/blocipedia-4.png" alt="Figure 4" style="width: 100%">
<small>**Figure 4.** *Result of new wiki from Figure 3.*</small>

<img src="{{site.baseurl}}/assets/img/portfolio/blocipedia/blocipedia-5.png" alt="Figure 5" style="width: 100%">
<small>**Figure 5.** *Users can upgrade to premium membership, which allows them to to post privately.*</small>

<img src="{{site.baseurl}}/assets/img/portfolio/blocipedia/blocipedia-6.png" alt="Figure 6" style="width: 100%">
<small>**Figure 6.** *We use Stripe's API to setup payment.*</small>

## Tech Stack

<a href="http://getbootstrap.com/" target="\_blank"><i class="icon-bootstrap" style="font-size:4em;"></i></a> Bootstrap for our front-end components and styling.
<br>
<br>
<a href="http://rubyonrails.org/" target="\_blank"><i class="icon-ruby-on-rails" style="font-size:4em;"></i></a> Rails is used for user management via static page frontend. It was also used as the API to handle received events from registered applications.
<br>
<br>
<a href="https://www.postgresql.org/" target="\_blank"><i class="icon-postgres" style="font-size:4em;"></i></a> PostgreSQL for the database layer.
