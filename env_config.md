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

### Use semantic ui
- add semantic ui: 
Go to [semantic-ui github repo](https://github.com/doabit/semantic-ui-sass) and copy the configuration to gemfile and add jquery as well
```
gem 'semantic-ui-sass'
gem 'jquery-rails'
```
save and go to terminal, run "bundle install"  

- add css and js
create custom.css.scss under app/assets/stylesheet/ 
```
@import 'semantic-ui';
```
and in app/assets/javascript/application.js add require jquery and semantic ui
```
//= require rails-ujs
//= require jquery
//= require activestorage
//= require turbolinks
//= require semantic-ui
//= require_tree .
```
the sequence of required dependencies is very important, otherwise doesn't work.  

- Add nav bar
In semantic ui website, find the nav bar needed, copy the source code and add to views/layouts/application.html.erb
```
<div class="ui small inverted menu">
  <div class="ui container">
    <a class="item">
      Home
    </a>
    <a class="item">
      Messages
    </a>
    <div class="right menu">
      <div class="ui dropdown item">
        Language <i class="dropdown icon"></i>
        <div class="menu">
          <a class="item">English</a>
          <a class="item">Russian</a>
          <a class="item">Spanish</a>
        </div>
      </div>
      <div class="item">
        <div class="ui primary button">Sign Up</div>
      </div>
    </div>
  </div>  
</div>
<div class="ui container">
  <%= yield %>
</div>
```
"ui small inverted menu": the nav bar mode and inverted indicate color inverting. added "ui container" to add indent and adjust the layout.  By adding container, you can adjust the layout.   

- Add turbolink:  
**Turbolinks** is a flexible and lightweight JavaScript library aimed to make your navigation through webpages faster, in app/assets/javascripts/applicaiton.js, add code as below. (Be aware we're using rails5, so javascript folder is under assets)  
```
//= require turbolinks
//= require semantic-ui
//= require_tree .

$(document).on('turbolinks:load', function() {
  $('.ui.dropdown').dropdown();
})
```
Before adding turbolink, the dropdown link is not clickable, after loading turbolink, it works.   

- Edit navigation menu and move to new created _navigation.html.erb (omit)  
- Add favicon using 
  - find out resource:  [awesome favicon](https://gauger.io/fonticon/) select coffee, and set up color to red with black background, then download, add to app/assets/images
  - Add to source, in application.html.erb, add under <title>, asset_path can be omitted if only on icon exist. 
  ```
    <title>MessageMe</title>
    <%= favicon_link_tag asset_path('favicon.ico') %>
  ```
