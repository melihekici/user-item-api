# user-item-api

## Build

    sudo docker-compose build

## Run

    sudo docker-compose up

# REST API
  In this application, there is a database that holds users.
  For each user, "username", "password" and "items" are hold in the database.
  "items" field is a list that keeps a list of dictionaries, each dictionary is an item.
  
  ## Register
    Register to the api with a username and password.
    
    ### Request:
    POST http://0.0.0.0:5000/register
    {
      "username": "username",
      "password": "password"
    }
    
    ### Response:
    {
      "msg": "You have successfuly registered to the API",
      "status": 200
    }
    
  ## Login
    Login to the API with username and password. Will return a token.
    
    ### Request:
    POST http://0.0.0.0:5000/login
    {
      "username": "username",
      "password": "password"
    }
    
    ### Response:
    {
      "msg": "You have signed in successfuly.",
      "status": 200,
      "token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VybmFtZSI6InVzZXJuYW1lIn0.PVpC0ZYLyPhvEjFGdNqWd2TTTsxs7JxNprOduJkF11I"
    }
  
  ## Get Items
    Returns the item list of the user. Token is passed with a POST request
    
    ### Request:
    POST http://0.0.0.0:5000/getItems
    {
      "access-token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VybmFtZSI6InVzZXJuYW1lIn0.PVpC0ZYLyPhvEjFGdNqWd2TTTsxs7JxNprOduJkF11I"
    }
    
    ### Response:
    {
      "currentUser": "username",
      "items": [],
      "msg": "Item list has been fetched successfuly.",
      "status": 200
    }
 
 ## Add, Edit, Delete, Get Items
    Using this endpoint you can Add items, Change an existing item, Delete an item and show your item list.
    
    ### Request: (Adding a new item)
    POST http://0.0.0.0:5000/items
    {
      "name": "Pokeball",
      "count": 20,
      "description": "Pokeballs are used to capture pokemons.",
      "access-token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VybmFtZSI6InVzZXJuYW1lIn0.PVpC0ZYLyPhvEjFGdNqWd2TTTsxs7JxNprOduJkF11I"
    }
    
    ### Response:
    {
      "msg": "Item has been added successfuly.",
      "status": 200
    }
    
    
    ### Request: (Displaying your items)
    Get http://0.0.0.0:5000/items?access-token=<Your access token>
    
    ### Response:
    {
      "currentUser": "username",
      "items": [
          {
              "count": 20,
              "description": "Pokeballs are used to capture pokemons.",
              "name": "Pokeball"
          }
      ],
      "msg": "Item list has been fetched successfuly.",
      "status": 200
    }
    
    ### Request: (Changing item values)
      You have used 10 of your pokeballs and you were not able to catch anything.
      Now you want to update both your pokeball count and description.
      
    PUT http://0.0.0.0:5000/items
    {
      "name": "Pokeball",
      "count": 10,
      "description": "Pokeballs are used to capture pokemons. They dont seem very successful though",
      "access-token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VybmFtZSI6InVzZXJuYW1lIn0.PVpC0ZYLyPhvEjFGdNqWd2TTTsxs7JxNprOduJkF11I"
    }
    
     Additional Info:
      "new-name" -> You can send this if you want to change the name as well. It is Optional
      "count" -> This is optinal. If not sent, the count wont be updated.
      "description" -> This is optional, if not sent, the description wont be updated.
      
    ### Response
    {
      "msg": "Item has been updated successfuly.",
      "status": 200
    }
    
    
    ### Request: (Delete item)
    DELETE http://0.0.0.0:5000/items
    {
      "name": "Pokeball",
      "access-token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VybmFtZSI6InVzZXJuYW1lIn0.PVpC0ZYLyPhvEjFGdNqWd2TTTsxs7JxNprOduJkF11I"
    }
    
    ### Response
    {
      "msg": "Item has been deleted successfuly.",
      "status": 200
    }
