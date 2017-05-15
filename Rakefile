require 'bundler'
Bundler::GemHelper.install_tasks

require 'rspec/core/rake_task'
require 'spree/testing_support/common_rake'

RSpec::Core::RakeTask.new

task :default => :spec

desc 'Generates a dummy app for testing'
task :test_app do
  ENV['LIB_NAME'] = 'spree/auth'
  Rake::Task['common:test_app'].invoke("Spree::User")
end

Rake::Task[:release].tap do |task|
  task.clear
  task.instance_variable_set :@arg_names, nil
end

desc "Build and release v#{SpreeAuthDevise::VERSION} to Gemfury"
task :release => :build do
  sh "curl -F package=@pkg/spree_auth_devise-#{SpreeAuthDevise::VERSION}.gem https://#{ENV.fetch('GEMFURY_TOKEN')}@push.fury.io/#{ENV.fetch('GEMFURY_USERNAME')}/"
  sh "git tag v#{SpreeAuthDevise::VERSION} -m 'Release #{SpreeAuthDevise::VERSION}'"
  sh "git push origin v#{SpreeAuthDevise::VERSION}"
end
