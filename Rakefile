require 'bundler/gem_tasks'

begin
  require 'rspec/core/rake_task'
  RSpec::Core::RakeTask.new(:spec)
rescue LoadError
  puts "Couldn't find RSpec core Rake task"
end

begin
  require 'yard'
  YARD::Rake::YardocTask.new do |t|
    t.options = ['--verbose']
    t.files   = ['lib/**/*.rb', 'doc/**/*.md']
    t.stats_options = ['--list-undoc']
  end
rescue LoadError
  puts "Couldn't find YARD"
end

begin
  require 'yard-doctest'
  YARD::Doctest::RakeTask.new do |task|
    task.doctest_opts = %w[]
    task.pattern = 'lib/**/*.rb'
  end
rescue LoadError
  puts "Couldn't find yard-doctest"
end

# TODO: Make this conditional on the presence of CLOC or use an alternative way ...
namespace :stats do
  namespace :loc do
    task :lib do
      sh "cloc lib"
    end
    task :spec do
      sh "cloc spec"
    end
    task :all do
      sh "cloc lib spec"
    end
  end
end

task :default => [:spec, 'yard:doctest']
