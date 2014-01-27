desc "compile and run the site"
task :default do
  Rake::Task["serve"].invoke
end

desc "compile and run the site"
task :serve do
  pids = [
    spawn("rsync _assets/images/* assets"),
    spawn("rsync _assets/javascripts/* assets"),
    spawn("rsync _vendor/assets/javascripts/* assets"),
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
  `rsync _assets/images/* assets`
  `rsync _assets/javascripts/* assets`
  `rsync _vendor/assets/javascripts/* assets`
  `scss _assets/stylesheets/application.scss:assets/application.css`
  `jekyll build`
end

desc "clean the site"
task :clean do
  FileUtils.rm_rf('_site')
  FileUtils.rm_rf('assets')
end