# Technical document for Location-based Quiz system
The system comprise of 2 client side applications and a webserver.
- <a href = "https://github.com/woravich-k/quiz">Location-based Quiz application (client)</a>
- <a href = "https://github.com/woravich-k/questions">Question Setting application (client)</a>
- <a href = "https://github.com/woravich-k/server">NodeJS Webserver (server)</a>

# To deploy this system
## Deploy
Phonegap V.7.1.1 as a deployment of the client side applications

## Hardware
Server
a database server and a webserver are needed.

Client
an moblie device


## Software
Server
- Postgres SQL on database server
- NodeJS on webserver (the system is tested on version v8.9.3 operating on Ubuntu 16.04.2 LTS)
  - some libraries are needed - i.e. express, path, https, fs, body-parser, pg
  
Client
- The applications are designed to be platform independent deployed by phonegap; however they have been tested on only Android v.6.0.1.

## Certificate
Since this system is served via https protocol, a SSL certificate is needed. However the code could be adapted to serve via http protocol.



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
    - id (primary key) (number)
    - question, choice1, choice2, choice3, choice4 (text) - store question and choices
    - qurl, choice1url, choice2url, choice3url, choice4url (text) (optional) - image URLs of the additional information of question and choices
    - answer (text) - the correct answer as "choice1", "choice2", "choice3", "choice4"
    - fullanswer (text) - the full answer of the correct choice
    - geom (unique) (geometry) - the GCS WGS 1984(espg:4326) coordinates         
    
  - account_web: a table of users' accounts
    - id (primary key) (number)
    - username (unique) (text) - the username of the account
    - password (text) - the password of the account
         
  - user_ans: a table of history answers of all accounts --> unique (accountid,questionid)
    - id (primary key) (number) 
    - accountid  (number) - id of the account that anwser the question
    - questionid (number) - id of the question that is anwsered by the account
    - userans (text) - the user's answer
    - truefalse (boolean) - indicate correct or incorrect answer
         
## Overview functions from JavaScript
### Server: httpsServer.js
  - GET 
    - get GeoJSON string of the table order by id (/getGeoJSON/:tablename/:geomcolumn)
    - get a list of the question and the history answer of the specified user as GeoJSON (/getQuestionANS/:id) 
      - the result is equal to " select a.*, b.* from question a left join (select * from user_ans c where c.accountid = id) b on a.id = b.questionid"
    - delete the question by specifying id(/deleteRow/:tablename/:id)
  - POST
    - Create new question (/uploadQuestion)
    - Edit question by posting attributes and id (/editQuestion)
    - Create account (/createAcc)
    - Record user's answer (/postAns)
    - Validate the login requesting by "select" query (/postAns)
      - Select count(*) from account_web where username = posted username and password = posted password
      - valid login result == 1; invalid login result == 0
 
 ### Client: Question
 the script is devided as two separated files according to the purpose of functions
 ### Client: Question - uploadData.js
 The JavaScript functions in this file are for manipulating data i.e. create, edit, delete question and loading leaflet map.
  - in order to manipulate data, the functions for recieving users' inputs are in this file.
  - POST functions to create, edit, delete
  
 ### Client: Question - main.js
 

 
         
  







##


# server
A server side code for location-based application ; working together with 'quiz' and 'questions' repositories
