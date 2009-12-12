require 'rubygems'
require 'less'

task :default => [:generate_css]

task :generate_css do
  File.open("custom.css", "w") do |file|
    file.write(Less::Engine.new(File.new("custom.less")).to_css)
  end
end

