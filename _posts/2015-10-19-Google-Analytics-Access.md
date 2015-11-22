---
layout: post
tags:
- analytics
- gattica
- oauth2
- legato
---

Gattica no longer works with the Google API as it does not support OAuth2. I am therefore moving a project away from using the Gattica gem (for Google Analytics access from the site) to using the Legato gem instead (along with the oauth2 or google-oauth2-installed gem).

# oauth2 or google-oauth2-installed gem?

You now need to use the OAuth 2.0 protocol to interact with the Google API, which is why Gattica is no longer working and why we're all here. Legato does not do this directly, instead you need to do this yourself or use a gem.

The oauth2 gem is "a Ruby wrapper for the OAuth 2.0 specification" and is to be used "when your application needs access as the user of your application".

The google-oauth2-installed gem allows you to "Configure and authenticate to Google with OAuth2 as an installed application" and is to be used "when your application needs to authenticate to Google services, as opposed to your application's users".

## Get and manage an OAuth2 Token using google-oauth2-installed

> See [google-oauth2-installed readme](https://github.com/carnesmedia/google-oauth2-installed)

The [google-oauth2-installed setup instructions](https://github.com/carnesmedia/google-oauth2-installed) are good (see the "Setup" section) so I will not go into detail here, except to say that it is important select the "Other" application type just after the first (create project) step, as explained here:

1. Click "APIs & Auth" > "Credentials"

2. Click "Add Credentials" > "OAuth2 Client ID" and select "Other" as the application type

> The redirect URI is set to `urn:ietf:wg:oauth:2.0:oob` for you when you select this "Other" application type. You will get an `Error: redirect_uri_mismatch` or similar error when trying to use google-oauth2-installed with other Application types (that do not have the correct redirect URI)

## Get an OAuth2 Token using oauth2

You probably do not want to do this, you probably want to use the google-oauth2-installed gem instead and skip this section. See above for details.

> See [Getting an OAuth2 Token instructins](https://github.com/tpitale/legato/wiki/OAuth2-and-Google) with some help from the [OAuth2 RubyDoc](http://www.rubydoc.info/gems/oauth2/1.0.0)

1. Go to the [Google API Console](https://code.google.com/apis/console/) and create a new 'Web Application' project

    Use the drop down list at the top of the page - `Create a project`

2. Turn on Google Analytics access

    Use the left menu: `APIs & Auth` > `APIs`, click on `Analytics API`, click on `Enable API`

3. Create an OAuth

    select `credentials` under `APIs & Auth` in the left menu, click `Add Credentials` > `OAuth2 Client ID`

    3.1 Add details, including `http://localhost` as an `Authorized redirect URI`

    3.2 Make a note of the `Client ID` and `Client secret` provided

4. Add the `oauth2` gem to your Rail application

    Add `gem 'oauth2'` to Gemfile and run `bundle` to install

5. Add details as Environment Variables to Application.yml file and restart the server

    ``` ruby
    LEGATO_OAUTH_CLIENT_ID: 'id_from_above'
    LEGATO_OAUTH_SECRET_KEY: 'key_from_above'
    ```

6. Get the 'Auth Code' token from Google

    6.1 In the console (in IRB) require 'oauth2'

    ``` ruby
    bundle exec rails c
    require 'oauth2'
    ```

    6.2 Create Auth Client Object

    ``` ruby
    client = OAuth2::Client.new(
      ENV['LEGATO_OAUTH_CLIENT_ID'],
      ENV['LEGATO_OAUTH_SECRET_KEY'], {
        :authorize_url => 'https://accounts.google.com/o/oauth2/auth',
        :token_url => 'https://accounts.google.com/o/oauth2/token'
      }
    )
    ```

    6.3 Create the Auth URL to get the URL string.

    ``` ruby
    client.auth_code.authorize_url({
      :scope => 'https://www.googleapis.com/auth/analytics.readonly',
      :redirect_uri => 'http://localhost',
      :access_type => 'offline'
    })
    ```

    6.3.1 Copy the resulting URL string into a browser and follow the prompts to get a new token in the form `http://localhost/?code=your_new_auth_code`

      > My token always started with `4/`

7. Add the token as Environment Variables to Application.yml file and restart the server

    ``` ruby
    LEGATO_OAUTH_AUTH_CODE: '4/wc0xtN2B32-mg7AyV8qUK8-vxGyzyGlU1qrx6sQDY54#'
    ```

8. Add something like this to a file such as `lib/analytics.rb`

    ``` ruby
    def get_token
      # Option 1
      client = OAuth2::Client.new(
        ENV['LEGATO_OAUTH_CLIENT_ID'],
        ENV['LEGATO_OAUTH_SECRET_KEY'], {
          :authorize_url =>
            'https://accounts.google.com/o/oauth2/auth',
          :token_url =>
            'https://accounts.google.com/o/oauth2/token'
        }
      )
      client.auth_code.authorize_url({
        :scope =>
          'https://www.googleapis.com/auth/analytics.readonly',
        :redirect_uri => 'http://localhost',
        :access_type => 'offline'
      })
      access_token =
        client.auth_code.get_token(
          ENV['LEGATO_OAUTH_AUTH_CODE'],
          :redirect_uri => 'http://localhost'
        )

      # Option 2
      # token = ENV['LEGATO_OAUTH_AUTH_CODE']
      # client = OAuth2::Client.new(
      #   ENV['LEGATO_OAUTH_CLIENT_ID'],
      #   ENV['LEGATO_OAUTH_SECRET_KEY'], {
      #     :authorize_url =>
      #       'https://accounts.google.com/o/oauth2/auth',
      #     :token_url => 'https://accounts.google.com/o/oauth2/token'
      #   }
      # )
      # client.auth_code.authorize_url({
      #   :scope =>
      #     'https://www.googleapis.com/auth/analytics.readonly',
      #   :redirect_uri => 'http://localhost',
      #   :access_type => 'offline'
      # })
      # access_token = OAuth2::AccessToken.from_hash client,
      #   {:access_token => token}
    end
    ```

# Setup Legato

> See [Legato Readme](https://github.com/tpitale/legato)

1. Add `gem 'legato'` to your Gemfile and run `bundle`

# Usage

If you have read beyond the "Setup" section of the [google-oauth2-installed setup instructions](https://github.com/carnesmedia/google-oauth2-installed) (i.e. if you have read the "Usage" section) you may already be in a position to access and use your Analytics data. Here is what I did:

1. Install google-oauth2-installed and set it up as shown above

2. Install legato

3. In `lib/analytics.rb` or somewhere:

    ```
    def sales_by_source
      get_google_analytics_profile unless @profile
      to_hash(Analytics::NewUsers.results(
          @profile,
          start_date: @start_date.strftime('%Y-%m-%d'),
          end_date: @end_date.strftime('%Y-%m-%d')
        ).to_a
      )
    end

    private

    def get_google_analytics_profile
      user = Legato::User.new GoogleOauth2Installed.access_token
      @profile = profile = user.profiles.first
    end

    def to_hash(array)
    result = {}
    referrer_count = 0 # new users from referring websites
    array.to_a.each do |row|
      # Group referring websites
      if row.source =~ /^([a-zA-Z0-9-]+\.[a-zA-Z0-9-]+)+$/
        source = 'referrer'
        new_users = referrer_count += row.newUsers.to_i
      else
        source = row.source
        new_users = row.newUsers
      end
      
      result[source] = new_users
    end
    result
  end
    ```

4. In `lib/analytics/new_users.rb`:

    ```
    class Analytics::NewUsers
      extend Legato::Model
      metrics :newUsers
      dimensions :source
      filter(:source) {|s| matches(:s, source)} # not used in this example
    end
    ```
