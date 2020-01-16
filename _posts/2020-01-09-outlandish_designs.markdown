---
layout: post
title:      "outLANdish designs"
date:       2020-01-09 12:25:29 -0500
permalink:  outlandish_designs
---



This application was built utilizing a Ruby on Rails backend with session cookies for API authentication and a vanilla JavaScript frontend.

## E-Commerce

I was excited to be able to incorporate a personal side business into this project and see it come to life . This project was an e-commerce application for my small custom T-shirt business. This application was very challenging to build. Just implementing the authentication process took multiple days to figure out. The backend consists of multiple join tables to form the cart, category, and wish list functionality. 


## Rails API Backend

The API backend uses a Model-View-Controller structure with CRUD actions and RESTful routes. The views are omitted because it is communicating with a JavaScript frontend. The core model associations were:

```
class Account < ApplicationRecord
    
    has_one :cart
    has_many :orders
    has_many :reviews
    has_one :wishlist
    
end


class Cart < ApplicationRecord

    has_many :cart_items
    has_many :items, through: :cart_items
    belongs_to :account, optional: true
		
end


class CartItem < ApplicationRecord

    belongs_to :item
    belongs_to :cart

end


class Item < ApplicationRecord

    has_many :cart_items
    has_many :carts, through: :cart_items
    has_many :order_items
    has_many :orders, through: :order_items
    has_many :reviews
    has_many :wishlist_items
    has_many :wishlists, through: :wishlist_items
    has_many :item_categories
    has_many :categories, through: :item_categories
		
end
```


## JavaScript Frontend

The frontend folllows a decorator design pattern where functionality of a base class is decorated  and used to separate functionality for the different adapters and page managers used in fetch requests.

```
class BaseAdapter{

    constructor(baseURL = 'http://localhost:3000/api/v1'){
        this.baseURL = baseURL
        this.authSetup()
        this.csrf_token = null
    }

    async authSetup(){
        const res = await fetch(`${this.baseURL}/auth`, {
            credentials: 'include'
        })
        const body = await res.json()
        this.csrf_token = body.csrf_auth_token
    }

    get headers(){
        let baseHeaders = {
            'Accept': 'application/json',
            'Content-Type': 'application/json',
            'X-CSRF-TOKEN': this.csrf_token
        }
        return baseHeaders
    }
}

```

```
class CartAdapter{

    constructor(baseAdapter){
        this.baseAdapter = baseAdapter
        this.baseURL = this.baseAdapter.baseURL
    }


    get headers(){
        return this.baseAdapter.headers
    }
        
				
    async showCartItems(){
        try{
            const cartItemResponse = await fetch(`${this.baseURL}/mycart`, {
                method: "GET",
                headers: this.headers,
                credentials: 'include'
            })
            const cartItemJson = await cartItemResponse.json()
            return cartItemJson
        }catch(error){
            console.log(error.message)
        }
    }


    async removeFromCart(currentId){
        try{
            const removeResponse = await fetch(`${this.baseURL}/cart_items/${currentId}`, {
                method: "DELETE",
                headers: this.headers,
                body: JSON.stringify({item_id: currentId}),
                credentials: 'include'
            })
        }catch(error){
            console.log(error.message)
        }
    }
}
```



## Project Outcome

This project had major hurdles and took much longer than expected to execute but overall, functionality is what I had envisioned. There is still quite some work to do in order to implement the checkout process, review, and wishlist functionality. 
