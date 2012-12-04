require 'sass'
require 'haml'

task :default => :build

desc 'Build site'
task :build do
	sh 'mkdir -p _site'
	sh 'rm -rf _site/*'
	sassengine = Sass::Engine.for_file("css/application.sass", :syntax => :sass, :style => :compressed)
	css = sassengine.render()

	File.open("_site/application.css", "w") { |f| f.write(css) }

	haml = IO.read("index.haml")
	hamlengine = Haml::Engine.new(haml)
	html = hamlengine.render()

	File.open("_site/index.html", "w") { |f| f.write(html) }

	sh 'cp -R font _site'
end

desc 'Build and deploy'
task :deploy => :build do
  sh 'rsync --checksum -rtzh --progress --delete _site/ www:/var/www/web_page_today'
end
