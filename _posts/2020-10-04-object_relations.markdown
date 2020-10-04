---
layout: post
title:      "Object Relations"
date:       2020-10-04 17:33:49 +0000
permalink:  object_relations
---


```
class Recipe

      def initialize(name)
             @name = name
             @ingredients = []
      end
  
      def add_ingredient(ingredient)
             @ingredients << ingredient
      end

      def add_ingredients(ingredients)
             ingredients.each do |ingredient| 
                  @ingredients << Ingredient.new(ingredient)
             end
      end
end 


class Ingredient

       def initialize(name)
             @name = name
       end
end


pb_j = Recipe.new("pb&j")

ingredients = ["bread", "peanut butter", "jelly"]

       ingredients.each_with_index do |ingredient, index| 
       ing_obj = Ingredient.new(ingredient)
       pb_j.add_ingredient(ing_obj)
  
       end
			 
      ingrs = ingredients.map do |ingredient| 
      Ingredient.new(ingredient)
      end


pb_j.add_ingredients(ingredients)
pb_j
```
