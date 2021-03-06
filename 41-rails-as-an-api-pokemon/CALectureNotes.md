# Instructions for Lecture:

[Learn.co Pokemon Trainers Lab](https://github.com/learn-co-students/js-rails-as-api-pokemon-teams-project-seattle-web-080519)

**Why use Rails as an API?**
    
> The fundamental difference between an API and a regular Rails app is that an API returns data for further processing, rather than data that is meant to be viewed directly. Therefore, rather than producing an HTML document (with CSS and/or Javascript) that looks pretty, APIs produce simple information structures that can be further processed by whatever will be consuming our API." - Thibaud Clement, Stack Overflow

## Backend

1. Create your backend file structure for Rails. We suggest using PostgreSQL for deployment purposes. 
    - `rails new pokemon-teams-backend --api --database=postgresql`
    - The `--api` flag configures it to handle API calls
2. `gem install faker`
3. `gem install active_model_serializers`
    - Be sure to install this BEFORE you install your resources so that they are properly linked
    - Your serializers allow access to specific attributes and implements ActiveRecord associations when querying for data to render to your frontend
4. Generate resources for your models:
    - `rails g resource trainer name`
    - `rails g resource pokemon species nickname trainer:references`
5. Confirm that all your folders / files have been created successfully. Double check `seeds.rb`, `routes.rb`, controllers folder, models folder, and serializers folder.
    - You will have to create seeds for the database (provided by the lab's README)
    - Be sure to check for relationships in the models
6. Set up your application for Cross Origin Resource Sharing (CORS)
    - Uncomment `gem rack-cors` in the Gemfile
    - Uncomment the code within config --> initializers --> cors.rb
    - Replace `example.com` with `*`, allowing your frontend to access all routes on your backend
7. `rails db:create`
8. `rails db:migrate`
9. `rails db:seed`
10. Create `index` and `show` actions in your trainers controller.
    - Note that within your controller actions, you need to _render_ your _json_
    - `render json: declared_instance_variable`
11. Create `index`, `show`, `new`, `create`, & `destroy` actions in your pokemons controller.
    - Include error handling in the create to account for reaching the trainer's limit of 6 pokemon.

**Note:** Do not forget that you will have to nest an additional attribute in the serializer that "holds many" of the other model.


## Frontend

1. Confirm that the fetches to your two URLs returns the data in the correct format.
2. We are going to start with pre-written code in our *frontend* folder to expedite lecture flow.
    - Fetch the trainers (with their "pokemons" from the `serializer`)
    - Render the trainers
    - Render a trainer
    - Render the pokemons
    - Render a pokemon
    - Release a pokemon


## Resource(s):

 - [Rails Error Handling](https://www.thegreatcodeadventure.com/rails-api-painless-error-handling-and-rendering-2/)
 - [Rails API Doc](https://guides.rubyonrails.org/api_app.html)
 - [sqlite vs. postgres](https://www.digitalocean.com/community/tutorials/sqlite-vs-mysql-vs-postgresql-a-comparison-of-relational-database-management-systems)