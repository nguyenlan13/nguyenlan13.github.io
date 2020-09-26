---
layout: post
title:      "Require and Require Relative"
date:       2020-09-26 19:52:19 +0000
permalink:  require_and_require_relative
---


When setting up the environment and bin files, require is a method that takes in a file name to load, the file must be in the project directory where the application is being run. When using require_relative, the required files will always be located relative to where the file that is calling require_relative is located.

```
FITNESS
   |
   |--bin
   |   |--console
   |   |--group_fitness_classes (executable)
   |   |--setup
   |
   |--lib
   |    |--fitness.rb
   |    |--fitness
   |          |--cli.rb
   |          |--group_fitness.rb
   |          |--gym_locations.rb
   |          |--scraper.rb
   |          |--version.rb
   |
   |--fitness.gemspec
   |--Gemfile
	 
	 ```
In this file directory, the executable file (group_fitness_classes) is using require_relative '../lib/fitness.rb'. The 'fitness.rb' file is the environment file that is requiring the rest of the files and it is located in the sibling 'lib' folder. The parent folder is indicated by the '../' prefix in file path while './' would indicate same or current folder.

