---
layout: post
title:      "Sinatra Project - Shelf Development"
date:       2019-08-26 10:27:37 +0000
permalink:  sinatra_project_-_shelf_development
---


# Scope
The project scope is comprised of utilizing CRUD (create, read, update, destroy) actions in a MVC (Model-View-Controller) structure and Sinatra framework to create a web application that keeps track of a collection.

# Topic: Self-Development
Self-development is often overlooked and stigmatized because it relates to mental health, but from my experience, access to this knowledge base can have such a profound impact on perspective and even change the trajectory of your life. It can set the foundation for generating more self-awareness and a better understanding of how to deal with all the obstacles that arise throughout life.

I had the idea to track different self-development medias (books, podcasts, and articles) for the purpose of creating a positive outlet for users to demonstrate vulnerability and be able to discuss their learning experiences, advice, insights, main takeaways, etc. in a group setting to form a collective and open space for learning. 
My vision for the application was to allow users to build a library comprised of books, podcast episodes, and articles. For each of these items, users would be able to insert their favorite quotes, rate the item (1 - 5 stars), comment on the item, and be able to reply and react to other user’s comments. 

# Model-View-Controller
Utilizing a Model-View-Controller structure for this application provides a separation of concerns, it is a way of organizing the code to make reading and debugging much easier. Each element has a specific function. 
The model element provides the logic and set the rules of the application, this is where object relationships are defined and where input validations are set. Typically, each model corresponds to a database table. In this application, there were 9 models: article, book, podcast, author, comment, quote, rating, reaction, and user. A portion of the models had polymorphic associations, meaning the model can belong to more than one model on a single association. An example is the comment model:


```
class Comment < ActiveRecord::Base
  validates :user_id, presence: true
  validates :content, presence: true
  validates :commentable_id, presence: true
  validates :commentable_type, presence: true

  belongs_to :user
  belongs_to :commentable, polymorphic: true

  has_many :comments, as: :commentable
  has_many :reactions, as: :reactable
end
```


The view element is the front-end portion and where the user directly interacts with the application, this is where user input forms, html, CSS, and embedded Ruby (erb tags) are used to display the content that the user sees in the browser. The example below is a form for adding new comments:


```
<h4>Add a comment:</h4>
<form method="post" action="/comments">
<input type="hidden" name="comment[commentable_type]" value="<%=esc commentable.class.name%>">
<input type="hidden" name="comment[commentable_id]" value="<%=esc commentable.id%>">
<input type="hidden" name="comment[comment_path]" value="<%=esc commentable_type%>">
<textarea name="comment[content]" placeholder="Type here"></textarea>
<br/>
<br/>
<input type="submit" value="Add Comment">
</form>
```


The controller element is the connection between the model and view. It is responsible for relaying the communicating between the browser and application. The controller consists of routes; routes take requests from the browser and use the models to run the code and then render the view files for the use to see. 


```
class CommentController < ApplicationController

  ##COMMENTS - polymorphic
  
	post '/comments' do
		authorize
    user = current_user
    @commentable_id = params[:comment][:commentable_id]
    @commentable_type = params[:comment][:commentable_type]
    @comment_path = params[:comment][:comment_path]
    Comment.create(user: user, content: params[:comment][:content], commentable_id: @commentable_id, commentable_type: @commentable_type)
    redirect "/#{@comment_path}/#{@commentable_id}"
	end


  get '/comments/:id/edit' do
    @comment = Comment.find_by(id: params[:id])
    auth_edit(@comment)
    erb :"comment/edit"
  end


  patch '/comments/:id' do
    @commentable_id = params[:comment][:commentable_id]
    @commentable_type = params[:comment][:commentable_type]
    comm_path
    @comment = Comment.find_by(id: params[:id])
    auth_edit(@comment)
    @comment.update(content: params[:comment][:content])
    redirect "/#{@comment_path}/#{@commentable_id}"
  end


  delete '/comments/:id' do
    @commentable_id = params[:comment][:commentable_id]
    @commentable_type = params[:comment][:commentable_type]
    comm_path
    @comment = Comment.find_by(id: params[:id])
    auth_edit(@comment)
    @comment.delete
    redirect "/#{@comment_path}"
  end
```


# Create, Read, Update, Destroy
Complete CRUD actions were allowed on two resources, the favorite quotes and comments. The difference between these two resources and the others are that these resources had edit and destroy capabilities. A user was allowed to edit or delete their own favorite quote or comment. The edit action corresponds to a patch request and destroy action corresponds to the delete request.


# Project outcome
Aside from not having yet added the reaction and reply features to the application, the application is functioning as expected. It took numerous days of refactoring and debugging and it was difficult to hold back from trying to implement every capability/feature I thought of. Users are able to add a discussion item if it doesn’t already exist in the library and meets the validation requirements. They can then provide a rating for the item and utilize CRUD actions on their favorite quotes and comments. In addition, a user cannot edit or delete another user’s quotes or comments; if they attempt to, it will redirect and render an error message page.

