# README

This README would normally document whatever steps are necessary to get the
application up and running.

Things you may want to cover:

* Ruby version

* System dependencies

* Configuration

* Database creation

* Database initialization

* How to run the test suite

* Services (job queues, cache servers, search engines, etc.)

* Deployment instructions

* ...



INSTRUCTIONS    _ _ _ __ __ _ _ _
RANDOM COMMANDS :::::::::

   bundle
   rake db:create
   rake db:migrate
   rake db:test:prepare
   rake db:seed

*rails new 'app name'

*Add   gem 'jquery-rails'  to GemFile

*  && Add   group :development, :test do
      gem 'byebug', platforms: [:mri, :mingw, :x64_mingw]
      gem 'rspec-rails'
      gem 'launchy'
      gem 'pry'
    end
                                      to Gemfile  




* bundle exec rails generate rspec:install (in Terminal)


* run rails server in Root dir of project [rails s]


* rake db:create

* rails g migration create_[class] (plural)

* Go into db/migrate/2438403258923095723509[project_name] & Add columns
   EX. t.column(:title, :string) &&  t.timestamps() * t.string: name*

*rake db:migrate

*rake db:test:prepare

*create new file in app/models/[class_name].rb (singular naming)and Add
        class [class_name] < ApplicationRecord
        end

* rails g migration create_[class] for additional classes


  FOR MANY 2 MANY RELATIONSHIPS
  { * rails g migration join_[class]_and_[class] (for join tables)

    *Add  
    create_table :albums_artists, id: false do |t|
     t.belongs_to :artist, index: true
     t.belongs_to :album, index: true
    end
                      in [class]_[class].rb (alpha + plural)


*Add has_and_belongs_to_many(:class) (plural)

                            in app/models/class.rb

  }


    ---->  t.integer :product_id  <-------  Don't forget!!

* in new migration, set up relationship between Class1 and Class2
"rails g migration add_foreign_key_for_[class2]"

* in new migration, set up foreign key relationship between Class1 and Class2

* create a new Model for class in 'app/models/class_name.rb (singular)

* Class2 belongs_to :class1, Class1 has_many :class2

      class Song < ApplicationRecord
        belongs_to :album
      end

      class Album < ApplicationRecord
        has_many :songs
      end

* Add 'models' folder to spec folder and add the album_spec.rb & song_spec.rb

* Add   require 'rails_helper'   to album_spec.rb

* Add
              group :test do
              gem 'shoulda-matchers'
              end                            to GemFile ¡AFTER! all other blocks


* Add                                          
            Shoulda::Matchers.configure do |config|
              config.integrate do |with|
                with.test_framework :rspec
                with.library :rails
              end
            end
                                          to spec/rails_helper.rb


* Add
            require 'rails_helper'

            describe Album do
              it { should have_many :songs }
            end                                          
                                            to spec/models/album_spec.rb

* Add
         require 'rails_helper'

         describe Album do
           it { should belong_to :albums }
         end                                          
                                        to spec/models/song_spec.rb



    ========MANY TO MANY ======  
    describe(Album) do
    it { should have_and_belong_to_many :employees }     
    end
    ==========================================



* Add validation for title and length: spec/models/album_spec.rb

  describe(Album) do
    it { should validate_length_of(:name).is_at_most(100) }
  end    



  * Add validation logic in app/models/album.rb

    class Album < ApplicationRecord
      validates :name, presence: true
    end     


*Add  
              before_save(:titleize_survey)

                  private
                  def titleize_survey
                    self.title = self.title.titleize
                  end

                  end                                                            
                                               to app/models/album.rb


*Add
                    Rails.application.routes.draw do
                    root to: 'albums#index'
                    resources :albums do
                    resources :songs
                    end
                    end

                      ========MANY TO MANY ======  



                      ===========================
                                             to config/routes.rb



* Check routes in terminal     (rake routes)                               

* Add  "app/controllers/[class]s_controller.rb"  file

"class [Class]sController < ApplicationController"

    make all the ruby methods
    rename album to survey
    change :genre to :author

* Add layout views folders/files for new/edit forms in "apps/views/[class]s
     edit.html.erb
     index.html.erb
     new.html.erb
     show.html.erb


* Add _errors.html.erb

<% if object.errors.any? %>
  <h3>Please fix these errors:</h3>
  <ul>
    <% object.errors.full_messages.each do |message| %>
      <li><%= message %></li>
    <% end %>
  </ul>
<% end %>
                                      to apps/views/layouts

                                      

  *Add      _[class]_form.html.erb" (w/ underscores)

                                        to apps/views/layouts/

*Add       
            <%= render "layouts/errors", :object => @[class]] %>

            <%= form_for @[class]] do |f| %>
            <%= f.label :div_name %>
            <%= f.text_field :div_name %>
            <%= f.submit %>
            <% end %>
                                         to apps/views/layouts/[class]


* Add 'faker' to Gemfile & bundle

* Add
Division.destroy_all
Employee.destroy_all

50.times do |index|
divisions = []
divisions.push(Division.create!(div_name: Faker::TvShows::BreakingBad.episode))
divisions
rand(3..15).times do |employee|
divisions.each do |division|
Employee.create! :name => Faker::Superhero.name,
            :division_id => division.id
end
end
end

p "Created #{Division.count} divisions"
                to db/seeds.rb                                     
