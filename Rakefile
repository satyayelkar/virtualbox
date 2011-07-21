require "rbconfig"
require "rubygems"
require "bundler/setup"
require "rake/testtask"

require "cucumber"
require "cucumber/rake/task"
Bundler::GemHelper.install_tasks

include Rake::DSL

task :default => "test:units"

namespace :test do
  Rake::TestTask.new(:units) do |t|
    t.libs << "test"
    t.pattern = 'test/**/*_test.rb'
  end

  Cucumber::Rake::Task.new(:integration) do |t|
    t.cucumber_opts = "features --format pretty"
  end

  begin
    require "rcov/rcovtask"

    Rcov::RcovTask.new do |t|
      t.libs << "test"
      t.test_files = FileList["test/**/*_test.rb"]
      t.output_dir = "test/coverage"
      t.verbose = true
    end
  rescue LoadError; end
end

if RbConfig::CONFIG["host_os"] !~ /^darwin11/
  # YARD is broken on Lion
  require "yard"
  YARD::Rake::YardocTask.new do |t|
    t.options = ['--main', 'Readme.md', '--markup', 'markdown']
    t.options += ['--title', 'VirtualBox Ruby Library Documentation']
  end
end