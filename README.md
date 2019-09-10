# course_WEEK_8

New group project - https://github.com/dtrts/acebook-ConnectU

Personal learning of Rails

- Getting started: 

There are a number of autocreated files : 

File/Folder	Purpose
app/	        Contains the controllers, models, views, helpers, mailers, channels, jobs, and assets for your application. You'll focus on this folder for the remainder of this guide.
bin/	        Contains the rails script that starts your app and can contain other scripts you use to setup, update, deploy, or run your application.
config/	        Configure your application's routes, database, and more. This is covered in more detail in Configuring Rails Applications.
config.ru	    Rack configuration for Rack based servers used to start the application. For more information about Rack, see the Rack website.
db/	            Contains your current database schema, as well as the database migrations.
Gemfile
Gemfile.lock	These files allow you to specify what gem dependencies are needed for your Rails application. These files are used by the Bundler gem. For more information about Bundler, see the Bundler website.
lib/	        Extended modules for your application.
log/	        Application log files.
package.json	This file allows you to specify what npm dependencies are needed for your Rails application. This file is used by Yarn. For more information about Yarn, see the Yarn website.
public/	        The only folder seen by the world as-is. Contains static files and compiled assets.
Rakefile	    This file locates and loads tasks that can be run from the command line. The task definitions are defined throughout the components of Rails. Rather than changing Rakefile, you should add your own tasks by adding files to the lib/tasks directory of your application.
README.md	    This is a brief instruction manual for your application. You should edit this file to tell others what your application does, how to set it up, and so on.
storage/	    Active Storage files for Disk Service. This is covered in Active Storage Overview.
test/	        Unit tests, fixtures, and other test apparatus. These are covered in Testing Rails Applications.
tmp/	        Temporary files (like cache and pid files).
vendor/	        A place for all third-party code. In a typical Rails application this includes vendored gems.
.gitignore	    This file tells git which files (or patterns) it should ignore. See GitHub - Ignoring files for more info about ignoring files.
.ruby-version	This file contains the default Ruby version.

Say - Hello Rails

- rails can generate controllers and views for certain requests and applications without doing it all from scratch. 

example :
```
rails generate controller Welcome index
```

Most important of these are of course the controller, located at app/controllers/welcome_controller.rb and the view, located at app/views/welcome/index.html.erb.

Open the app/views/welcome/index.html.erb file in your text editor.

```root 'welcome#index' ``` tells Rails to map requests to the root of the application to the welcome controller's index action and get 'welcome/index' tells Rails to map requests to http://localhost:3000/welcome/index to the welcome controller's index action.

Rails can generate controllers which once run on the server will tell the next steps to display files.


$ rails generate model Article title:string text:text

this part makes the article model with a title and text attribute. 

Once created the model we need to display it with the correct params 

```
  def create
    @article = Article.new(article_params)

    @article.save
    redirect_to @article
  end
  private

  def article_params
    params.require(:article).permit(:title, :text)
  end
```

Once that is done, the show from rails routes needs to be displayed, which is created in a file with a root - app/views/articles/show.html.erb

finally, we need to add links to navigate between pages. These are coded like example:
``` 
<%= link_to 'My Blog', controller: 'articles' %>
```

To validate the title we add to the article model -- 

```

class Article < ApplicationRecord
  validates :title, presence: true,
                    length: { minimum: 5 }
end

```

With this step we integrate the render method into the controller. The render method is used so that the @article object is passed back to the new template when it is rendered. If you reload http://localhost:3000/articles/new and try to save an article without a title, Rails will send you back to the form, but that's not very useful. 

we should add errors in the new articles pages. 

```
<% if @article.errors.any? %>
    <div id="error_explanation">
      <h2>
        <%= pluralize(@article.errors.count, "error") %> prohibited
        this article from being saved:
      </h2>
      <ul>
        <% @article.errors.full_messages.each do |msg| %>
          <li><%= msg %></li>
        <% end %>
      </ul>
    </div>
  <% end %>
```




