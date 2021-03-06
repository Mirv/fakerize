# Fakerize

Replace all personal data from your models with faker-generated ones.

## Installation

Add this line to your application's Gemfile:

```ruby
gem 'fakerize'
```

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install fakerize

## Usage

Create a subclass of Faker::Model and specify columns you want to fakerize.
You need to override `default_config` method, for example:

    class Fakerize::Company < Fakerize::Model
      private
    
      def default_config
        {
          name: ->() { Faker::Company.name },
          address: ->() { Faker::Address.street_address }
        }
      end
    end

    # Replace values of `name` and `address` company columns with random ones:
    Company.find_each do |company|        
      Fakerize::Company.new(company).perform
    end

You can also specify methods to be called before save (to remove a carrierwave logo in this case):

    class Fakerize::Company < Fakerize::Model
      private
    
      def before_save_methods
        [:remove_logo!]
      end 
    end 


## Development

After checking out the repo, run `bin/setup` to install dependencies. Then, run `rake spec` to run the tests. You can also run `bin/console` for an interactive prompt that will allow you to experiment.

To install this gem onto your local machine, run `bundle exec rake install`. To release a new version, update the version number in `version.rb`, and then run `bundle exec rake release`, which will create a git tag for the version, push git commits and tags, and push the `.gem` file to [rubygems.org](https://rubygems.org).

## Contributing

Bug reports and pull requests are welcome on GitHub at https://github.com/kollegorna/fakerize. This project is intended to be a safe, welcoming space for collaboration, and contributors are expected to adhere to the [Contributor Covenant](http://contributor-covenant.org) code of conduct.

## License

The gem is available as open source under the terms of the [MIT License](https://opensource.org/licenses/MIT).

## Code of Conduct

Everyone interacting in the Fakerize project’s codebases, issue trackers, chat rooms and mailing lists is expected to follow the [code of conduct](https://github.com/[USERNAME]/fakerize/blob/master/CODE_OF_CONDUCT.md).
