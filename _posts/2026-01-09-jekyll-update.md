---
navigation: true
cover: assets/images/jekyll-main.png
title: Jekyll Local Build Update for MacOS
date: 2026-01-09
class: post-template
tags: miscellaneous
layout: post
current: post
subclass: 'post'
---

I had made a post describing how I can built my Jekyll blog locally to make edits more efficient. 

However, recently I've switched to MacOS, and I've hit other problems which I will briefly describe their solution. 

Once I followed the instructions, I had hit the problem once I tried to run (please make sure you're in the local cloned repo of you Jekyll website)

```
bundle exec jekyll serve
```

The error was as follows:

```
/Users/burakayyorgun/.gem/ruby/3.4.1/gems/jekyll-3.9.0/lib/jekyll.rb:28: warning: csv was loaded from the standard library, but is not part of the default gems starting from Ruby 3.4.0.
You can add csv to your Gemfile or gemspec to silence this warning.
bundler: failed to load command: jekyll (/Users/burakayyorgun/.gem/ruby/3.4.1/bin/jekyll)
/Users/burakayyorgun/.rubies/ruby-3.4.1/lib/ruby/3.4.0/bundled_gems.rb:82:in 'Kernel.require': cannot load such file -- csv (LoadError)
	from /Users/burakayyorgun/.rubies/ruby-3.4.1/lib/ruby/3.4.0/bundled_gems.rb:82:in 'block (2 levels) in Kernel#replace_require'
	from /Users/burakayyorgun/.gem/ruby/3.4.1/gems/jekyll-3.9.0/lib/jekyll.rb:28:in '<top (required)>'
	from /Users/burakayyorgun/.rubies/ruby-3.4.1/lib/ruby/3.4.0/bundled_gems.rb:82:in 'Kernel.require'
	from /Users/burakayyorgun/.rubies/ruby-3.4.1/lib/ruby/3.4.0/bundled_gems.rb:82:in 'block (2 levels) in Kernel#replace_require'
	from /Users/burakayyorgun/.gem/ruby/3.4.1/gems/jekyll-3.9.0/exe/jekyll:8:in '<top (required)>'
	from /Users/burakayyorgun/.gem/ruby/3.4.1/bin/jekyll:25:in 'Kernel#load'
	from /Users/burakayyorgun/.gem/ruby/3.4.1/bin/jekyll:25:in '<top (required)>'
	from /Users/burakayyorgun/.gem/ruby/3.4.1/gems/bundler-4.0.3/lib/bundler/cli/exec.rb:61:in 'Kernel.load'
	from /Users/burakayyorgun/.gem/ruby/3.4.1/gems/bundler-4.0.3/lib/bundler/cli/exec.rb:61:in 'Bundler::CLI::Exec#kernel_load'
	from /Users/burakayyorgun/.gem/ruby/3.4.1/gems/bundler-4.0.3/lib/bundler/cli/exec.rb:24:in 'Bundler::CLI::Exec#run'
	from /Users/burakayyorgun/.gem/ruby/3.4.1/gems/bundler-4.0.3/lib/bundler/cli.rb:500:in 'Bundler::CLI#exec'
	from /Users/burakayyorgun/.gem/ruby/3.4.1/gems/bundler-4.0.3/lib/bundler/vendor/thor/lib/thor/command.rb:28:in 'Bundler::Thor::Command#run'
	from /Users/burakayyorgun/.gem/ruby/3.4.1/gems/bundler-4.0.3/lib/bundler/vendor/thor/lib/thor/invocation.rb:127:in 'Bundler::Thor::Invocation#invoke_command'
	from /Users/burakayyorgun/.gem/ruby/3.4.1/gems/bundler-4.0.3/lib/bundler/vendor/thor/lib/thor.rb:538:in 'Bundler::Thor.dispatch'
	from /Users/burakayyorgun/.gem/ruby/3.4.1/gems/bundler-4.0.3/lib/bundler/cli.rb:35:in 'Bundler::CLI.dispatch'
	from /Users/burakayyorgun/.gem/ruby/3.4.1/gems/bundler-4.0.3/lib/bundler/vendor/thor/lib/thor/base.rb:584:in 'Bundler::Thor::Base::ClassMethods#start'
	from /Users/burakayyorgun/.gem/ruby/3.4.1/gems/bundler-4.0.3/lib/bundler/cli.rb:29:in 'Bundler::CLI.start'
	from /Users/burakayyorgun/.gem/ruby/3.4.1/gems/bundler-4.0.3/exe/bundle:28:in 'block in <top (required)>'
	from /Users/burakayyorgun/.gem/ruby/3.4.1/gems/bundler-4.0.3/lib/bundler/friendly_errors.rb:118:in 'Bundler.with_friendly_errors'
	from /Users/burakayyorgun/.gem/ruby/3.4.1/gems/bundler-4.0.3/exe/bundle:20:in '<top (required)>'
	from /Users/burakayyorgun/.gem/ruby/3.4.1/bin/bundle:25:in 'Kernel#load'
	from /Users/burakayyorgun/.gem/ruby/3.4.1/bin/bundle:25:in '<main>'
```

I had gone through various troubles, but ultimetly the solution was simply as follows (for MacOS Sequoia 15.7), please also reference [this github page](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/creating-a-github-pages-site-with-jekyll)

1. first update the gemfile:
```
nano Gemfile
```
from this:
```
source "https://rubygems.org"
gem "ffi", "= 1.16.3"
gem "jekyll", "~> 3.9.0"
gem "github-pages", "~> 214"
gem "rake", "~> 13.0.3"
gem "slugify", "~> 1.0.7"
gem "jekyll-sitemap"
gem 'jekyll-paginate'
gem 'webrick', '>= 1.7.0'
```
to be this:

~~~
source "https://rubygems.org"
gem "github-pages", "~> GITHUB-PAGES-VERSION", group: :jekyll_plugins
~~~

Replace GITHUB-PAGES-VERSION with the latest supported version of the github-pages gem. You can find this version here: [Dependency versions](Replace GITHUB-PAGES-VERSION with the latest supported version of the github-pages gem. You can find this version here: Dependency versions.).


Then run 

```
bundle install
```

and then finally you can run 

```
bundle exec jekyll serve
```


And there you go! Please reach out if I missed something!!

See you next time!
