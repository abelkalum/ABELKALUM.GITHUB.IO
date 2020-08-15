---
layout: post
title:      "Authentication in Sinatra CRUD App"
date:       2020-08-15 16:15:36 -0400
permalink:  authentication_in_sinatra_crud_app
---


It is not safe to store passwords in the database in their raw form. To protect each password we need to have them encrypted. To this end, we use the bcrypt gem to encrypt passwords. The bcrypt gem helps encrypt passwords before being stored in the database. The bcrypt gem provides us with a has_secure_password method which encrypts passwords by hashing and salting them. The bcrypt gem will then store the salted and hashed version of the users' passwords in the database in a password column called password_digest. 

So how does this work? For the password authentication to work one should:

1. Include bcrypt gem in the Gemfile.
2. Add the password_digest column in the users’ table.
3. Add has_secure_password method in the User model file.
4. Include sign up and login form for User model.

When the above conditions have been met, then one should create users through signup and login, and add #authenticate method in the sessions controller to verify app users’ passwords. The #authenticate method is provided by the has_secure_password method. 
In my app I used the #authenticate method in my post ‘/login’ route as shown below:
```
post '/login' do
    @user = User.find_by(email: params[:email])
    if @user && @user.authenticate(params[:password])
      session[:user_id] = @user.id

      redirect "users/#{@user.id}"
    else
      redirect '/login'
    end
  end
```
Essentially, the #authenticate method in line 3 above turns the user's password input into a hash that would get compared with the hashed password already stored in the database. If the user is verified, the method would return the User instance; otherwise, it would return false. This is a more safe way as the user’s password is protected in a salted and hashed version. If line 3 had been written without the #authenticate method the passwords would not be protected (see example below).

if @user && @user.password == params[:password])

The above code will not protect the entered and stored passwords as they are not encrypted, they are being compared in their raw form. So the #authenticate method provided by has_secure_password is very crucial in protecting passwords because it compares encrypted passwords without revealing the raw passwords.
