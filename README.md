# Technical document for Location-based Quiz system
The system comprise of 2 client side applications and a webserver.
- <a href = "https://github.com/woravich-k/quiz">Location-based Quiz application (client)</a>
- <a href = "https://github.com/woravich-k/questions">Question Setting application (client)</a>
- <a href = "https://github.com/woravich-k/server">NodeJS Webserver (server)</a>



# To further develop the application
## Language
Server
- JavaScript (NodeJS)
- SQL Query

Client
- HTML (for the structure)
- CSS (for styling)
- JavaScript (for actions)
  - leaflet is used as a library for mapping objects
  
## Reference
Server
- <a href = "http://www.postgresonline.com/journal/archives/267-Creating-GeoJSON-Feature-Collections-with-JSON-and-PostGIS-functions.html,">Postgres Online Journal</a>
  - for query returning GeoJSON text
- practicals of UCL, CEGEG077: Web and Mobile GIS - Apps and Programming, 2017/2018
  - for POST and GET methods

Client
- <a href = "https://getmdl.io/templates/index.html"> Material Design Lite</a>
  - for web template and CSS design
- <a href = "https://www.w3schools.com/howto/howto_css_switch.asp"> W3 School</a> 
  - for toggle switches CSS
- <a href = "https://www.htmlgoodies.com/beyond/javascript/calculate-the-distance-between-two-points-in-your-web-apps.html"> Rob Gravelle</a>
  - for calculate distance function
- practicals of UCL, CEGEG077: Web and Mobile GIS - Apps and Programming, 2017/2018
  - for general uses of JavaScript, such as AJAX, requesting POST and GET
  
## Database Table
There are three tables used in this system. The SQL statements creating these tables are uploaded to this repository
  
  - question: a table of questions
  field: id (primary key) (number)
         question, choice1, choice2, choice3, choice4 (text) - store question and choices
         qurl, choice1url, choice2url, choice3url, choice4url (text) (optional) - image URLs of the additional information of question and choices
         answer (text) - the correct answer as "choice1", "choice2", "choice3", "choice4"
         fullanswer (text) - the full answer of the correct choice
         geom (unique) (geometry) - the GCS WGS 1984(espg:4326) coordinates
         
  - account_web: a table of users' accounts
  filed: id (primary key) (number)
         username (text) - the username of the account
         password (text) - the password of the account
         
    - user_ans: a table of history answers of all accounts
  filed: id (primary key) (number) 
         accountid (unique) (number) - id of the account that anwser the question
         questionid (number) - id of the question that is anwsered by the account
         userans (text) - the user's answer
         truefalse (boolean) - indicate correct or incorrect answer
         
## Overview functions

         
  





# To deploy this system

## hardward
Server
a database server and a webserver are needed.

Client
an moblie device


## software
Server
- Postgres SQL on database server
- NodeJS on webserver (the system is tested on version v8.9.3 operating on Ubuntu 16.04.2 LTS)
  - some libraries are needed - i.e. express, path, https, fs, body-parser, pg
  
Client
- The applications are designed to be platform independent deployed by phonegap; however they have been tested on only Android v.6.0.1.

## Certificate
Since this system is served via https protocol, a SSL certificate is needed. However the code could be adated to serve via http protocol.


##


# server
A server side code for location-based application ; working together with 'quiz' and 'questions' repositories
