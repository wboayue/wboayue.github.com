---
layout: draft
title: "Rails 4 Engines with RSpec and FactoryGirl"
date: 2014-04-02 12:42
comments: true
categories: ruby,rails,factorygirl,rspec
---

I've been using [Rails Engines](http://guides.rubyonrails.org/engines.html) to share reusable code across multiple applications. Engines, by default, support [MiniTest](http://ruby-doc.org/stdlib-2.1.0/libdoc/minitest/rdoc/MiniTest.html) and [fixtures](http://guides.rubyonrails.org/testing.html#the-low-down-on-fixtures).

My preferred testing tools are [RSpec](http://rspec.info/) and [FactoryGirl](https://github.com/thoughtbot/factory_girl). This is a guide for creating a Rails Engine configured for RSpec and Factory girl.

1. Create the engine

  `rails plugin new ENGINE_NAME --dummy-path=spec/dummy --skip-test-unit --mountable`

  * `--dummy-path=spec/dummy` specifies the path for the test application. Default path is test/dummy
  * `--skip-test-unit` skips the generation of the test unit files
  * `--mountable` generates a namespaced engine

2. Add RSpec and FactoryGirl dependencies to gemspec.

  s.add_development_dependency 'rspec-rails'
  s.add_development_dependency 'factory_girl_rails'

Specify test files

s.test_files = Dir["spec/**/*"]

bundle install

Configure engine to use RSpec and FactoryGirl
lib/engine_name/engine.rb

module GemName
  class Engine < ::Rails::Engine
    isolate_namespace GemName

    config.generators do |g|
      g.test_framework :rspec
      g.fixture_replacement :factory_girl, :dir => 'spec/factories'
    end
  end
end

. Run the rspec generator:

rails generate rspec:install


Modify spec helper to load the dummy application

require File.expand_path("../../config/environment", __FILE__)

require File.expand_path("../dummy/config/environment", __FILE__)
