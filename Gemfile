source "https://rubygems.org"

# Pins the same Jekyll/plugin versions GitHub Pages uses to build the site,
# so a local build matches what actually gets deployed.
gem "github-pages", group: :jekyll_plugins

# Ruby 3.0+ dropped webrick from the standard library; jekyll serve needs it.
gem "webrick"

# Ruby 3.4+ dropped these from default gems; the pinned (old) jekyll/rouge
# still expect them to be present without an explicit require.
gem "csv"
gem "logger"
gem "base64"
gem "bigdecimal"
