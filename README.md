# Backend Folder Structure and Microservice Architecture

## Overview

This project follows a microservices-based architecture, where each feature is separated into a distinct service, with individual Node.js servers and databases for each service.

## Project Initialization

To initiate a new service, follow these steps:

1. **Create a New Folder:** Create a new folder with the desired service name.
2. **Initialize NPM Project:** Run `npm init` to initialize a new npm project.
3. **Install Dependencies:**
   - `express`: A framework for creating an Express server.
   - `body-parser`: Middleware for parsing incoming request bodies.
   - `nodemon`: A tool for automatically restarting the server during development.

Project structure includes separate `src` and `tests` folders:

- `src/`: Contains the main application logic and files for deployment.
  - `index.js`: Entry point for the application.
  - `models/`: Stores data models.
  - `migrations/`: Manages database schema changes.
  - `controllers/`: Handles request-response logic.
  - `middlewares/`: Contains middleware functions.
  - `utils/`: Houses utility functions.
  - `config/`: Holds configuration files.
  - `services/`: Implements business logic.
  - `repository/`: Manages data access logic.
  - `seeders/`: Populates the database with initial data.
  - `routes/`: Defines API routes.

- `tests/`: Contains test files.
- `package.json`: Project configuration file.
- `package-lock.json`: Records the exact version of each installed package.
- `.gitignore`: Specifies files and directories to be ignored by version control.

## Setting Up Basic Express Server

1. **Set Up Express Server:** Establish a basic Express server.
2. **Install dotenv:** Use `npm i dotenv` to install dotenv, a zero-dependency module for loading environment variables.
3. **Create `.env` File:** Create a `.env` file in the root folder to store environment variables. Ensure that it is added to the `.gitignore` file.
4. **Configure dotenv:** Set up dotenv in the `config` folder by creating a `serverConfig.js` file. Refer to the documentation for further setup.

## Setting Up Sequelize (ORM for MySQL)

1. **Install Sequelize and MySQL Dependencies:** Run `npm i mysql2 sequelize sequelize-cli` to install Sequelize and MySQL dependencies.
2. **Initialize Sequelize:** Run `npx sequelize init` to generate the necessary folders (`config`, `migrations`, `models`, `seeders`).
3. **Configure Sequelize:** Edit `config/config.json` with local MySQL server details and create a database using `npx sequelize db:create` in the `src` folder.

## Creating Models

1. **Generate Model:** In the `src` folder, run `npx sequelize model:generate --name <Model Name> --attributes <Schemas>:<type>` to generate a model.
2. **Run Migrations:** Execute `npx sequelize db:migrate` to run migrations and create a table in the local database.
3. **Undo Migrations:** Use `npx sequelize db:migrate:undo` to undo migrated files.

## Repository and Service Layers

1. **Repository Layer:** In the `repository` folder, create a `<Model Name>` repository file for CRUD operations.
2. **Export Repositories:** Create an `index.js` file in the `repository` folder to export all repositories as a single object.
3. **Service Layer:** Repeat the same structure for the `services` folder.

## Database Structure

1. **Create Model:** Begin by creating a model.
2. **Repository Layer:** Create a file in the `repository` folder for CRUD API operations. The repository layer communicates with any layer or the database.
3. **Service Layer:** In the `services` layer, create a file for the model. The service layer is responsible for business logic and calls the repository layer. Create CRUD functions similar to the repository layer.
4. **Controllers:** Controllers call services. Controllers are functions; create named functions (e.g., `const create = (req, res) => {}`).
5. **Express Router:** Use Express Router. Create an `index.js` file for routing. Combine files using export/import. In folder files, use controller functions (e.g., `router.use("/name", controllerFunc)`).
6. **Main API Routes:** In the main `index.js` file, write the main API routes (e.g., `app.use("/api", routesFunc)`).
7. **Seeders:** Seeders are used to add hardcoded data into the database.

## PostgreSQL Commands

For working with PostgreSQL, here are some useful commands:

```bash
sudo -i -u postgres        # Open PostgreSQL server terminal
psql                       # Open PostgreSQL database terminal
sudo systemctl status postgresql.service  # Show PostgreSQL server status
sudo systemctl start postgresql.service   # Start PostgreSQL server locally
sudo systemctl stop postgresql.service    # Stop PostgreSQL server locally
\l                          # List all databases
\c database_name            # Switch to a database or use a database
\dt                         # Show all available tables
\d table_name               # Describe table
\x                          # Expanded display (recommended to turn off)
TABLE "table_name";         # View table data
