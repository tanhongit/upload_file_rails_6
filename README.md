# Welcome to Rails 6 File Upload by TANHONGIT

The Rails 6 File Upload is a small task for everyone to practice more when programming with Ruby on Rails.

We will use gem carrierwave to perform this task.

## Support for me
Support this project :stuck_out_tongue_winking_eye: :pray:
<p align="center">
    <a href="https://www.paypal.me/tanhongit" target="_blank"><img src="https://img.shields.io/badge/Donate-PayPal-green.svg" data-origin="https://img.shields.io/badge/Donate-PayPal-green.svg" alt="PayPal buymeacoffee TanHongIT"></a>
</p>

# 1. Technology
- Ruby on Rails

# 2. Configuration requirements
We are going to build the web application using:
    - Rails 6.0.3.2
    - Ruby 2.7.1

# 3. Feature

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

```
class Resume < ApplicationRecord   
mount_uploader :attachment, AttachmentUploader # Tells rails to use this uploader for this model.   
   validates :name, presence: true # Make sure the owner's name is present.   
end  
```

