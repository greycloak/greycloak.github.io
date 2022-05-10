---
layout: post
title:  "Quick Tip: Exporting to CSV from Rails console"
date:   2013-10-08 10:34:56 +0530
categories: tutorial
author:     vince
image:      /images/posts/linux-image.jpg
tags:
 - ruby
 - rails
 - git
---

This is an ugly solution but one that can come in handy if you just need to get some sample data out of your rails application. My particular use case was exporting data from various tables into a CSV file so I could use a 3rd party email service. We have users in a multi-tenant app so it's not quite so simple as just exporting a single table. This is something you almost certainly don't need to use if your SQL-fu is strong. For the rest of us, here we go:

require 'csv'

    file = "#{Rails.root}/public/users.csv"

    userrefs = UserReference.where(:tenant_id => 7)

    CSV.open( file, 'w' ) do |writer|
      userrefs.each do |ur|
        next unless ur.user.present?
        writer << [ur.user.username, ur.user.email]
      end
    end

So what's going on here? Well, first things first we require the CSV library since we'll be manipulating a CSV file.

Next, we create a string that points to that file (make sure the file is created first). The userrefs variable grabs the top level data you need and from there we cycle though them adding records to our CSV file based on any associations we have. Done!

Pretty straight-forward but handy to have in a pinch!
