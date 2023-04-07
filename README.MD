# Node with fastify

This project was built with the intention of studying Node.js. For this purpose, I created a transaction API using some helper tools such as Fastify. 

# Technologies
- Node v18.14.0;
- Fastify(framework to replace express) v4.15.0;
- Knex(query builder) v2.4.2;
- Zod(validation library) v3.21.4;
- Vitest(tests) v0.29.7;
- sqlite3(dev) v5.1.6 and PostgreSQL(prod) v8.10.0;
- tsup(to convert ts in js) v6.7.0;
- Typescript v5.0.2;

# Launch
- To launch this project run the script `tsx watch src/server.ts` or run `npm run dev`;
- The API is online in this link: https://node-with-fastify.onrender.com

## Table of contents
* [General Info](#general-info)

## General Info

This project was built and configured following these steps:

### Init Setup 

- `npm init -y`
    - This will init your project with a package.json;
    - Create a folder src and inside this folder, create a file called server.ts;

### Typescript Setup

- `npm i -D typescript`
    - Install the typescript as a dev dependency(typescript is just use in prod);
    - Run `npx tsc --init` to generate a tsconfig.json;
    - Change the target of this file to es2020(to get the new features of ecmaScript);
    - Run `npm i -D @types/node` to provides type definitions for Node.js in TypeScript. This allows TypeScript developers to write code for Node.js with more accurate autocomplete and type checking in their code editors;
    - Run `npm i tsx -D` to install a CLI command (alternative to node) for seamlessly running TypeScript;
    - So, the script `npx tsx src/server.ts` will automate the all process to convert the file ts in js and run the app;
    - Update the script above to `tsx watch src/server.ts` to node update the server when something in the code changes;
### Fastify Setup

- `npm i fastify`
    - This script will install the fastify;

### ESLint Setup

- Run `npm i eslint @rocketseat/eslint-config -D` to get the eslint config of rocketseat;
- Create a .eslintrc.json to setup the extends of eslint-config installed;
- To automate the formatting texts with eslint, go to command pallet and search for Open Workspace Settings(JSON)
and put this command: 
    "editor.codeActionsOnSave": {
        "source.fixAll.eslint": true
    };
- Besides that, go to preferences -> settings and uncheck the Editor: Format On Save;
- Run the command `eslint src --ext .ts` to see all files that needs to be fixed;
- Run the command `eslint src --ext .ts --fix` will show all files that needs to be fixed and will fix all files that are easier to be fixed;

### Query Builder

- For this project, i used Knex.js as a Query Builder;
- Run `npm install knex` to install knex ( SQL query builder);
- Run `npm install knex sqlite3 -D` to install sqlite3 as a devDependency;
- Create a file database.ts to create a conection with DB;

### Migrations

- Version control of databse (similar with git but for database);
- Create a knexfile.ts to setup the config of knex;
- In package.json put the script knex as `node --no-warnings --loader tsx ./node_modules/.bin/knex` to execute with ts and not with js;
- Run the command `npm run knex -- migrate:make create-transactions`
- Fill the methods inside the create-transactions;
- Run the command `npm run knex -- migrate:latest` to read all migrations and execute;
- Run the app and see all tables in the database with `await knex('sqlite_schema').select('*')`;
- If you wanna undo what yo've made run the script `npm run knex -- migrate:rollback`;
- Run the command `npm run knex -- migrate:make add-session-id-to-transactions` to insert a field id into transactions table;
- Fill the methods inside the create-transactions;
- Run the command `npm run knex -- migrate:latest` to read all migrations and execute;

### DOT ENV

- Create the file .env;
- Install the dotenv dependecy with `npm install dotenv`;
- Use import 'dotenv/config' in the file that you need to use the .env with process.env;
- Run `npm install zod ` to install zod;
- Use zod to validate data;
- Create a folder called env in your sourve folder to validate data with zod;

### Cookies

- Run `npm install @fastify/cookie` to start work with cookies

### Tests

- Vitest `npm install vitest -D`;
- Created script test in package.json to execute the tests `npm test or npm run test`;
- Install supertest `npm install supertest -D ` to avoid to up a server when called app.listen;
- Install the @types from supertest `npm install -D @types/supertest`;
- Important to create a new db for tests;
- Create a .env.test file;
- When you run npm run test, vitest will create a node_env and set his value as a test;
- Check in the .env folder to set the correct env to each enviroment;
- Create a beforeEach in the spec.ts;
- This beforeEach will run execSync('npm run knex migrate:latest') and create the tables inside table.db;
- Important to be in beforeEach because each test must have a db empty to avoid conclicts;

### Deploy

- Install tsup to convert ts in js besides use `npx tsc`;
- Run `npm install tsup -D`;
- Create in package.json the script build that will run `tsup src`;
- Run `npm run build`;
- Run `node dist/server.js` and see everthing running;
- Create a .eslintignore to ignore the files that are in /dist;
- Put the dist file inside gitignore;

### Options of deploy

- render.com ( choosed for this project )
- fly.io
- railway.com

### Render (Cloud Service)

- Create a database with PostgreSQL; 
- This database will be deleted in 90 days, so it`s necessary to create again in 90 days;
- Copy the db URL that were created;
- Our app needs do support PostgreSQL(production) and sqlite(development);
- Create a new env variable called DATABASE_CLIENT that will be a enum and set it in src/env;
- Install postgree with `npm install pg`;
- Change in database.ts to get DATABASE_CLIENT value; 
- Inform engines in package.json to set node version compatible with render and the node from this project;
- Back to Render and when the database is created, back to dashboard and create a new web service;
- Fill the fields with the commands that are used to up the application;
- Click in advance options and set de env variables DATABASE_CLIENT and DATABASE_URL (was generetated when the database was created);
- See the log the web app deploying;