source 'https://rubygems.org'

gemspec

# We need a newish Rake since Active Job sets its test tasks' descriptions.
gem 'rake', '>= 10.3'

# This needs to be with require false as it is
# loaded after loading the test library to
# ensure correct loading order
gem 'mocha', '~> 0.14', require: false


# AS
gem 'dalli', '>= 2.2.1'

# ActiveJob
group :job do
  gem 'resque', require: false
  gem 'resque-scheduler', require: false
  gem 'sidekiq', require: false
  gem 'sucker_punch', require: false
  gem 'delayed_job', require: false
  gem 'queue_classic', "< 3.0.0", require: false, platforms: :ruby
  gem 'sneakers', '0.1.1.pre', require: false
  gem 'que', require: false
  gem 'backburner', require: false
  gem 'qu-rails', github: "bkeepers/qu", branch: "master", require: false
  gem 'qu-redis', require: false
  # gem 'delayed_job_active_record', require: false
  gem 'sequel', require: false
end

# Add your own local bundler stuff
local_gemfile = File.dirname(__FILE__) + "/.Gemfile"
instance_eval File.read local_gemfile if File.exist? local_gemfile

group :test do
  # FIX: Our test suite isn't ready to run in random order yet
  gem 'minitest', '< 5.3.4'

  platforms :mri_19 do
    gem 'ruby-prof', '~> 0.11.2'
  end

  platforms :mri_21, :mri_22 do
    gem 'stackprof'
  end

  # platforms :mri do
  #   gem 'byebug'
  # end

  gem 'benchmark-ips'
end

platforms :ruby do
  gem 'nokogiri', '>= 1.4.5'

  # Needed for compiling the ActionDispatch::Journey parser
  gem 'racc', '>=1.4.6', require: false

  # AR
  gem 'sqlite3', '~> 1.3.6'

  group :db do
    gem 'pg', '>= 0.15.0'
    gem 'mysql', '>= 2.9.0'
    gem 'mysql2', '>= 0.3.13'
  end
end

platforms :jruby do
  gem 'json'
  if ENV['AR_JDBC']
    gem 'activerecord-jdbcsqlite3-adapter', github: 'jruby/activerecord-jdbc-adapter', branch: 'master'
    group :db do
      gem 'activerecord-jdbcmysql-adapter', github: 'jruby/activerecord-jdbc-adapter', branch: 'master'
      gem 'activerecord-jdbcpostgresql-adapter', github: 'jruby/activerecord-jdbc-adapter', branch: 'master'
    end
  else
    gem 'activerecord-jdbcsqlite3-adapter', '>= 1.3.0'
    group :db do
      gem 'activerecord-jdbcmysql-adapter', '>= 1.3.0'
      gem 'activerecord-jdbcpostgresql-adapter', '>= 1.3.0'
    end
  end
end

platforms :rbx do
  # The rubysl-yaml gem doesn't ship with Psych by default
  # as it needs libyaml that isn't always available.
  gem 'psych', '~> 2.0'
end

# gems that are necessary for ActiveRecord tests with Oracle database
if ENV['ORACLE_ENHANCED']
  platforms :ruby do
    gem 'ruby-oci8', '~> 2.1'
  end
  gem 'activerecord-oracle_enhanced-adapter', github: 'rsim/oracle-enhanced', branch: 'master'
end

# A gem necessary for ActiveRecord tests with IBM DB
gem 'ibm_db' if ENV['IBM_DB']
