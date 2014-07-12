source 'https://rubygems.org'

gem 'rake'
gem 'kitchen-digitalocean'

group :test, :integration do
  gem 'berkshelf'#, '~> 2.0.14'
end

group :test do
  gem 'chefspec', '~> 3.4.0'
  gem 'elecksee', '~> 1.0.20'
  gem 'etcd', '~> 0.2.3'
  gem 'foodcritic', '~> 3.0.3'
  gem 'rubocop', '~> 0.20.0'
end

group :integration do
  gem 'busser-serverspec'#, '~> 0.2.6'
  gem 'kitchen-vagrant'#, '~> 0.13'
  gem 'test-kitchen'#, '~> 1.1'
end
