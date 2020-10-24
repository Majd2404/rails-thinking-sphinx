
<h1> How to bring Sphinx into Rails, using Thinking Sphinx, to provide fast and flexible full-text search.</h1>





<h2>Installing Sphinx</h2>
Linux
Debian/Ubuntu
Install either python3-sphinx using apt-get:
+ apt-get install python3-sphinx
If it not already present, this will install Python for you.

<h2>Create new rails app</h2> 
+ rails new rails-thinking-sphinx -d mysql

The mysql2 gem was already included in the gemfile.
So, you should just add the <strong>Thinking Sphinx gem</strong> and run bundle install command:

+ gem 'thinking-sphinx', '3.1.4'
+ bundle install

<h3>Generate:</h3>

+ rails db:create
+ rails g scaffold article title:text content:text
+ rake db:migrate

<h3>Index:</h3>

let’s get the Sphinx index file in the app/indices directory (which you will have to create).
We will name the file article_index.rb and it will look like this:

ThinkingSphinx::Index.define :article, :with => :active_record do

  indexes title, :sortable => true
  indexes content
end

<h3>Run indexer with:</h3>
+ rake ts:index:
+ rake ts:start

