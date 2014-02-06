desc "compile and run the site"
task :default do
  Rake::Task["serve"].invoke
end

desc "compile and run the site"
task :serve do
  Rake::Task["rsync"].invoke
  pids = [
    spawn("scss --watch _assets/stylesheets/application.scss:assets/application.css"),
    spawn("jekyll serve --watch")
  ]
 
  trap "INT" do
    Process.kill "INT", *pids
    exit 1
  end
 
  loop do
    sleep 1
  end
end

desc "compile the site"
task :build do
  Rake::Task["rsync"].invoke
  `scss _assets/stylesheets/application.scss:assets/application.css`
  `jekyll build`
end

desc "common rsync used in build and serve tasks"
task :rsync do
  FileUtils.mkdir('_site')
  FileUtils.mkdir('assets')
  `rsync _assets/images/* assets`
  `rsync _assets/javascripts/* assets`
  `rsync _vendor/assets/javascripts/* assets`
end

desc "clean the site"
task :clean do
  FileUtils.rm_rf('_site')
  FileUtils.rm_rf('assets')
end
