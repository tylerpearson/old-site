require "rake"
require 'stringex'
require 'fileutils'
# require "open-uri"

source_dir = "./"
posts_dir = "_posts"
new_post_ext = "md"

#
# From Octopress.
#
desc "Begin a new post in #{source_dir}/#{posts_dir}"
task :create, :title do |t, args|
  mkdir_p "#{source_dir}/#{posts_dir}"
  args.with_defaults(:title => 'new-post')
  title = args.title
  filename = "#{source_dir}/#{posts_dir}/#{Time.now.strftime('%Y-%m-%d')}-#{title.to_url}.#{new_post_ext}"

  if File.exist?(filename)
    abort("rake aborted!") if ask("#{filename} already exists. Do you want to overwrite?", ['y', 'n']) == 'n'
  end

  puts "Creating new post: #{filename}"
  open(filename, 'w') do |post|
    post.puts "---"
    post.puts "layout: post"
    post.puts "title: \"#{title.gsub(/&/,'&amp;')}\""
    post.puts "date: #{Time.now.strftime('%Y-%m-%d %H:%M')}"
    post.puts "tags: []"
    post.puts "categories: "
    post.puts "---"
  end
end

desc "Process LESS into CSS."
task :less do
  FileUtils.mkdir_p 'assets/css/'
  sh "lessc assets/_less/all.less -x > assets/css/site.css"
end