```
    ____        __             ____________     ____        __              __      
   / __ \__  __/ /_  __  __   /_  __/ ____/    / __ \__  __/ /_____  __  __/ /______
  / /_/ / / / / __ \/ / / /    / / / /_       / / / / / / / __/ __ \/ / / / __/ ___/
 / _, _/ /_/ / /_/ / /_/ /    / / / __/      / /_/ / /_/ / /_/ /_/ / /_/ / /_(__  ) 
/_/ |_|\__,_/_.___/\__, /    /_/ /_/         \____/\__,_/\__/ .___/\__,_/\__/____/  
                  /____/                                   /_/                      
```
[![Build Status](https://travis-ci.org/jae2/ruby-tfoutputs.svg?branch=master)](https://travis-ci.org/jae2/ruby-tfoutputs)   [![Gem Version](https://badge.fury.io/rb/tfoutputs.svg)](https://badge.fury.io/rb/tfoutputs)


# Ruby TF Outputs

This gem is a ruby interface to access your terraform outputs.

## Installation

Add this line to your application's Gemfile:

```ruby
gem 'tfoutputs'
```

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install tfoutputs




## Pre-requistes

Ruby >= 2.2.2
Your terraform state file also needs to be generated by terraform > 0.7.0  there are currently no plans to support terraform < 0.7.0



## Usage

Require the gem:

```ruby
require 'tfoutputs'
```

tfoutputs uses 'backends' as a means of retrieving the state files. A backend is a place where the terraform state file lives. Currently only two are supported: s3 and file.

Setting up an s3 backend:

```ruby
config = {:backend => 's3',:options => {:bucket_name => 'my-bucket-name-goes-here',
           :bucket_region => 'eu-west-1', :bucket_key => 'terraform.tfstate' }
         }
state_reader = TfOutputs.configure(config)
puts(state_reader.my_output_name)
         
S3 backends also have the following optional parameters:

**profile** - The AWS Credential profile to use.

Setting up a file backend:
```ruby
config = {:backend => 'file', :options => { :file_path => '/path/to/state/file/terraform.tfstate' } }
state_reader = TfOutputs.configure(config)
puts(state_reader.my_output_name)

```


Using multiple states with multiple backends:

```ruby
config = [{:backend => 's3',:options => {:bucket_name => 'my-bucket-name-goes-here',
           :bucket_region => 'eu-west-1', :bucket_key => 'terraform.tfstate' }
         },
          {:backend => 'file', :options => { :file_path => '/path/to/state/file/terraform.tfstate' } }
        ]
state_reader = TfOutputs.configure(config)
puts(state_reader.my_output_name)
```

[Blog post on tfoutputs](https://jaetech.org/terraform-outputs-in-ruby/)


## Contributing

Bug reports and pull requests are welcome on GitHub at https://github.com/jae2/ruby-tfoutput. This project is intended to be a safe, welcoming space for collaboration, and contributors are expected to adhere to the [Contributor Covenant](http://contributor-covenant.org) code of conduct.


## License

The gem is available as open source under the terms of the [MIT License](http://opensource.org/licenses/MIT).

