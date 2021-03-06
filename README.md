# ActionDispatch::GzStatic

ActionDispatch::GzStatic is a derivative of ActionDispatch::Static, that has
been modified to serve the .gz files that are created by the Rails asset
precompiler.

If you are using Rails to serve static assets in production, and
you are using the asset precompiler, then it is probably a good idea to use this
gem. If you are running on Heroku's Cedar stack, this includes you.

ActionDispatch::GzStatic is a better solution that using Rack::Deflater on your
static assets, because this has the undesirable side effect of recompressing
assets that are already compressed, such as images. It is still a good idea to
use Rack::Deflater for your app responses, but it should be positioned after
Rack::GzStatic in the middleware stack.

## Installation

Add this line to your application's Gemfile:

    gem 'action_dispatch-gz_static'

Add this to application.rb:

    # The railtie initializer will look for ActionDispatch::Static, and swap it
    # with ActionDispatch::GzStatic
    config.serve_static_assets = true

    # This isn't required, but is generally a good idea.
    config.static_cache_control = "public, max-age=#{1.month.to_i}"
