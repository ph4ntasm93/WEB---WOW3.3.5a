# WEB---WOW3.3.5a
This is a website built for the World of Warcraft 3.3.5 expansion, specifically AzerothCore.


⚠️This project is written for wamp server. If you use another server app, something may not work.⚠️


This is not a finished project so it still needs improvement. In some places there may be non-optimal solutions so it may be difficult to understand, please take this into account. 
Some things about the project:

💳 I have integrated the stripe system in the support section, you only need to add the token and it works.

🔐 The registration uses SRP.

⭐ The VIP / premium system is very simple. I created an extra field (vip) in the server core account, if this is set to 1 for the given user, the user will be promoted to VIP rank. I used this by writing a lua script in the game so that only those with VIP rank can use the shop in the game. Maybe I will share this shop with you.

🔐 Password change is email-based. I used phpmailer for this, which you can set in the config. 

⚙️ Config, or configs... Well, there are several configs in this project, so there is not just one global one! There are 4 configs in total. The admin panel uses two. There is one for messages and one for main config. This also applies to the non-admin panel, in the core folder there is one and the other for messages. It is important to adapt these to your own server. Now the question may arise why so many are needed? Well, some things were added later and therefore there was a problem accessing the configs in some places (I don't understand either). 

📌 As I mentioned above, there are some non-optimal solutions, and the project may be quite difficult to understand, but I will gradually update these.



🛠️ HOW TO USE:

🛒Shop System

 • server_character (database) → item_instance table → set the guid field to AUTO INCREMENT.
 
 • server_character (database) → mail_items table → set the item_guid field to AUTO INCREMENT.
 
 • server_character (database) → mail table → set the id field to AUTO INCREMENT.
 
 
⭐VIP System

 • server_auth (database) → accounts table → add a new field named vip (INT NOT NULL DEFAULT).

🛠️ 404 Error Code
 • If .htaccess is disabled: this is very important due to the 404 error and preventing access to the root directory.
 
 • Find this section in the Apache config (httpd.conf):
 
   <Directory />
      AllowOverride none
      Require all denied
   </Directory>
   
  • Change it to:
    <Directory />
     AllowOverride All
     Require all denied
   </Directory>
   
• Find this:
  #ErrorDocument 404 /404.html
  
 • Change it to:
   ErrorDocument 404 /404.php
   
🧍Armory System
  Stats will only work if character stats are saved in the database.
  To do this, make the following 2 modifications in worldserver.conf:
 
 Changes:
 
 ❌ PlayerSave.Stats.MinLevel = 0  
 
 ✅ PlayerSave.Stats.MinLevel = 1
 
 ❌ PlayerSave.Stats.SaveOnlyOnLogout = 1
 
 ✅ PlayerSave.Stats.SaveOnlyOnLogout = 0
 
   
🔌 SOAP COMMAND

 • To send GM commands via web: enable SOAP.Enabled in worldserver.conf.
 
 • This requires a gm account which can be set up in core/armory/armory.php

📎Other

 • The web admin panel is accessible if in the server_site database, in the users table, the security_key = 1.
 • In this case, the admin button will appear in the profile.
