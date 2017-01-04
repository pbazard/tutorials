How to build a Node web application
########

Project setup
*****
Create your project with 

  npm init

Create a server.js file

  touch server.js
 
Install Express
  
  npm install express --save
  
If you want to restart the server automatically, install Nodemon

  npm install nodemon --save-dev
  
and create a script key in the package.json file
  .. code-block:: ini
    {
    // ...
    "scripts": {
      "dev": "nodemon server.js"
      }
    // ...
    }
  
Then you can run npm run dev to trigger nodemon server.js. Node will reload changed resources on the fly.

Static resources
*****

Data model
*****

REST Api
*****
