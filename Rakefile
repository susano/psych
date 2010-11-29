begin
  require 'jeweler'
  Jeweler::Tasks.new do |gemspec|
    gemspec.name = "km-psych"
    gemspec.summary = "Port of Psych to use Jeweler as gem release manager"
    gemspec.description = "Psych is a YAML parser and emitter"
    gemspec.email = "aaronp@rubyforge.org, jbarnette@rubyforge.org"
    gemspec.homepage = "http://github.com/kristianmandrup/psych"
    gemspec.authors = ["Aaron Patterson", "John Barnette"]    
    gemspec.homepage = "http://github.com/tenderlove/psych"
    gemspec.add_development_dependency "test-unit", ">= 2.0.1"
    gemspec.files= FileList["lib/**/*", "ext/**/*"]
  end
  Jeweler::GemcutterTasks.new
rescue LoadError
  puts "Jeweler not available. Install it with: sudo gem install jeweler"
end

task :test => :compile

desc "merge psych in to ruby trunk"
namespace :merge do
  basedir = File.expand_path File.dirname __FILE__
  rubydir = File.join ENV['HOME'], 'git', 'ruby'
  mergedirs = {
    # From                          # To
    [basedir, 'ext', 'psych/']  => [rubydir, 'ext', 'psych/'],
    [basedir, 'lib/']           => [rubydir, 'ext', 'psych', 'lib/'],
    [basedir, 'test', 'psych/'] => [rubydir, 'test', 'psych/'],
  }

  rsync = 'rsync -av --exclude extconf.rb --exclude lib --exclude ".*" --delete'

  task :to_ruby do
    mergedirs.each do |from, to|
      sh "#{rsync} #{File.join(*from)} #{File.join(*to)}"
    end
  end

  task :from_ruby do
    mergedirs.each do |from, to|
      sh "#{rsync} #{File.join(*to)} #{File.join(*from)}"
    end
  end
end

# vim: syntax=ruby
