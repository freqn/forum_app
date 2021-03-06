# Database Structure

**User** - Devise
* email
* password

```ruby
has_many :forum_threads
has_many :forum_posts
```

**ForumThread**

* user_id:integer
* subject:string

```ruby
belongs_to :user
```

**ForumPost**

* forum_thread_id:integer
* user_id:integer
* body:text

```ruby
belongs_to :forum_thread
belongs_to :user
```

--------------------------------

# Devise Notes

**Use `gem 'devise', github: 'plataformatec/devise', branch: 'lm-rails-4-2'` in your Gemfile since Devise is not yet fully compatible with 4.2b1**

Some setup you must do manually if you haven't yet:

  1. Ensure you have defined default url options in your environments files. Here
     is an example of default_url_options appropriate for a development environment
     in config/environments/development.rb:

       config.action_mailer.default_url_options = { host: 'localhost', port: 3000 }

     In production, :host should be set to the actual host of your application.

  2. Ensure you have defined root_url to *something* in your config/routes.rb.
     For example:

       root to: "home#index"

  3. Ensure you have flash messages in app/views/layouts/application.html.erb.
     For example:

       <p class="notice"><%= notice %></p>
       <p class="alert"><%= alert %></p>

  4. If you are deploying on Heroku with Rails 3.2 only, you may want to set:

       config.assets.initialize_on_precompile = false

     On config/application.rb forcing your application to not access the DB
     or load models when precompiling your assets.

  5. You can copy Devise views (for customization) to your app by running:

       rails g devise:views
