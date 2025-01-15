## Table of Contents
- **[Getting Started](#getting-started)**<br>
- **[Installing](#installing)**<br>
- **[Overview](#overview)**<br>
- **[Back-end](#back-end)**<br>
- **[API Endpoints](#api-endpoints)**<br>
- **[Register Endpoint](##register-endpoint)**<br>
- **[Login Endpoint](##login-endpoint)**<br>
- **[Logout Endpoint](##logout-endpoint)**<br>
- **[Campaign Endpoints](##campaign-endpoint)**<br>
- **[Metrics Endpoints](##metrics-endpoints)**<br>

# backend-api
Back-end REST API

# Getting Started

These instructions will get you a copy of the project up and running on your local machine for development and testing purposes. See deployment for notes on how to deploy the project on a live system.

# Installing

A step by step series of examples that tell you how to get a development environment running
`cd` into `server` folder and install dependencies with:

1. Clone the repository:
   - git clone https://github.com/kaspares/projekt-api.git
2. Open terminal and install dependencies:
   - npm install
3. Create file .env and write:
   DB_USER= <yourname>
   DB_PASSWORD= <yourpassword>
   DB_NAME= <databasename>
   JWT_KEY= <secret>
4. Create connection to your database
5.Then launch the api with: 
nodemon server.js

# Overview
- The application allows you to manage parcel lockers, parcels, and couriers. Users can create, edit, and delete parcel lockers, parcels, and assign couriers. The system provides easy tracking of parcels and organizing their delivery.
  <strong>Functioncs:</strong>
  - Creating and managing parcel lockers
  - Creating and managing parcels
  - Adding, editing, and deleting couriers
  - Assigning parcels to parcel lockers and couriers
  - Checking which parcels are in a specific parcel locker

# Back-end 

<strong>API's</strong>

The back-end exposes a set of RESTful API endpoints to interact with parcel lockers, parcels, and couriers. These endpoints allow users to create, read, update, and delete the necessary data. The API also supports querying for parcels in specific parcel lockers and assigning couriers to parcels.

<strong>RDBMS and Data Persistence</strong>

The application uses MongoDB with Mongoose for data storage and management. MongoDB is a NoSQL database that stores data in a flexible, JSON-like format. Mongoose is used to define schemas and models for the different entities, such as parcel lockers, parcels, and couriers, and handle interactions with the database. All data is persisted in MongoDB, ensuring future retrieval and analysis.

<strong>Authentication</strong>

The application implements authentication mechanisms, such as JWT (JSON Web Tokens), to ensure that only authorized users can access or modify data (e.g., creating or updating parcels or lockers). Users must log in to receive an authentication token, which they include in the header of their API requests.

# API Endpoints
Use Base URL: http://localhost:3000/

Register & Login 
| Method | Route                  | Description                                      |
|--------|------------------------|--------------------------------------------------|
| POST   | /api/auth/register     | registers new users                              |
| POST   | /api/auth/login        | logins into user account                         |
| GET    | /api/auth/logout       | logs out of user account                         |

Campaigns
| Method | Route                  | Description                                      |
|--------|------------------------|--------------------------------------------------|
| GET    | /api/campaigns         | returns array of campaigns in database           |
| GET    | /api/campaigns/:id     | returns campaigns specified by :id  --NOT READY  |
| PUT    | /api/campaigns/:id     | updates campaign specified by :id                |
| POST   | /api/campaigns         | creates & returns new campaign                   |
| DELETE | /api/campaigns/:id     | deletes campaign specified by :id                |


Users
| Method | Route                  | Description                                      |
|--------|------------------------|--------------------------------------------------|
| GET    | /api/users             | returns array of users                           |
| GET    | /api/users/:id         | returns user specified by :id                    |
| PUT    | /api/users/:id         | updates user specified by :id                    |
| DELETE | /api/user/:id          | deletes user specified by :id                    |

Metrics
| Method | Route                      | Description                                  |
|--------|----------------------------|----------------------------------------------|
| POST   | /api/campaigns/:id/metrics | returns array of photos                      |
<!-- | GET    | /api/photos/:id       | returns photos specified by :id                   |
| POST   | /api/photos           | creates & returns new story                       |
| PUT    | /api/photos/:id       | updates photos specified by :id                   |
| DELETE | /api/photos/:id       | deletes photos specified by :id                   | -->


## Register Endpoint
```js
POST /api/auth/register
```
Expected Body 
```js
    {
    "username": "new_user", // string, unique, required
    "password": "password", // string, required
    "age": 18, // integer, required
    "email": "JaneDoe@gmail.com" // string, unique, required
    }
```

Expected Response
```js
    {
        "id": 4,
        "username": "new_user",
        "password": "$2a$08$Sp/WntMm7eAZnDn3tp40tOAp77T8CTMUel8bqZGD3CoJcuSrH.NZ6",
        "email": "JaneDoe@gmail.com",
        "age": 18
    }
```

## Login Endpoint
```js
POST /api/auth/login
```
Expected Body
```js
{
    "username": "test_user",
    "password": "password"
}
```
Expected Response
```js
{
    "message": "Welcome test_user",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWJqZWN0IjoxMiwidXNlcm5hbWUiOiJuZXdfdXNlcjEyMTIxMiIsImlhdCI6MTU5ODQyMDg0NywiZXhwIjoxNTk4NDI4MDQ3fQ.YyR_rrRxYaDVTt3FPM155hPwbUAEFhyaDSOWqVOD8kM"
}
```

## Kurier Endpoints
### GET All kurierzy
```js
GET http://localhost:3000/kurierzy

Expected Response: returns array of kurierzy in database 
{
    "wiadomość": "Liszta wszystkich kurierów",
    "kurierzy": [
        {
            "_id": "677eecaf3fdb91fe83c2cc83",
            "imie": "Julia",
            "nazwisko": "Kowalska",
            "__v": 0
        }
    ]
}
```

### POST kurierzy
```js
POST http://localhost:3000/kurierzy

Expected Body: 
{
    imie: String,
    nazwisko: String
})
Expected Response: returns object of created kurierzy in database 

{
    "wiadomość": "Nowy kurier został dodany!",
    "kurier": {
        "_id": "678819627e7d7c268866b9cc",
        "__v": 0,
	imie: "Ania", //name example
	nazwisko: "Kowalska", //surname example
    }
}
```

### PUT kurierzy By ID
```js
PUT http://localhost:3000/kurierzy/677eecaf3fdb91fe83c2cc83

{
    "wiadomość": "Nie odnaleziono"
}

Expected Response: updates campaign specified by :id

PUT http://localhost:3000/kurierzy/id
{
    "wiadomość": "Zaktualizowano kuriera o numerze 677eecaf3fdb91fe83c2cc83",
    "updatedKurier": {
        "_id": "677eecaf3fdb91fe83c2cc83",
        "imie": "Julia",
        "nazwisko": "Kowalska",
        "__v": 0
    }
}

```

### DELETE kurierzy by ID
```js
DELETE  http://localhost:3000/kurierzy/id

Expected Response: deletes kurierzy specified by :id

Expected Response: 
    {
    "wiadomość": "Usunięto kuriera o numerze 677eecaf3fdb91fe83c2cc83"
}
```

## paczkomaty Endpoints
### GET All paczkomaty
```js
GET http://localhost:3000/paczkomaty

Expected Response: returns array of paczkomaty in database 
{
    "wiadomość": "Lista wszystkich paczkomatów",
    "paczkomaty": [
        {
            "_id": "677eed933fdb91fe83c2cc8b",
            "miasto": "Płock",
            "adres": "Klonowa 1",
            "pojemnosc": 20,
            "__v": 0
        }
    ]
}
```

### POST paczkomaty
```js
POST http://localhost:3000/paczkomaty

Expected Body: 
{
    miasto: String,
    adres: String,
    pojemnosc: Number
}
Expected Response: returns object of created kurierzy in database 

{
    "wiadomość": "Nowy paczkomat został dodany!",
    "paczkomat": {
        "_id": "67881d0e7e7d7c268866b9d5",
        "miasto": "Puck", // city example
        "adres": "Wolna", // adress example
        "pojemnosc": 10, // capacity example
        "__v": 0
    }
}
```

### PUT paczkomaty By ID
```js
PUT http://localhost:3000/paczkomaty

{
    "wiadomość": "Nie odnaleziono"
}

Expected Response: updates campaign specified by :id

PUT http://localhost:3000/paczkomaty/67881d0e7e7d7c268866b9d5
{
    "wiadomość": "Zaktualizowano paczkomat o 67881d0e7e7d7c268866b9d5",
    "updatedPaczkomat": {
        "_id": "67881d0e7e7d7c268866b9d5",
        "miasto": "Puck",
        "adres": "Wolna",
        "pojemnosc": 10,
        "__v": 0
    }
}

```

### DELETE paczkomaty by ID
```js
DELETE  http://localhost:3000/paczkomaty/67881d0e7e7d7c268866b9d5

Expected Response: deletes paczkomaty specified by :id

Expected Response: 
{
    "wiadomość": "Usunięto paczkomat o numerze 67881d0e7e7d7c268866b9d5"
}
```

## paczki Endpoints
### GET All paczki
```js
GET http://localhost:3000/paczki

Expected Response: returns array of paczki in database 
{
    "wiadomość": "Lista wszystkich przesyłek",
    "paczki": [
        {
            "_id": "677eef763fdb91fe83c2cca0",
            "kodPaczki": "123",
            "kurier": null,
            "paczkomat": {
                "_id": "677eed933fdb91fe83c2cc8b",
                "miasto": "Płock",
                "adres": "Klonowa 1"
            },
            "status": "dostarczona",
            "__v": 0
        },
        {
            "_id": "677f7827382767cc994affd0",
            "kodPaczki": "ABC123",
            "kurier": null,
            "paczkomat": {
                "_id": "677eed933fdb91fe83c2cc8b",
                "miasto": "Płock",
                "adres": "Klonowa 1"
            },
            "status": "dostarczona",
            "__v": 0
        }
    ]
}
```

### POST paczki
```js
POST http://localhost:3000/paczki

Expected Body:
{
    kodPaczki: String, 
    kurier: {
	kurierId: "534563456345e63456"
        ref: "Kurier" 
    },
    paczkomat: {
	paczkomatId: "4524456576889667467"
        ref: "Paczkomat" 
    },
    status: String 
}
Expected Response: returns object of created kurierzy in database 

{
    "wiadomość": "Nowy kurier został dodany!",
    "kurier": {
        "_id": "678819627e7d7c268866b9cc",
        "__v": 0,
	imie: "Ania", //przykład
	nazwisko: "Kowalska",
    }
}
```

### PUT paczki By ID
```js
PUT http://localhost:3000/paczki

{
    "wiadomość": "Nie odnaleziono"
}

Expected Response: updates campaign specified by :id

PUT http://localhost:3000/paczki/id
{
    "wiadomość": "Zaktualizowano paczke o numerze 677eef763fdb91fe83c2cca0",
    "updatedPaczka": {
        "_id": "677eef763fdb91fe83c2cca0",
        "kodPaczki": "123",
        "kurier": "677eecaf3fdb91fe83c2cc83",
        "paczkomat": "677eed933fdb91fe83c2cc8b",
        "status": "dostarczona",
        "__v": 0
    }
}

```

### DELETE paczki by ID
```js
DELETE  http://localhost:3000/paczki/id

Expected Response: deletes campaign specified by :id

Expected Response: 
    {
    "wiadomość": "Usunięto paczke o numerze 677eef763fdb91fe83c2cca0"
}
```

