|     Project | Information                                                     |
|------------:|:----------------------------------------------------------------|
| Domain:     | [Coding Dojo](http://codingdojo.com) (cd)                       |
| Topic:      | Ruby on Rails (ror) <br> Understanding Rails - Models (02model) |
| Assignment: | Blogs/Posts/Messages #1 (03blog1)                               |
| Repository: | cd-ror-02model-03blog1                                          |

~~~

---------------
#1: Start a new project 
---------------

rails new blog-post-message
cd blog-post-message

edit> Gemfile
  gem 'bcrypt', '~> 3.1.7'    # Using bcrypt (3.1.7)
  gem 'foundation-rails'      # Using foundation-rails (5.4.0.0)
  gem 'hirb'                  # Using hirb (0.7.2)
bundle install

---------------
#2: Create appropriate models/tables using "rails generate model", "rake db:create", and "rake db:migrate"
---------------

rails generate model Blog name:string description:text
rails generate model Post title:string content:text blog:references
rails generate model Message author:string message:text post:references


edit> blog.rb
  - add: has_many :posts
  - add: has_many :messages, through: :posts

edit> post.rb
  - add: has_many :messages

edit> message.rb
  - NA

rake db:create
rake db:migrate

---------------
#3: Implement the following validations
---------------

---------------
#3.1: Require the presence of name and description for the blog
---------------

edit> blog.rb
class Blog < ActiveRecord::Base
    has_many :posts
    has_many :messages, through: :posts

    validates :name, :description, presence: true
end


---------------
#3.2: Require the presence of title and content for the posts, require the title to be at least 7 characters long
---------------

edit> Post
class Post < ActiveRecord::Base
  belongs_to :blog
  has_many :messages

  validates :title, :content, presence: true
  validates :title, :length => { :minimum => 7 }
end

---------------
#3.3: Require author and message for the messages. Require the message to be at least 15 characters long.
---------------

edit> message.rb
class Message < ActiveRecord::Base
  belongs_to :post

  validates :author, :message, presence: true
  validates :message, :length => { :minimum => 15 }
end

---------------
#3.4: Reload model
---------------
rails console 
Hirb.enable()

---------------
#4.1: Create 5 new blogs
---------------

Blog.create(:name => "Benjamin", :description => "There are seven days in each week.")
Blog.create(:name => "Tom", :description => "The ground under the building is unstable.")
Blog.create(:name => "Bob", :description => "It is good to know what you don't what.")
Blog.create(:name => "Carol", :description => "The plans for the day are set in stone.")
Blog.create(:name => "Victoria", :description => "Take the back door to get to the swimmimg pool.")

+----+----------+-------------------------------------------------+-------------------------+-------------------------+
| id | name     | description                                     | created_at              | updated_at              |
+----+----------+-------------------------------------------------+-------------------------+-------------------------+
| 1  | Benjamin | There are seven days in each week.              | 2014-06-05 15:54:26 UTC | 2014-06-05 15:54:26 UTC |
| 2  | Tom      | The ground under the building is unstable.      | 2014-06-05 15:56:21 UTC | 2014-06-05 15:56:21 UTC |
| 3  | Bob      | It is good to know what you don't what.         | 2014-06-05 15:57:05 UTC | 2014-06-05 15:57:05 UTC |
| 4  | Carol    | The plans for the day are set in stone.         | 2014-06-05 15:58:38 UTC | 2014-06-05 15:58:38 UTC |
| 5  | Victoria | Take the back door to get to the swimmimg pool. | 2014-06-05 16:01:14 UTC | 2014-06-05 16:01:14 UTC |
+----+----------+-------------------------------------------------+-------------------------+-------------------------+

---------------
#4.2: Create several posts for each blog
---------------

Post.create( :blog_id => 1, :title => "Blog 1 Post 1 Title", :content => "Blog 1 Post 1 Content")
Post.create( :blog_id => 1, :title => "Blog 1 Post 2 Title", :content => "Blog 1 Post 2 Content")
Post.create( :blog_id => 1, :title => "Blog 1 Post 3 Title", :content => "Blog 1 Post 3 Content")
Post.create( :blog_id => 1, :title => "Blog 1 Post 4 Title", :content => "Blog 1 Post 4 Content")
Post.create( :blog_id => 1, :title => "Blog 1 Post 5 Title", :content => "Blog 1 Post 5 Content")

Post.create( :blog_id => 2, :title => "Blog 2 Post 1 Title", :content => "Blog 2 Post 1 Content")
Post.create( :blog_id => 2, :title => "Blog 2 Post 2 Title", :content => "Blog 2 Post 2 Content")
Post.create( :blog_id => 2, :title => "Blog 2 Post 3 Title", :content => "Blog 2 Post 3 Content")
Post.create( :blog_id => 2, :title => "Blog 2 Post 4 Title", :content => "Blog 2 Post 4 Content")
Post.create( :blog_id => 2, :title => "Blog 2 Post 5 Title", :content => "Blog 2 Post 5 Content")

Post.create( :blog_id => 3, :title => "Blog 3 Post 1 Title", :content => "Blog 3 Post 1 Content")
Post.create( :blog_id => 3, :title => "Blog 3 Post 2 Title", :content => "Blog 3 Post 2 Content")
Post.create( :blog_id => 3, :title => "Blog 3 Post 3 Title", :content => "Blog 3 Post 3 Content")
Post.create( :blog_id => 3, :title => "Blog 3 Post 4 Title", :content => "Blog 3 Post 4 Content")
Post.create( :blog_id => 3, :title => "Blog 3 Post 5 Title", :content => "Blog 3 Post 5 Content")

Post.create( :blog_id => 4, :title => "Blog 4 Post 1 Title", :content => "Blog 4 Post 1 Content")
Post.create( :blog_id => 4, :title => "Blog 4 Post 2 Title", :content => "Blog 4 Post 2 Content")
Post.create( :blog_id => 4, :title => "Blog 4 Post 3 Title", :content => "Blog 4 Post 3 Content")
Post.create( :blog_id => 4, :title => "Blog 4 Post 4 Title", :content => "Blog 4 Post 4 Content")
Post.create( :blog_id => 4, :title => "Blog 4 Post 5 Title", :content => "Blog 4 Post 5 Content")

Post.create( :blog_id => 5, :title => "Blog 5 Post 1 Title", :content => "Blog 5 Post 1 Content")
Post.create( :blog_id => 5, :title => "Blog 5 Post 2 Title", :content => "Blog 5 Post 2 Content")
Post.create( :blog_id => 5, :title => "Blog 5 Post 3 Title", :content => "Blog 5 Post 3 Content")
Post.create( :blog_id => 5, :title => "Blog 5 Post 4 Title", :content => "Blog 5 Post 4 Content")
Post.create( :blog_id => 5, :title => "Blog 5 Post 5 Title", :content => "Blog 5 Post 5 Content")

Post.all
+----+---------------------+-----------------------+---------+-------------------------+-------------------------+
| id | title               | content               | blog_id | created_at              | updated_at              |
+----+---------------------+-----------------------+---------+-------------------------+-------------------------+
| 1  | Blog 1 Post 1 Title | Blog 1 Post 1 Content | 1       | 2014-06-05 17:13:28 UTC | 2014-06-05 17:13:28 UTC |
| 2  | Blog 1 Post 2 Title | Blog 1 Post 2 Content | 1       | 2014-06-05 17:14:13 UTC | 2014-06-05 17:14:13 UTC |
| 3  | Blog 1 Post 3 Title | Blog 1 Post 3 Content | 1       | 2014-06-05 17:14:53 UTC | 2014-06-05 17:14:53 UTC |
| 4  | Blog 1 Post 4 Title | Blog 1 Post 4 Content | 1       | 2014-06-05 17:15:16 UTC | 2014-06-05 17:15:16 UTC |
| 5  | Blog 1 Post 5 Title | Blog 1 Post 5 Content | 1       | 2014-06-05 17:15:41 UTC | 2014-06-05 17:15:41 UTC |
| 6  | Blog 2 Post 1 Title | Blog 2 Post 1 Content | 2       | 2014-06-05 17:17:42 UTC | 2014-06-05 17:17:42 UTC |
| 7  | Blog 2 Post 2 Title | Blog 2 Post 2 Content | 2       | 2014-06-05 17:17:42 UTC | 2014-06-05 17:17:42 UTC |
| 8  | Blog 2 Post 3 Title | Blog 2 Post 3 Content | 2       | 2014-06-05 17:17:42 UTC | 2014-06-05 17:17:42 UTC |
| 9  | Blog 2 Post 4 Title | Blog 2 Post 4 Content | 2       | 2014-06-05 17:17:42 UTC | 2014-06-05 17:17:42 UTC |
| 10 | Blog 2 Post 5 Title | Blog 2 Post 5 Content | 2       | 2014-06-05 17:17:42 UTC | 2014-06-05 17:17:42 UTC |
| 11 | Blog 3 Post 1 Title | Blog 3 Post 1 Content | 3       | 2014-06-05 17:19:03 UTC | 2014-06-05 17:19:03 UTC |
| 12 | Blog 3 Post 2 Title | Blog 3 Post 2 Content | 3       | 2014-06-05 17:19:03 UTC | 2014-06-05 17:19:03 UTC |
| 13 | Blog 3 Post 3 Title | Blog 3 Post 3 Content | 3       | 2014-06-05 17:19:03 UTC | 2014-06-05 17:19:03 UTC |
| 14 | Blog 3 Post 4 Title | Blog 3 Post 4 Content | 3       | 2014-06-05 17:19:03 UTC | 2014-06-05 17:19:03 UTC |
| 15 | Blog 3 Post 5 Title | Blog 3 Post 5 Content | 3       | 2014-06-05 17:19:03 UTC | 2014-06-05 17:19:03 UTC |
| 16 | Blog 4 Post 1 Title | Blog 4 Post 1 Content | 4       | 2014-06-05 17:21:01 UTC | 2014-06-05 17:21:01 UTC |
| 17 | Blog 4 Post 2 Title | Blog 4 Post 2 Content | 4       | 2014-06-05 17:21:01 UTC | 2014-06-05 17:21:01 UTC |
| 18 | Blog 4 Post 3 Title | Blog 4 Post 3 Content | 4       | 2014-06-05 17:21:01 UTC | 2014-06-05 17:21:01 UTC |
| 19 | Blog 4 Post 4 Title | Blog 4 Post 4 Content | 4       | 2014-06-05 17:21:01 UTC | 2014-06-05 17:21:01 UTC |
| 20 | Blog 4 Post 5 Title | Blog 4 Post 5 Content | 4       | 2014-06-05 17:21:01 UTC | 2014-06-05 17:21:01 UTC |
| 21 | Blog 5 Post 1 Title | Blog 5 Post 1 Content | 5       | 2014-06-05 17:22:51 UTC | 2014-06-05 17:22:51 UTC |
| 22 | Blog 5 Post 2 Title | Blog 5 Post 2 Content | 5       | 2014-06-05 17:22:51 UTC | 2014-06-05 17:22:51 UTC |
| 23 | Blog 5 Post 3 Title | Blog 5 Post 3 Content | 5       | 2014-06-05 17:22:51 UTC | 2014-06-05 17:22:51 UTC |
| 24 | Blog 5 Post 4 Title | Blog 5 Post 4 Content | 5       | 2014-06-05 17:22:51 UTC | 2014-06-05 17:22:51 UTC |
| 25 | Blog 5 Post 5 Title | Blog 5 Post 5 Content | 5       | 2014-06-05 17:22:51 UTC | 2014-06-05 17:22:51 UTC |
+----+---------------------+-----------------------+---------+-------------------------+-------------------------+

---------------
#4.3: Create several messages for the first post
---------------

Message.create( :post_id => 1, :author => "Blog 1 Post 1 Message 1 author", :message => "Blog 1 Post 1 Message 1 message")
Message.create( :post_id => 1, :author => "Blog 1 Post 1 Message 2 author", :message => "Blog 1 Post 1 Message 2 message")
Message.create( :post_id => 1, :author => "Blog 1 Post 1 Message 3 author", :message => "Blog 1 Post 1 Message 3 message")
Message.create( :post_id => 1, :author => "Blog 1 Post 1 Message 4 author", :message => "Blog 1 Post 1 Message 4 message")
Message.create( :post_id => 1, :author => "Blog 1 Post 1 Message 5 author", :message => "Blog 1 Post 1 Message 5 message")

Message.all
+----+--------------------------------+---------------------------------+---------+-------------------------+-------------------------+
| id | author                         | message                         | post_id | created_at              | updated_at              |
+----+--------------------------------+---------------------------------+---------+-------------------------+-------------------------+
| 1  | Blog 1 Post 1 Message 1 author | Blog 1 Post 1 Message 1 message | 1       | 2014-06-05 17:31:13 UTC | 2014-06-05 17:31:13 UTC |
| 2  | Blog 1 Post 1 Message 2 author | Blog 1 Post 1 Message 2 message | 1       | 2014-06-05 17:32:47 UTC | 2014-06-05 17:32:47 UTC |
| 3  | Blog 1 Post 1 Message 3 author | Blog 1 Post 1 Message 3 message | 1       | 2014-06-05 17:32:47 UTC | 2014-06-05 17:32:47 UTC |
| 4  | Blog 1 Post 1 Message 4 author | Blog 1 Post 1 Message 4 message | 1       | 2014-06-05 17:32:47 UTC | 2014-06-05 17:32:47 UTC |
| 5  | Blog 1 Post 1 Message 5 author | Blog 1 Post 1 Message 5 message | 1       | 2014-06-05 17:32:47 UTC | 2014-06-05 17:32:47 UTC |
+----+--------------------------------+---------------------------------+---------+-------------------------+-------------------------+

---------------
#4.4: Know how to retrieve all posts for the first blog
---------------

Blog.first.posts
+----+---------------------+-----------------------+---------+-------------------------+-------------------------+
| id | title               | content               | blog_id | created_at              | updated_at              |
+----+---------------------+-----------------------+---------+-------------------------+-------------------------+
| 1  | Blog 1 Post 1 Title | Blog 1 Post 1 Content | 1       | 2014-06-05 17:13:28 UTC | 2014-06-05 17:13:28 UTC |
| 2  | Blog 1 Post 2 Title | Blog 1 Post 2 Content | 1       | 2014-06-05 17:14:13 UTC | 2014-06-05 17:14:13 UTC |
| 3  | Blog 1 Post 3 Title | Blog 1 Post 3 Content | 1       | 2014-06-05 17:14:53 UTC | 2014-06-05 17:14:53 UTC |
| 4  | Blog 1 Post 4 Title | Blog 1 Post 4 Content | 1       | 2014-06-05 17:15:16 UTC | 2014-06-05 17:15:16 UTC |
| 5  | Blog 1 Post 5 Title | Blog 1 Post 5 Content | 1       | 2014-06-05 17:15:41 UTC | 2014-06-05 17:15:41 UTC |
+----+---------------------+-----------------------+---------+-------------------------+-------------------------+

---------------
#4.5: know how to retrieve all posts for the last blog (sorted by title in the DESC order)
---------------

Blog.last.posts.order("title DESC")
+----+---------------------+-----------------------+---------+-------------------------+-------------------------+
| id | title               | content               | blog_id | created_at              | updated_at              |
+----+---------------------+-----------------------+---------+-------------------------+-------------------------+
| 25 | Blog 5 Post 5 Title | Blog 5 Post 5 Content | 5       | 2014-06-05 17:22:51 UTC | 2014-06-05 17:22:51 UTC |
| 24 | Blog 5 Post 4 Title | Blog 5 Post 4 Content | 5       | 2014-06-05 17:22:51 UTC | 2014-06-05 17:22:51 UTC |
| 23 | Blog 5 Post 3 Title | Blog 5 Post 3 Content | 5       | 2014-06-05 17:22:51 UTC | 2014-06-05 17:22:51 UTC |
| 22 | Blog 5 Post 2 Title | Blog 5 Post 2 Content | 5       | 2014-06-05 17:22:51 UTC | 2014-06-05 17:22:51 UTC |
| 21 | Blog 5 Post 1 Title | Blog 5 Post 1 Content | 5       | 2014-06-05 17:22:51 UTC | 2014-06-05 17:22:51 UTC |
+----+---------------------+-----------------------+---------+-------------------------+-------------------------+

---------------
#4.6: know how to update the first post's title
---------------

Post.first.update(:title => "Blog 1 Post 1 title UPDATED")
or
Post.first.update(title: "Blog 1 Post 1 title UPDATED")

Post.first
+----+-----------------------------+-----------------------+---------+-------------------------+-------------------------+
| id | title                       | content               | blog_id | created_at              | updated_at              |
+----+-----------------------------+-----------------------+---------+-------------------------+-------------------------+
| 1  | Blog 1 Post 1 title UPDATED | Blog 1 Post 1 Content | 1       | 2014-06-05 17:13:28 UTC | 2014-06-05 17:44:04 UTC |
+----+-----------------------------+-----------------------+---------+-------------------------+-------------------------+

---------------
#4.7: know how to delete the third post (have the model automatically delete all messages associated with the third post when you delete the third post)
---------------

First, will need to add the messages...
Message.create( :post_id => 3, :author => "Blog 1 Post 3 Message 1 author", :message => "Blog 1 Post 3 Message 1 message")
Message.create( :post_id => 3, :author => "Blog 1 Post 3 Message 2 author", :message => "Blog 1 Post 3 Message 2 message")
Message.create( :post_id => 3, :author => "Blog 1 Post 3 Message 3 author", :message => "Blog 1 Post 3 Message 3 message")
Message.create( :post_id => 3, :author => "Blog 1 Post 3 Message 4 author", :message => "Blog 1 Post 3 Message 4 message")
Message.create( :post_id => 3, :author => "Blog 1 Post 3 Message 5 author", :message => "Blog 1 Post 3 Message 5 message")

Post.find(3).messages
+----+--------------------------------+---------------------------------+---------+-------------------------+-------------------------+
| id | author                         | message                         | post_id | created_at              | updated_at              |
+----+--------------------------------+---------------------------------+---------+-------------------------+-------------------------+
| 6  | Blog 1 Post 3 Message 1 author | Blog 1 Post 3 Message 1 message | 3       | 2014-06-05 18:27:45 UTC | 2014-06-05 18:27:45 UTC |
| 7  | Blog 1 Post 3 Message 2 author | Blog 1 Post 3 Message 2 message | 3       | 2014-06-05 18:27:45 UTC | 2014-06-05 18:27:45 UTC |
| 8  | Blog 1 Post 3 Message 3 author | Blog 1 Post 3 Message 3 message | 3       | 2014-06-05 18:27:45 UTC | 2014-06-05 18:27:45 UTC |
| 9  | Blog 1 Post 3 Message 4 author | Blog 1 Post 3 Message 4 message | 3       | 2014-06-05 18:27:45 UTC | 2014-06-05 18:27:45 UTC |
| 10 | Blog 1 Post 3 Message 5 author | Blog 1 Post 3 Message 5 message | 3       | 2014-06-05 18:27:45 UTC | 2014-06-05 18:27:45 UTC |
+----+--------------------------------+---------------------------------+---------+-------------------------+-------------------------+

edit> post.rb
  - edit: has_many :messages, :dependent => :destroy 

reload!

Post.find(3).destroy

Post.find(3)
ActiveRecord::RecordNotFound: Couldn't find Post with id=3

Messages.all
+----+--------------------------------+---------------------------------+---------+-------------------------+-------------------------+
| id | author                         | message                         | post_id | created_at              | updated_at              |
+----+--------------------------------+---------------------------------+---------+-------------------------+-------------------------+
| 1  | Blog 1 Post 1 Message 1 author | Blog 1 Post 1 Message 1 message | 1       | 2014-06-05 17:31:13 UTC | 2014-06-05 17:31:13 UTC |
| 2  | Blog 1 Post 1 Message 2 author | Blog 1 Post 1 Message 2 message | 1       | 2014-06-05 17:32:47 UTC | 2014-06-05 17:32:47 UTC |
| 3  | Blog 1 Post 1 Message 3 author | Blog 1 Post 1 Message 3 message | 1       | 2014-06-05 17:32:47 UTC | 2014-06-05 17:32:47 UTC |
| 4  | Blog 1 Post 1 Message 4 author | Blog 1 Post 1 Message 4 message | 1       | 2014-06-05 17:32:47 UTC | 2014-06-05 17:32:47 UTC |
| 5  | Blog 1 Post 1 Message 5 author | Blog 1 Post 1 Message 5 message | 1       | 2014-06-05 17:32:47 UTC | 2014-06-05 17:32:47 UTC |
+----+--------------------------------+---------------------------------+---------+-------------------------+-------------------------+

---------------
#4.8: know how to retrieve all blogs
---------------

Blog.all

---------------
#4.9: know how to retrieve all blogs whose id is less than 5
---------------

Blog.where("id < 5")

---------------
#4.10: think of other potential information you may need for this application and get comfortable being able to pull information using the console
---------------

== Find all messages where Blog.name = "Benjamin"

Blog.find(1).messages
+----+--------------------------------+---------------------------------+---------+-------------------------+-------------------------+
| id | author                         | message                         | post_id | created_at              | updated_at              |
+----+--------------------------------+---------------------------------+---------+-------------------------+-------------------------+
| 1  | Blog 1 Post 1 Message 1 author | Blog 1 Post 1 Message 1 message | 1       | 2014-06-05 17:31:13 UTC | 2014-06-05 17:31:13 UTC |
| 2  | Blog 1 Post 1 Message 2 author | Blog 1 Post 1 Message 2 message | 1       | 2014-06-05 17:32:47 UTC | 2014-06-05 17:32:47 UTC |
| 3  | Blog 1 Post 1 Message 3 author | Blog 1 Post 1 Message 3 message | 1       | 2014-06-05 17:32:47 UTC | 2014-06-05 17:32:47 UTC |
| 4  | Blog 1 Post 1 Message 4 author | Blog 1 Post 1 Message 4 message | 1       | 2014-06-05 17:32:47 UTC | 2014-06-05 17:32:47 UTC |
| 5  | Blog 1 Post 1 Message 5 author | Blog 1 Post 1 Message 5 message | 1       | 2014-06-05 17:32:47 UTC | 2014-06-05 17:32:47 UTC |
+----+--------------------------------+---------------------------------+---------+-------------------------+-------------------------+

Blog.find_by(name: 'Benjamin').messages
+----+--------------------------------+---------------------------------+---------+-------------------------+-------------------------+
| id | author                         | message                         | post_id | created_at              | updated_at              |
+----+--------------------------------+---------------------------------+---------+-------------------------+-------------------------+
| 1  | Blog 1 Post 1 Message 1 author | Blog 1 Post 1 Message 1 message | 1       | 2014-06-05 17:31:13 UTC | 2014-06-05 17:31:13 UTC |
| 2  | Blog 1 Post 1 Message 2 author | Blog 1 Post 1 Message 2 message | 1       | 2014-06-05 17:32:47 UTC | 2014-06-05 17:32:47 UTC |
| 3  | Blog 1 Post 1 Message 3 author | Blog 1 Post 1 Message 3 message | 1       | 2014-06-05 17:32:47 UTC | 2014-06-05 17:32:47 UTC |
| 4  | Blog 1 Post 1 Message 4 author | Blog 1 Post 1 Message 4 message | 1       | 2014-06-05 17:32:47 UTC | 2014-06-05 17:32:47 UTC |
| 5  | Blog 1 Post 1 Message 5 author | Blog 1 Post 1 Message 5 message | 1       | 2014-06-05 17:32:47 UTC | 2014-06-05 17:32:47 UTC |
+----+--------------------------------+---------------------------------+---------+-------------------------+-------------------------+

Blog.where(name: 'Benjamin')
or 
Blog.where("name = 'Benjamin'")
+----+----------+------------------------------------+-------------------------+-------------------------+
| id | name     | description                        | created_at              | updated_at              |
+----+----------+------------------------------------+-------------------------+-------------------------+
| 1  | Benjamin | There are seven days in each week. | 2014-06-05 15:54:26 UTC | 2014-06-05 15:54:26 UTC |
+----+----------+------------------------------------+-------------------------+-------------------------+

???????????? NOT SURE HOW TO DO ONE BELOW?

Blog.where(name: 'Benjamin').messages
undefined method `messages' for #<ActiveRecord::Relation::ActiveRecord_Relation_Blog:0x007fc5de85cef0>

---------------
The End!
---------------

~~~
