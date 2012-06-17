require 'rubygems/package_task'
require 'rake/clean'
require 'yaml'
require 'fileutils'

NAME='sass_twitter_bootstrap'
INFOS = YAML::load(File.read("lib/webgen/bundle/#{NAME}/info.yaml"))

desc "Update the included Twitter Bootstrap files"
task :update do
  data_dir = "lib/webgen/bundle/#{NAME}/data/"
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
  puts "Generating VERSION file for #{INFOS['version']}"
  File.open('VERSION', 'w+') {|file| file.write(INFOS['version'] + "\n")}
end

spec = Gem::Specification.new do |s|
  s.name = "webgen-#{NAME}-bundle"
  s.version = INFOS['version']
  s.summary = INFOS['summary']
  s.description = INFOS['description']
  s.files = FileList.new(['lib/**/*', 'README.md', 'LICENSE', 'VERSION'])
  s.add_dependency('sass')
  s.require_path = 'lib'
  s.has_rdoc = false

  author_info = INFOS['author'].scan(/(?:^|,)\s*(.*?)\s*<(.*?)>/)
  s.authors = author_info.map(&:first)
  s.email = author_info.map(&:last)
  s.homepage = INFOS['homepage']
end

Gem::PackageTask.new(spec).define

task :gem => ['VERSION']

task :release => [:gem] do
  sh "gem push pkg/webgen-#{NAME}-bundle-#{INFOS['version']}.gem"
end
