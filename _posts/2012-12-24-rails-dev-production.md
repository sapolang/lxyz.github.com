---
layout: post
title: Test Rails App Production Environment on Dev Machine
tags: 
 - rails
 - Test
---
To Test rails app's Production Environment on dev machine,we should deploy to dev machine first.These tips show how we need to do:

1.create & migrate databases

    rake db:create RAILS_ENV=production
    //create production database use the parameter 'RAILS_ENV=production'

    rake db:migrate RAILS_ENV=production
    //migrate procution tables
 
2.precompile assets
    bundle exec rake assets:precompile RAILS_ENV=production
    //this commands tells system that precompile all the assets.
And this is not enough,we need to change something as follow:
    //in file RAILS_APP_PATH/config/environments/production.rb
    config.serve_static_assets = false
set the value to true,like follows:
    config.serve_static_assets = true
3.restart our rails app:
    rails s -e production