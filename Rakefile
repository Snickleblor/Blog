require 'rake'

task :dev do
  sh "bundle exec jekyll serve"
end

task :sync do
  sh "git add ."
  sh "git commit -m 'Automatic Update #{Time.now.strftime('%Y-%m-%d %H:%M:%S')}'"
  sh "git push"
end
