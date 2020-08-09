# Welcome to Rails 6 File Upload by TANHONGIT

The Rails 6 File Upload is a small task for everyone to practice more when programming with Ruby on Rails.

We will use gem carrierwave to perform this task.

## Support for me
Support this project :stuck_out_tongue_winking_eye: :pray:
<p align="center">
    <a href="https://www.paypal.me/tanhongit" target="_blank"><img src="https://img.shields.io/badge/Donate-PayPal-green.svg" data-origin="https://img.shields.io/badge/Donate-PayPal-green.svg" alt="PayPal buymeacoffee TanHongIT"></a>
</p>

# Demo

You can try it at https://calm-escarpment-34931.herokuapp.com/

# 1. Technology
- Ruby on Rails

# 2. Configuration requirements
We are going to build the web application using:
- Rails 6.0.3.2
- Ruby 2.7.1

# 3. Feature
Ability to upload many different types of files: .jpg, .png, .pdf, .mp4 , .mp3, .word, .excel, .....

# 4. Tutorial

## Step 1 Create a Rails application called upload.

```
rails new upload 
```

## Step 2 Change your directory to upload.

```
cd upload  
```

## Step 3 Install the following gems.

```
gem install carrierwave  
gem install bootstrap-sass  
```

## Step 4 Go to the Gemfile in your directory and add the following gems.

```
gem 'carrierwave'   
gem 'bootstrap-sass'  
```

## Step 5 Run the following command.

```
bundle install  
```

## Step 6 Create a model with two strings as name and attachment.

```
rails g model Resume name:string attachment:string  
```

## Step 7 Migrate your database.

```
rake db:migrate  
```

## Step 8 Generate the controller file in your application.

```
rails g controller Resumes index new create destroy  
```

## Step 9 In this step, we will create an uploader through carrierwave gem.

```
rails g uploader attachment  
```

## Step 10 Now open the app/models/resume.rb model file and write the following code.

```ruby
class Resume < ApplicationRecord   
mount_uploader :attachment, AttachmentUploader # Tells rails to use this uploader for this model.   
   validates :name, presence: true # Make sure the owner's name is present.   
end  
```

## Step 11 Go to config/routes.rb file and write the following code.

```ruby
resources :resumes, only: [:index, :new, :create, :destroy]   
   root "resumes#index"  
```

## Step 12 Go to app/controllers/resumes_controller.rb file and write the following code.

```ruby
class ResumesController < ApplicationController

    def index   
      @resumes = Resume.all   
   end   
      
   def new   
      @resume = Resume.new   
   end   
      
   def create   
      @resume = Resume.new(resume_params)   
         
      if @resume.save   
         redirect_to resumes_path, notice: "Successfully uploaded."   
      else   
         render "new"   
      end   
         
   end   
      
   def destroy   
      @resume = Resume.find(params[:id])   
      @resume.destroy   
      redirect_to resumes_path, notice:  "Successfully deleted."   
   end   
      
   private   
      def resume_params   
      params.require(:resume).permit(:name, :attachment)   
   end   
end
```

## Step 13 Add bootstrap in app/assets/stylesheets/resumes.scss file.

```ruby
@import "bootstrap";  
```

## Step 14 Go to app/views/layouts/application.html.erb file and write the following code.

```ruby
<!DOCTYPE html>
<html>
  <head>
    <title>UploadFileRails6</title>
    <%= csrf_meta_tags %>
    <%= csp_meta_tag %>

    <%= stylesheet_link_tag 'application', media: 'all', 'data-turbolinks-track': 'reload' %>
    <%= javascript_pack_tag 'application', 'data-turbolinks-track': 'reload' %>
  </head>

  <body>
    <%= yield %>
  </body>
</html>
```

## Step 15 Go to app/views/resumes/index.html.erb file.

```ruby
<div class="container">   
<% if !flash[:notice].blank? %>   
   <div>   
      <%= flash[:notice] %>   
   </div>   
<% end %>   
  
<br>   
  
<%= link_to "New Resume", new_resume_path %>   
<br>   
<br>   
  
<table border="3">   
   <thead>   
      <tr>   
         <th>Candidate Name</th>   
         <th>Download Link</th>   
         <th>Action</th>   
      </tr>   
   </thead>   
      
   <tbody>   
      <% @resumes.each do |resume| %>   
            
         <tr>   
            <td><%= resume.name %></td>   
            <td><%= link_to "Download", resume.attachment_url %></td>   
            <td><%= link_to "Delete",  resume, method: :delete, confirm: "Are you sure you want to delete #{resume.name}?" %></td>   
         </tr>   
            
      <% end %>   
   </tbody>   
      
</table>   
</div>
```

## Step 16 Go to app/views/resumes/new.html.erb file.

```ruby
<div class="container">
  <% if !@resume.errors.empty? %>
    <div>

      <ul>
        <% @resume.errors.full_messages.each do |msg| %>
          <li><%= msg %></li>
        <% end %></ul>
    </div>
  <% end %>
</div>

<div class="container">
  <% if !@resume.errors.empty? %>
    <div>

      <ul>
        <% @resume.errors.full_messages.each do |msg| %>
          <li><%= msg %></li>
        <% end %>      </ul>

    </div>
  <% end %>

  <div>
    <%= form_for @resume, html: {multipart: true} do |f| %>
      <%= f.label :name %>
      <%= f.text_field :name %>
      <br><br>
      <%= f.label :attachment %>
      <%= f.file_field :attachment %>
      <br>
      <%= f.submit "Save" %>
    <% end %>
  </div>
</div>
```

## Step 17 Now start the server.

```
rails s
```

# Demo

![Image](https://imgur.com/Rt7aXkF.png)

---------------------------------------------------------------------------------

![Image](https://imgur.com/xw6ZZTN.png)

---------------------------------------------------------------------------------

![Image](https://imgur.com/80d12lx.png)
