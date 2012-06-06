require 'rubygems/package_task'
require 'rake/clean'
require 'fileutils'

########################################################################
VERSION='1.0.0'
NAME='webgen-sass_twitter_bootstrap-extension'
########################################################################

desc "Update the included Twitter Bootstrap files"
task :update do
  data_dir = "lib/webgen/extension/sass_twitter_bootstrap/data/"
  dir = ENV['dir']
  raise "The given path is not a directory: #{dir}" unless File.directory?(dir)

  FileUtils.cp(Dir.glob("#{dir}/lib/*.scss"), File.join(data_dir, "css", "bootstrap"))
  FileUtils.cp(Dir.glob("#{dir}/img/*"), File.join(data_dir, "img"))
  FileUtils.cp(Dir.glob("#{dir}/js/*.js"), File.join(data_dir, "js"))

  var_file = File.join(data_dir, 'css', 'bootstrap', '_variables.scss')
  content = File.read(var_file)
  content.sub!(/"..\/img\/glyphicons-halflings.png"/, "relocatable('/images/glyphicons-halflings.png')")
  content.sub!(/"..\/img\/glyphicons-halflings-white.png"/, "relocatable('/images/glyphicons-halflings-white.png')")
  File.open(var_file, 'w') {|f| f.write(content)}

  puts "Done!"
end

CLOBBER << "VERSION"
file 'VERSION' do
  puts "Generating VERSION file"
  File.open('VERSION', 'w+') {|file| file.write(VERSION + "\n")}
end

spec = Gem::Specification.new do |s|
  s.name = NAME
  s.version = VERSION
  s.summary = "webgen extension for Twitter Bootstrap framework support"
  s.description = <<EOF
This webgen extension provides the Sass port of the Twitter Bootstrap
framework. It allows the easy inclusion of parts or all of the framework
in a webgen website.
EOF
  s.files = FileList.new(['lib/**/*', 'README.md', 'LICENSE', 'VERSION'])
  s.add_dependency('sass')
  s.require_path = 'lib'
  s.has_rdoc = false

  s.author = 'Thomas Leitner'
  s.email = 't_leitner@gmx.at'
  s.homepage = "http://github.com/gettalong/#{NAME}"
end

Gem::PackageTask.new(spec).define

task :gem => ['VERSION']

task :release => [:gem] do
  sh "gem push pkg/#{NAME}-#{Webgen::VERSION}.gem"
end
