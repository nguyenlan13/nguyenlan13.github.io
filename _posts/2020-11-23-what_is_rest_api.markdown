---
layout: post
title:      "What is REST API?"
date:       2020-11-23 07:23:19 +0000
permalink:  what_is_rest_api
---


REST is a convention for structuring URLs, it stands for REpresentational State Transfer. These URLs are coordinated with the CRUD (create, read, update, destroy) action and the associated HTTP verb (GET, POST, PATCH, DELETE). For example, if we had a book site, these could be our URLs:


| Method | URL | Description |
--------------------
| GET | /books | Show all Books |
| POST | /books | Create a new book |
| GET | /books/new | Render form for creating new book |
| GET | /books/:id/edit | Render form for editing book |
| GET | /books/:id | Show a single book |
| PATCH | /books/:id | Update a book |
| DELETE | /books/:id | Delete a book |


