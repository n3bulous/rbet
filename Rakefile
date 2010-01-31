require 'rubygems'
require 'rake/gempackagetask'
require 'rake/testtask'
require 'rake/rdoctask'
require 'lib/rbet/version'

spec = Gem::Specification.new do |s|
  s.name             = 'rbet'
  s.version          = RBET::Version.to_s
  s.has_rdoc         = true
  s.extra_rdoc_files = %w(README.rdoc)
  s.rdoc_options     = %w(--main README.rdoc)
  s.summary          = "A ruby wrapper for the Exact Target API"
  s.author           = 'See Contributing Section'
  s.email            = 'kevin@conceptsahead.com'
  s.homepage         = 'http://github.com/n3bulous/rbet'
  s.files            = %w(README.rdoc Rakefile) + Dir.glob("{lib,test}/**/*")
  # s.executables    = ['rbet']

  # s.add_dependency('gem_name', '~> 0.0.1')
end

Rake::GemPackageTask.new(spec) do |pkg|
  pkg.gem_spec = spec
end

Rake::TestTask.new do |t|
  t.libs << 'test'
  t.test_files = FileList["test/*_test.rb"]
  t.verbose = true
end

begin
  require 'rcov/rcovtask'

  Rcov::RcovTask.new(:coverage) do |t|
    t.libs       = ['test']
    t.test_files = FileList["test/*_test.rb"]
    t.verbose    = true
    t.rcov_opts  = ['--text-report', "-x #{Gem.path}", '-x /Library/Ruby', '-x /usr/lib/ruby']
  end

  task :default => :coverage

rescue LoadError
  warn "\n**** Install rcov (sudo gem install relevance-rcov) to get coverage stats ****\n"
  task :default => :test
end


desc 'Generate the gemspec to serve this Gem from Github'
task :github do
  file = File.dirname(__FILE__) + "/#{spec.name}.gemspec"
  File.open(file, 'w') {|f| f << spec.to_ruby }
  puts "Created gemspec: #{file}"
end