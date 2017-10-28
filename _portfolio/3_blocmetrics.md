---
layout: portfolio
title: "Blocmetrics"
img: portfolio/blocmetrics/blocmetrics-cover.png # Image for homepage
page-img: portfolio/blocmetrics/blocmetrics-page-img.png # Image for landing page
date: 2017-03-15 00:00:00 +0500
description: An analytics service to track events on websites # Add post description (optional)
tag: [Rails, Ruby, Analytics, Tracking]
icons: [icon-ruby-on-rails, icon-postgres]
---

![](https://github.com/favicon.ico) &nbsp;&nbsp;<a href="https://github.com/davelively14/blocmetrics" target="\_blank">View on GitHub</a>

## Overview

Blocmetrics provides a way to track customized events on a website. A user will create an account on Blocmetrics and register their apps by providing a name and a url. Users can then build and send an event object from their website to Blocmetrics. Blocmetrics will match the call via the origin's url with a registered application and then persist the event. Users can login to Blocmetrics and view event metrics.

<img src="{{site.baseurl}}/assets/img/portfolio/blocmetrics/blocmetrics-my-apps.png" alt="Figure 1" style="width: 100%">
<small>**Figure 1.** *User main menu listing all registered apps.*</small>

<img src="{{site.baseurl}}/assets/img/portfolio/blocmetrics/blocmetrics-new-app.png" alt="Figure 1" style="width: 100%">
<small>**Figure 2.** *Registering a new application.*</small>

<img src="{{site.baseurl}}/assets/img/portfolio/blocmetrics/blocmetrics-summary.png" alt="Figure 1" style="width: 100%">
<small>**Figure 3.** *Summary for a registered application with events received from the website.*</small>

## Tech Stack

<a href="http://rubyonrails.org/" target="\_blank"><i class="icon-ruby-on-rails" style="font-size:4em;"></i></a> Rails is used for user management via static page frontend. It was also used as the API to handle received events from registered applications.
<br>
<br>
<a href="https://www.postgresql.org/" target="\_blank"><i class="icon-postgres" style="font-size:4em;"></i></a> PostgreSQL for the database layer.
