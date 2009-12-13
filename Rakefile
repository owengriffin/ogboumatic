require 'rubygems'
require 'less'
require 'fileutils'

SSH_USER="owengriffin.com"
WP_DIR="/home/ogriffin/owengriffin.com/public/wp-content/themes/ogboumatic"

META_CSS="meta.css"

THEMATIC_CSS = ['../thematic/library/styles/reset.css', 
                      '../thematic/library/styles/typography.css',
                      '../thematic/library/layouts/2c-r-fixed.css',
                      '../thematic/library/styles/images.css',
                      '../thematic/library/styles/plugins.css']


task :default => "style.css"

rule ".css" => ".less" do |file|
  File.open(file.name, "w") do |fh|
    fh.write(Less::Engine.new(File.new(file.source)).to_css)
  end
end

stylesheets = FileList["*.less"].sub(/less$/, "css")

def append_file(fh, filename)
  File.open(filename) do |fh1|
    while content = fh1.gets
      fh.write content
    end
  end
end

file "style.css" => stylesheets do |task|
  File.open("style.css", "w") do |fh0|
    append_file(fh0, META_CSS)
    THEMATIC_CSS.each { |stylesheet|
      append_file(fh0, stylesheet)
    }
    task.prerequisites.each { |stylesheet|
      append_file(fh0, stylesheet)
    }
  end
  system("java -jar yuicompressor.jar style.css -o style.css.cmp")
  FileUtils.mv('style.css.cmp', 'style.css')
end

task :clean do
  File.delete('style.css')
end

task :deploy => "style.css" do
  puts "Uploading changes to server"
  system("rsync -avzP --exclude \"Rakefile\" --exclude \".git\" --exclude \"*\\~\" --delete . #{SSH_USER}:#{WP_DIR}")
end
