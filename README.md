mkdir auth-system
cd auth-system
npm init -y
npm install express pg bcryptjs jsonwebtoken body-parser
npm install dotenv

## Installing and Starting PostgreSQL
brew install postgresql@14
brew services start postgresql@14
brew services list
psql -U xkolz -d postgres

## Create the dababase & table
CREATE DATABASE authdb;

CREATE TABLE users (
  id SERIAL PRIMARY KEY,
  username VARCHAR(50) UNIQUE NOT NULL,
  email VARCHAR(100) UNIQUE NOT NULL,
  password VARCHAR(255) NOT NULL,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

## Verify that the table has been created by running:
\dt

## View All Data in the users Table:
SELECT * FROM users;

## Exit the PostgreSQL Shell:
\q

## Access the users Table:
In the left sidebar, expand your server, 
then the database "postgres", then "Schemas", then "public", then "Tables".
Right-click on the users table and select "View/Edit Data" > "All Rows".
Then you will see a table view with all the data in the users table.

## Create a .env
PORT=3000
DB_USER=
DB_HOST=
DB_NAME=
DB_PASSWORD=
DB_PORT=
JWT_SECRET=your_jwt_secret

## Test the db is connected
curl http://localhost:3000/api/auth/test-db


## Register 
    curl -X POST http://localhost:3000/api/auth/register \
    -H "Content-Type: application/json" \
    -d '{
    "username": "testuser",
    "email": "testuser@example.com",
    "password": "testpassword"
    }'

## Login
    curl -X POST http://localhost:3000/api/auth/login \
    -H "Content-Type: application/json" \
    -d '{
    "email": "testuser@example.com",
    "password": "testpassword"
    }'
