require "rubygems"
require "tmpdir"

require "bundler/setup"
require "jekyll"


desc "Generate page files"
task :generate do
  Jekyll::Site.new(Jekyll.configuration({
    "source"      => ".",
    "destination" => "_site"
  })).process
end


desc "Generate and publish site to master"
task :publish => [:generate] do
  Dir.mktmpdir do |tmp|
    cp_r "_site/.", tmp

    pwd = Dir.pwd
    Dir.chdir tmp

    system "git init"
    system "git add ."
    message = "Site updated at #{Time.now.utc}"
    system "git commit -m #{message.inspect}"
    system "git remote add origin git@github.com:pokonski/pokonski.github.io.git"
    system "git push origin master --force"

    Dir.chdir pwd
  end
end
