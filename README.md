## Active Record Sinatra boilerplate

## Sinatra :

Sinatra is a DSL (Doman Specific Language), the principle of this small web framework is to write web applications in Ruby with minimal effort.



## File Structure :

<img src="https://res.cloudinary.com/kzkjr/image/upload/v1659995695/Screen_Shot_2022-08-08_at_22.47.37.png"/>


First thing you need to do when you download this boilerplate :

1 - run ```bundle install``` to set all the dependencies needed for this exercise.

2 - Launch the app by using the main file <code> ruby app.rb</code>

3 - Access the page by going to your navigator with the link : localhost:4567


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
