Review MVC and REST

ROUTES SECTION
Rewrite mentors/girls to use the collection do block
```ruby
    # get 'mentors/girls', to: 'mentors#girls'
    collection do      
      get :girls      
      get :admins    
    end
```
View rake routes

Show resources :mentors but written out explicitly
```ruby
      get 'mentors', to: 'mentors#index'
      get 'mentors/:id', to: 'mentors#show'
      get 'mentors/new', to: 'mentors#new'
      post 'mentors', to: 'mentors#create'
      get 'mentors/:id/edit', to: 'mentors#edit'
      patch 'mentors/:id', to: 'mentors#update'
      put 'mentors/:id', to: 'mentors#update'
      delete 'mentors/:id', to: 'mentors#destroy'
```
Add a member block
```ruby
    member do      
      patch :inactivate    
    end
```
Create an export for mentors
```ruby
    collection do      
      get :girls      
      get :admins      
      post :export    
    end
```
Create another resource with all restful routes
```ruby
    resources :mentees
```
Remove the destroy mentee route
```ruby
    resources :mentees, except: [:destroy]
```
Default to mentees instead of mentors
```ruby
    root 'mentees#index'
```
show class the error when going to root

uninitialized constant MenteesController
Manually create - mentees_controller.rb
```ruby
    class MenteesController < ApplicationController
    end
```
show error - action could not be found

Add action
```ruby
class MenteesController < ApplicationController

  def index
  end

end
```
show error - missing template

create mentees view folder
create mentees index view file
explain file extension .html.erb

link_to helper section

add url to link
add plan text link
show rake routes | grep mentor
mentors GET    /mentors(.:format)                mentors#index
explain on left side is a variable; mentors_path, mentors_url

show difference between variables
```
<a href="/mentors">Go to mentors page</a>
<a href="<%= mentors_path %>">Go to mentors page</a>
<a href="<%= mentors_url %>">Go to mentors page</a>
<%= link_to 'Go to mentors page', mentors_path, id: 'my_mentor_link'  %>
```
show how to edit link_to
```ruby
<br><%= link_to 'Go to mentors page', mentors_path, id: 'my_mentor_link', style: "font-size:20px"  %>
<br><br><%= link_to 'Go to mentors page', mentors_path, id: 'my_mentor_link', class: "btn"  %>
```
show documentation
https://api.rubyonrails.org/v5.2.1/classes/ActionView/Helpers/UrlHelper.html#method-i-link_to

Add a member route variable
show rake routes | grep mentor
add link
```ruby
<br><%= link_to 'Favorite Mentor', mentor_path(999), style: "color:white"  %>
```
edit the mentor/show.html.erb
This is my mentor show page

Go to link now through browser
Add instance variable
```ruby
  def show
    @mentor_name = "Steve Jobs"
  end
```
This is my mentor show page
```ruby
<br>Their name is <%= @mentor_name %>
```
template section
show how it defaults to action_name
```ruby
  def show
    @mentor_name = "Steve Jobs"
    render 'show'
  end  
```
and defaults to format
```ruby
def show
  @mentor_name = "Steve Jobs"
  render 'show.html.erb'
end
```
We can render whatever template file we want
```ruby
  def show
    @mentor_name = "Steve Jobs"
    render 'mentees/index.html.erb'
  end
```
view in browser
remove line
