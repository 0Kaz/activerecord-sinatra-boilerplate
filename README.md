<h1>Active Record Sinatra Livecode</h1>

<h2> Sinatra :</h2>
Sinatra is a DSL (Doman Specific Language), the principle of this small web framework is to write web applications in Ruby with minimal effort.



<h2>File Structure :</h2>

<img src="https://res.cloudinary.com/kzkjr/image/upload/v1659995695/Screen_Shot_2022-08-08_at_22.47.37.png"/>


First thing you need to do when you download this boilerplate is to run ```bundle install``` to set all the dependencies needed for this exercise.




## Building a restaurant web app :

The main user story for this small web app is as such :

- <i style="background-color: silver">As a user I can list all the restaurants</i>
- <i style="background-color: silver">As a user I can see one restaurant's details</i>
- <i style="background-color: silver">As a user I can add a restaurant</i>


## Migration

First step is to create your database :

<code>
rake db:migrate
</code>


Generate then a new migration to create the ```restaurants``` table with the ```name``` and ```address``` columns:

In your terminal :

```
TIMESTAMP =`rake db:timestamp`
touch db/migrate/${TIMESTAMP}_create_restaurants.rb
```

Then add this code in your new migration file :

<code>
class CreateRestaurants < ActiveRecord::Migration[7.0]
  def change
    create_table :restaurants do |t|
      t.string :name
      t.string :address
      t.timestamps
    end
  end
end
</code>

Run the migration ```rake db:migrate```

Generate the model then:
```touch models/restaurant.rb```

<code>
# models/restaurant.rb
class Restaurant < ActiveRecord::Base
end
</code>


<h2>Seeds</h2>

Let's add some seeds :

<code>
require 'faker'

10.times do
  Restaurant.create!(
    name: Faker::Coffee.blend_name,
    address: Faker::Address.city
  )
end

</code>


1 - Launch the app by using the main file <code> ruby app.rb</code>

2 - Access the page by going to your navigator with the link : localhost:4567
