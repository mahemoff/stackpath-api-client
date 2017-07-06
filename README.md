# Stackpath::Api::Client

An unofficial Ruby client for Stackpath API, only supports purging so far.

## Installation

Add this line to your application's Gemfile:

```ruby
gem 'stackpath-api-client'
```

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install stackpath-api-client

## API Access

1. [Login to Stackpath](https://stackpath.com) and open [the API management page](https://app.stackpath.com/account/api).
1. Create a new application and give it full permissions (full permissions are suggested because there may be a bug with Stackpath's fine-grain as at July 2017).
1. The API application page will show a consumer key, consumer secret, and a company alias . You'll need these for API calls as described in the next section.

## Usage

Using your consumer key, consumer secret, and company alias from the API application page, you can now run the following to purge resources. Note the default site ID is an ID of one of your sites [in your Stackpath sites list](https://app.stackpath.com/sites) under the "Site Name" column. You may omit this here and specify it in subsequent calls too.

```ruby
# require the library
require 'stackpath_api'

# setup your app's front-door to Stackpath
stackpath = StackpathApi::Client.new(
  consumer_key: 'your-consumer-key',
  consumer_secret: 'your-consumer-secret',
  company_alias: 'your-company-alias',
  default_site_id: 'exampledotcom'
)

# purge a file
stackpath.purge files: '/a-stale-resource'

# purge multiple files
stackpath.purge files: ['/stale-resource', /another-stale-resource']

# purge another of your sites
stackpath.purge site_id: 'exampledotorg', files: '/a-stale-resource'

# purge another of your companies
stackpath.purge company_alias: 'another-company-alias', files: '/a-stale-resource'
```

## Development

After checking out the repo, run bin/setup to install dependencies. Then, run rake spec to run the tests. You can also run bin/console for an interactive prompt that will allow you to experiment.

To install this gem onto your local machine, run bundle exec rake install. To release a new version, update the version number in version.rb, and then run bundle exec rake release, which will create a git tag for the version, push git commits and tags, and push the .gem file to rubygems.org.

## Contributing

Bug reports and pull requests are welcome on GitHub at https://github.com/Overbryd/stackpath-api-client.


## License

The gem is available as open source under the terms of the [MIT License](http://opensource.org/licenses/MIT).
