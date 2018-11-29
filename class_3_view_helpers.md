**Templates**

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


**Formats**
add show action to mentees
```ruby
  def show
  end
```  
Go to an example of a show
http://localhost:3000/mentees/1

Add view file
show.html.erb

Show it works now
http://localhost:3000/mentees/1

Show different format
http://localhost:3000/mentees/1.xml

Force template file extension
```ruby
  def show
    render 'show.html.erb'
  end
```
Allow for both extensions to work (remove render line)

create show.xml.erb file
add instance variable
```ruby
  <mentee>
    <%= @mentee %>
  </mentee>
```
 **Partials**
create that a partial filename must have  "_" at the start of the name
_mentee_info.html.erb
```ruby
  <tr>
   <td><%= @first_name %></td>
   <td><%= @last_name %></td>
   <td>USA</td>
   <td><%= @mentor_name %></td>
 </tr>
```
In mentee/index.html
add a render partial
```ruby
<table>
  <tr>
    <th>First Name</th>
    <th>Last Name</th>
    <th>Country</th>
    <th>Mentor Name</th>
  </tr>
  <br> <%= render partial: 'mentee_info' %>

</table>
```
Go to index URL - show how there are blank values
now add instance variables
```ruby
class MenteesController < ApplicationController
  def index
    @first_name = 'John'
    @last_name = 'Smith'
    @mentee = "James"
  end
```
Reuse partial
```ruby
 <%= render partial: 'mentee_info' %>
 <%= render partial: 'mentee_info' %>
```
Show local (var_name) vs instance variables (@var_name)

Show difference between instance and local - talk about <%= vs <%
```ruby
<table>
  <tr>
    <th>First Name</th>
    <th>Last Name</th>
    <th>Country</th>
    <th>Mentor Name</th>
  </tr>
  <br>

  <% mentor_name = 'bill' %>
  <% @mentor_name = 'Billy' %>
  <br> <%= render partial: 'mentee_info' %>

  <% @mentor_name = 'Jack' %>
  <br> <%= render partial: 'mentee_info' %>
</table>
```
Add another column to _mentee_info.html
```ruby
    <th>Mentor</th>
  </tr>
  <tr>
   <td><%= @first_name %></td>
   <td><%= @last_name %></td>
   <td>USA</td>
   <td><%= @mentor_name %></td>
 </tr>
</table>
```
show how you can use both those local variables but only in the index file not partial
```ruby
<%= mentor_name  %>
<%= @mentor_name %>
```

**if statement**

Add to mentees/show
explain params keyword and how its a hash
```ruby
<br><br>
<% if params[:id] == '1' %>
  You are our very first mentor
<% else  %>
  Welcome to the group!
<% end %>
```
add else if
```ruby
<br><br>
<% if params[:id] == '1' %>
  You are our very first mentor
<% elsif params[:id] == '2'  %>
   You are the second mentor!
<% else %>
  Welcome to the group!
<% end %>
```

**for each**
```ruby
<% @mentor_names = ["john", "bill", "sarah", "alex"] %>

<% @mentor_names.each do |mentor_name| %>
   <%= mentor_name %>
<% end %>
```
**hash**
```ruby
<% @mentor_info = { 'name' => 'John Pollard', 'address' => '1965 Crane Creek'  }  %>
<%= @mentor_info["name"] %>
<%= @mentor_info["address"] %>
```

**for each with a hash**
```ruby
<% @mentees = [{ 'name' => 'John Pollard', 'address' => '1965 Crane Creek'  },
               { 'name' => 'Bill Gates', 'address' => '13015 Deep River Way'}]  %>

<% @mentees.each do |mentee| %>
   <%= mentee["name"] %>
   <%= mentee["address"] %>
   <br>
<% end %>
```
Now you can render a partial with a collection
```ruby
<%= render partial: 'mentee_info', collection: @mentees %>
```
