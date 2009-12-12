require 'rubygems'
require 'less'

SSH_USER="owengriffin.com"
WP_DIR="/home/ogriffin/owengriffin.com/public/wp-content/themes/ogboumatic"

task :default => [:generate_css]

task :generate_css do
  File.open("custom.css", "w") do |file|
    file.write(Less::Engine.new(File.new("custom.less")).to_css)
  end
end

task :deploy => 'generate_css' do
  puts "Uploading changes to server"
  system("rsync -avzP --exclude \"Rakefile\" --exclude \".git\" --exclude \"*\\~\" --delete . #{SSH_USER}:#{WP_DIR}")
end
