# frozen_string_literal: true

source "https://rubygems.org"

gem "jekyll", "~> 4.2"
gem "jekyll-theme-chirpy"

# Plugins
group :jekyll_plugins do
  gem "jekyll-archives"
  gem "jekyll-sitemap"
  gem "jekyll-seo-tag"
  gem "jekyll-feed"
  gem "jekyll-redirect-from"
  gem "jekyll-gist"
  gem "jekyll-include-cache"
  gem "jekyll-sass-converter"
end

# For tests
gem "html-proofer", group: :test

# Windows and JRuby does not include zoneinfo files
platforms :mingw, :x64_mingw, :mswin, :jruby do
  gem "tzinfo", ">= 1", "< 3"
  gem "tzinfo-data"
end

# Performance-booster for watching directories on Windows
gem "wdm", "~> 0.1.1", :platforms => [:mingw, :x64_mingw, :mswin]

# Lock `http_parser.rb` gem to `v0.6.x` on JRuby builds since newer versions of the gem
# do not have a Java counterpart.
gem "http_parser.rb", "~> 0.6.0", :platforms => [:jruby]