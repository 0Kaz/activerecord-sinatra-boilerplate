<h1>Active Record Sinatra Livecode</h1>


Hello class, this is a repo with a complete guideline for our Sinatra livecode


<h2> Sinatra :</h2>
Sinatra is a DSL (Doman Specific Language), the principle of this small web framework is to write web applications in Ruby with minimal effort.



<h2>File Structure :</h2>

<img src="https://res.cloudinary.com/kzkjr/image/upload/v1659995695/Screen_Shot_2022-08-08_at_22.47.37.png"/>


First thing you need to do when you download this boilerplate below :

```
git clone git@github.com:lewagon/activerecord-sinatra-boilerplate.git
cd activerecord-sinatra-boilerplate
code .
```

And to run ```bundle install``` to set all the dependencies needed for this exercise.




## Building a restaurant web app :

The main user story for this small web app is as such :

- <i style="background-color: silver">As a user I can list all the restaurants</i>
- <i style="background-color: silver">As a user I can see one restaurant's details</i>
- <i style="background-color: silver">As a user I can add a restaurant</i>


## Migration

First step is to create your database :

```
rake db:create
```


Generate then a new migration to create the ```restaurants``` table with the ```name``` and ```address``` columns:

In your terminal :

```
TIMESTAMP =`rake db:timestamp`
touch db/migrate/${TIMESTAMP}_create_restaurants.rb
```

Then add this code in your new migration file :

```
class CreateRestaurants < ActiveRecord::Migration[7.0]
  def change
    create_table :restaurants do |t|
      t.string :name
      t.string :address
      t.timestamps
    end
  end
end
```

Run the migration ```rake db:migrate```

Generate the model then:
```touch models/restaurant.rb```

```
# models/restaurant.rb
class Restaurant < ActiveRecord::Base
end
```


<h2>Seeds</h2>

Let's add some seeds :

```
require 'faker'

10.times do
  Restaurant.create!(
    name: Faker::Coffee.blend_name,
    address: Faker::Address.city
  )
end

```


1 - Launch the app by using the main file <code> ruby app.rb</code>

2 - Access the page by going to your navigator with the link : localhost:4567

3 - Do a quick reading and understanding of the ```app.rb```file  (get "/" do ... end)

<h2>ERB </h2>

ERB stands for Embedded Ruby, its a templating language based on Ruby, in our case with Sinatra, this will help us mix both Html and Ruby on Sinatra , for more information , check out this link : <a href="https://puppet.com/docs/puppet/5.5/lang_template_erb.html"> Here </a>


Let's add this code in ``app.rb`` :

```
get "/" do
  @restaurants = Restaurant.all
  erb :index
end
```


Now let's add the view for index in ```views/index.erb```:

```
<h1>My Restaurant App</h1>
<p>The list of my favorite restaurants</p>

<ul>
  <% @restaurants.each do |restaurant| %>
    <li><%= restaurant.name %></li>
  <% end %>
</ul>

```


<h2>Displaying only one restaurant</h2>

We want to be able to go to the page of a specific restaurant.

Restaurants have ids. So we want to go to a URL like: restaurant/3

At this step, you can give IRL examples:

- airbnb.com/rooms/432044
- github.com/ssaunier

We need to add a new route on ```app.rb```:

```
get '/restaurant/:id' do
  restaurant_id = params[:id]
  @restaurant = Restaurant.find(restaurant_id)
  erb :show
end

```

and a view called ```show.erb``` with this code :

```
<h1><%= @restaurant.name %></h1>
<p><%= @restaurant.address %></p>

<a href="/">back</a>
```

<h2> Adding URL Routing to our Restaurant app :</h2>

We can add URL routes for the path in ```show.erb``` if we wish to link our lists of restaurants with their specific page.

```
<h1>My Restaurant App</h1>
<p>The list of my favorite restaurants</p>

<ul>
  <% @restaurants.each do |restaurant| %>
    <li><a href="/restaurant/<%= restaurant.id=%>"><%= restaurant.name %></a></li>
  <% end %>
</ul>

```
