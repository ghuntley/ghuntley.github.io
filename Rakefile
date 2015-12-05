require "html/proofer"

# windows unicode
`chcp 65001`


task :default do
	`bundler exec guard`
end

task :test do
 sh "bundle exec jekyll build --trace"
 # ignore href="#" for the "Copy to clipboard" button
 HTML::Proofer.new("./_site", :href_ignore => ["#"]).run
end
