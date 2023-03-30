### To manage multiple ruby and rails version
We're going to use ruby-2.5.1 and rails-5.2.1 
- rvm manage multiple ruby versions
```
rvm list known
rvm list //list installed ruby versions and current active ruby version 
rvm install 2.5.1 
```
confirm:   
```
❯ rvm list
=> ruby-2.5.1 [ x86_64 ]
   ruby-2.6.10 [ x86_64 ]
 * ruby-2.7.2 [ x86_64 ]
```
- gem install rails version
rails can be installed in different spaces/folders, therefore you can create multiple folders for different rails, eg. "rails_5_space" and "rails_6_space". If you installed rails v6.x in rails_6_space and then switch to rails_5_space, check with "rails -v", showing no rails installed, so you can install rails v5.x in rails_5_space.   
```
❯ gem install rails -v 5.2.1 
ERROR:  Error installing rails:
	The last version of nokogiri (>= 1.6) to support your Ruby & RubyGems was 1.12.5. Try installing it with `gem install nokogiri -v 1.12.5` and then running the current command again
	nokogiri requires Ruby version >= 2.7, < 3.3.dev. The current ruby version is 2.5.1.57.
❯ gem install nokogiri -v 1.12.5
...
❯ gem install rails -v 5.2.1 // you will encounter several errors, just follow the suggestion by system and install necessary package then reinstall rails v5.2.1, and finally you can get the tasks done.  
```  
- create app with designated rails version 
```
❯ rails _5.2.1_ new message_me
cd message_me
```
- to switch ruby version with rvm: 
when open a new terminal, maybe need to reset the default ruby version:  
```
❯ rvm --default use 2.5.1
```

**sqlite is no longer available for ruby-2.5.x, so I have to switch to ruby-2.7.2, the purpose is to use rails-5, ruby's version is not so strict.**  