# Workshop NodeJS MongoDB

In this workshop you will learn how to create a express server CRUD with mongoDB.

# Prerequisite

You can work on Linux or Windows as you want.

- **Programing Language :** [NodeJS] [Install it!](https://nodejs.org/en/download/current)

- **Database :** [MongoDB community] [Install it!](https://www.mongodb.com/docs/manual/administration/install-community/)

- **Tool view your database :** [MongoDB compass] [Install it!](https://www.mongodb.com/docs/compass/current/install/)

- **Tool to make request :** [Postman] [Install it!](https://learning.postman.com/docs/getting-started/installation/installation-and-updates/) or [Insomnia] [Install it!](https://insomnia.rest/download)

## 📚 **Documentation**:

- [ExpressJS](https://expressjs.com/fr/)
- [Mongoose](https://mongoosejs.com/docs/)

# Init project

```
mkdir node-express-mongodb
cd node-express-mongodb
npm init -y
```

## Dependencies

#### Install Express

```
npm install express --save
```

#### Install Mongoose

```
npm install mongoose --save
```

#### Install Nodemon

```
npm install nodemon --save-dev
```

#### In package.json add this line:

```javascript
"scripts": {
  "start": "nodemon app.js"
}
```

## Step 0 - Create express server

### 📌 **Tasks**:

#### Create a file named app.js and code your express server in

```
touch app.js
```

- Set the port to 8080

- Create a GET request at the root ("/") that returns 'Welcome to NodeJS MongoDB workshop'

#### Start server

```
node app.js
App listening on port 8080
```

#### Test your server

Navigate to http://localhost:8080/ and it should display :

```
Welcome to NodeJS MongoDB workshop
```

### 📚 **Documentation**:

- [How to create a express server](https://expressjs.com/en/starter/hello-world.html)

## Step 1 - Connect to mongoDB

### 📌 **Tasks**:

#### Write your code in [mongodb.js](./node-express-mongodb/mongodb.js) to connect your server to mongodb

- Complete the function **connectToMongoDB** in [mongodb.js](./node-express-mongodb/mongodb.js)
- In [app.js](./node-express-mongodb/app.js) import the function **connectToMongoDB** and use it

#### Start server

```
node app.js
Connected to MongoDB
App listening on port 8080
```

### 📚 **Documentation**:

- [How to connect to mongoDB](https://mongoosejs.com/docs/)

## Step 2 - Create route for CRUD

### 📑 **Description**:

#### In order to make the CRUD we will need to create 4 route

### 📌 **Tasks**:

- CREATE

  - `("transaction/")` **POST** request, create a transaction
  - The request should have this body

  ```
  {
    "name": String,
    "description": String,
    "amount": Number,
  }
  ```

  - Try to print the body when making the request

- READ

  - `("transaction/")` **GET** request, get a single transaction
  - Try to print a message

- UPDATE

  - `("transaction/:id")` **PUT** request, update single transaction
  - Try to print the id passed in the request. (_this is a params_)

- DELETE
  - `("transaction/:id")` **DELETE** request, delete a transaction
  - Try to print the id passed in the request. (_this is a params_)

### 📚 **Documentation**:

- [What is a CRUD ?](https://en.wikipedia.org/wiki/Create,_read,_update_and_delete)
- [How to create a CRUD express.](https://dev.to/ericlecodeur/nodejs-express-partie-4-creer-un-crud-api-4mn5)

## Step 3 - Test your routes

### 📑 **Description**:

#### In order to test your routes you need to make request to your server

#### To do this you need to install postman or insomnia

### 📌 **Tasks**:

Run your server:

```javascript
npm start
```

Send HTTP request to these url:

```javascript
POST http://localhost:8000/transaction/
body : {
  name,
  description,
  amount
}
```

```javascript
GET http://localhost:8000/transaction/
```

```javascript
PUT http://localhost:8000/transaction/:name
body: {
  newDescription,
  newAmount,
}
```

```javascript
DELETE http://localhost:8000/transaction/:name
```

### 📚 **Documentation**:

- [Postman](https://learning.postman.com/docs/sending-requests/requests/)
- [Insomnia](https://docs.insomnia.rest/insomnia/send-your-first-request)

## Step 4 - Create a Schema and Model

### 📑 **Description**:

#### In order to our save data properly we need to create a Schema and a Model

### 📌 **Tasks**:

- Create a **models** folder.
- Create a **transaction.js** file and write your schema in the file.
- Create a mongoose schema named **transactionSchema** that contains :

  - **title :** _title of the transaction_.

  ```javascript
  [type: String, required: true]
  ```

  - **description :** _description of the transaction_.

  ```javascript
  [type: String, required: true]
  ```

  - **amount :** _amount of the transaction_.

  ```javascript
  [type: String, required: true]
  ```

- Once the schema is created, create a Model with the schema.

#### To check if you have completed this step successfully, run your server and open MongoDB Compass. You should see your collection appear.

### 📚 **Documentation**:

- [How to create a mongoose Schema](https://mongoosejs.com/docs/guide.html#definition)
- [How to create a mongoose Model](https://mongoosejs.com/docs/guide.html#models)

## Step 5 - Create function for MongoDB

### 📌 **Tasks**:

#### Create 4 function in [mongodb.js](./node-express-mongodb/mongodb.js) to interact with your database:

- Create a transaction, should return the created transaction.
  ```javascript
  async function createTransaction(name, description, amount) {}
  ```
- Read transactions, should return all the transaction.
  ```javascript
  async function readTransactions() {}
  ```
- Update transaction, should return the updated transaction.
  ```javascript
  async function updateTransaction(name, newDescription, newAmount) {}
  ```
- Delete transaction, should return the deleted transaction.

  ```javascript
  async function deleteTransaction(name) {}
  ```

  ### 📚 **Documentation**:

- [Mongo Queries](https://mongoosejs.com/docs/queries.html)
- [Mongo Models](https://mongoosejs.com/docs/models.html)

## Step 6 - Connect functions to your routes

### 📑 **Description**:

#### Now you have your function that can create, read, update and delete transaction from the database<br>Its time to use it with the server.

### 📌 **Tasks**:

#### Add the function you created in the previous step in your route :

- <u>**POST** `("transaction/")` + `createTransaction(name, description, amount)` </u>

  - Retrieve data from the request body :
    - name
    - description
    - amount
  - Send these data to the function and return the value returned by the `createTransaction` function.
  - It create a transaction in the database and should return the created transaction.

- <u>**GET** `("transaction/")` + `readTransactions()` </u>

  - No data needed just call the function and return the value returned by the `readTransactions` function
  - It should read all transaction from the database and return the all the transaction.

- <u>**PUT** `("transaction/:name")` + `updateTransaction(name, newDescription, newAmount)` </u>

  - Retrieve name from the request params :

    - name

  - Retrieve data from the request body :

    - newDescription
    - newAmount

  - Send the these data to the function and return the value returned by the `updateTransaction` function.
  - It should update the transaction in the database and return the updated transaction.

- <u>**DELETE** `("transaction/:name")` + `deleteTransaction(name)`</u>

  - Retrieve name from the request params :

    - name

  - Send the these data to the function and return the value returned by the `deleteTransaction` function.

  - It should delete the transaction from the database and return the deleted transaction.

### 📚 **Documentation**:

- [How to create a CRUD express](https://dev.to/ericlecodeur/nodejs-express-partie-4-creer-un-crud-api-4mn5)

## Conclusion

You just create a NodeJS API with expressJS, that can create, read, update and delete from mongoDB.

I hope you enjoyed the workshop!

## Authors

| [<img src="https://media.licdn.com/dms/image/D4E03AQE315c6WOIgAA/profile-displayphoto-shrink_400_400/0/1683929826391?e=1707350400&v=beta&t=4MxlKmuKo9vIduelZG7lOZ39q8v0wFlv3pNJjT9DTtQ" width=120><br><sub>Joseph Yu</sub>](https://github.com/Jouzep) |
| :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: |
