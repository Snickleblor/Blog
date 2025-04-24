require "rake"
require "date"
task :dev do
  sh "bundle exec jekyll serve"
end

task :sync do
  sh "git add ."
  sh "git commit -m 'Automatic Update #{Time.now.strftime('%Y-%m-%d %H:%M:%S')}'"
  sh "git push"
end

task :post do
  date = Date.today.strftime("%Y-%m-%d")
  
  posts = Dir.glob('_posts/*')
  highest_counter = 0

  posts.each do |post|
    if post =~ /-(\d+)\.md$/
      counter = $1.to_i
      highest_counter = [highest_counter, counter].max
    end
  end

  new_counter = highest_counter + 1

  filename = "_posts/#{date}-#{new_counter}.md"

  content = <<~POST
    ---
    layout: post
    title: "Title"
    date: #{date} #{Time.now.strftime("%H:%M:%S %z")}
    categories: []
    tags: []
    ---
    
    # Title
    
  POST

  FileUtils.mkdir_p('_posts') unless Dir.exist?('_posts')
  File.write(filename, content)

  puts "Post created: #{filename}"
end