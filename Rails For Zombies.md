###CHALLANGE 1

* Zombie.find(1)

* t = Zombie.new(id:4, name:"Goktay", graveyard: "GopCity")

t.save

* Zombie.last

* Zombie.order(:name)

* t = Zombie.find(3)

 t.graveyard = "Benny Hills Memorial"
 
 t.save

* t = Zombie.find(3).destroy

###CHALLANGE 2

* class Zombie < ActiveRecord::Base

end

* class Zombie < ActiveRecord::Base

  validates_presence_of :name
  
end

* class Zombie < ActiveRecord::Base

  validates_uniqueness_of :name
  
end


* class Zombie < ActiveRecord::Base

  validates :name, presence: true, uniqueness: true
  
end


* class Weapon < ActiveRecord::Base

  belongs_to :zombie
  
end


* ash = Zombie.find(1)

ash.weapons


###CHALLANGE 3

* <;h1><%= zombie.name %></h1>

<p> <%= zombie.graveyard %></p>


* <p><%= link_to zombie.name, zombie %></p>


* <% zombies.each do |zombie| %>

<%=zombie.name%>

<%end%>


* <% zombies.each do |zombie| %>

      <%= zombie.name %>
      
      <% if zombie.tweets.size > 1 %>
      
      SMART ZOMBIE
      
      <% end %>
      
  <% end %>


* <ul>

  <% zombies.each do |zombie| %>
  
    <;li>
    
      <td><%= link_to zombie.name, edit_zombie_path(zombie)%>
      
      <%= zombie.name %>
      
    </li>
    
  <% end %>
  
</ul>


###CHALLANGE 4

* class ZombiesController < ApplicationController

  def show
  
    @zombie = Zombie.find(params[:id])
    
  end
  
end



* class ZombiesController < ApplicationController

  def show
  
    @zombie = Zombie.find(params[:id])

    respond_to do |format|
    
      format.html # show.html.erb
      
      format.xml { render xml: @zombie}
      
    end
    
  end
  
end



* class ZombiesController < ApplicationController

  def create
  
    @zombie = Zombie.create(zombie_params)
    
    redirect_to(@zombie)
    
  end

private

  def zombie_params
  
    params.require(:zombie).permit(:name, :graveyard)
    
  end
  
end



* class ZombiesController < ApplicationController

  before_action :find_zombie
  
  before_action :has_tweets, only: :show
  
  def show
  
	  render action: :show
	  
  end

  def find_zombie
  
    @zombie = Zombie.find params[:id]
   
  end
  def has_tweets 
  
    if @zombie.tweets.size == 0
    
    redirect_to(zombies_path)
    
     end
     
  end
  
end


###CHALLANGE 5

* TwitterForZombies::Application.routes.draw do

  resources :zombies
  
end


* TwitterForZombies::Application.routes.draw do

   resources :zombies
   
   get '/undead' => "zombies#undead"
   
end


* TwitterForZombies::Application.routes.draw do

get '/undead' => redirect('/zombies')

end


* TwitterForZombies::Application.routes.draw do

  root to: "zombies#index"
  
end


* TwitterForZombies::Application.routes.draw do

  get '/zombies/:name', to: 'zombies#index', as: 'graveyard'
  
end
