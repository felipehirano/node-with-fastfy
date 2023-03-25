# Init

- npm init - y
- create folder src and file index.ts
- npm i -D typescript
- create a settings file of typescript using npx
- npx tsc --init -> generates de tsconfig.json
- change the target of tsconfig.json to es2020
- npx tsc src/index.ts -> transform the typescript file into javascript file
- npm i fastify
- npm i -D @types/node
- npm install tsx -D
- run `npx tsx src/server.ts` will automate the all process to convert the file in js and run the app,
  but this is not recomendable to use in production enviroment because does't have a good perfomance.
- npm i eslint @rocketseat/eslint-config -D
- create a file called .eslintrc.json
- To automate the formatting texts with eslint, go to command pallet and search for Open Workspace Settings(JSON)
and put this command: 

"editor.codeActionsOnSave": {
    "source.fixAll.eslint": true
}

- Besides that, go to preferences->settings and uncheck the Editor: Format On Save
- Run the command `eslint src --ext .ts` to see all files that needs to be fixed;
- Run the command `eslint src --ext .ts --fix` will show all files that needs to be fixed and will fix all files that are easier to be fixed;


# Query builder 

- Use Knex.js as a query builder and sqlite3 as a driver for DB;
- See the docs in knexjs.org;
- Run `npm install knex sqlite3`;
- Create database.ts to connect with database;

# Migrations

- Version control of database;
- It is similar with git, but for database;
- Create a knexfile.ts to config set up the config of knex;
- In package.json put the script knex as `node --no-warnings --loader tsx ./node_modules/.bin/knex` to execute with ts and not with js;
- Run the command `npm run knex -- migrate:make create-transactions`
- Fill the methods inside the create-transactions;
- Run the command `npm run knex -- migrate:latest` to read all migrations and execute;
- Run the app and see all tables in the database with `await knex('sqlite_schema').select('*')`;
- If you wanna undo what yo've made run the script `npm run knex -- migrate:rollback`;
- Run the command `npm run knex -- migrate:make add-session-id-to-transactions` to insert a field id into transactions table;
- Fill the methods inside the create-transactions;
- Run the command `npm run knex -- migrate:latest` to read all migrations and execute;

# DOT ENV

- Create the file .env;
- Install the dotenv dependecy with `npm install dotenv`;
- Use import 'dotenv/config' in the file that you need to use the .env with process.env;
- Use zod to validate data;
- Create a folder called env in your sourve folder to validate data with zod


# Requisitos funcionais

- [x] Usuario deve poder criar uma nova transação(crédito e débito);
- [x] Usuário deve obter um resumo da sua conta;
- [x] Usuário deve poder listar todas as transações que já ocorreram;
- [x] Usuário deve poder visualizar uma transação única;

# Regras de negócio

- [x] A transação pode ser do tipo crédito que somará ao valor total, ou débito que irá subtrair do valor total;
- [ ] Deve ser possível identificarmos o usuário entre as requisições;
- [ ] O usuário só pode visualizar transações o qual ele criou;

# Cookies

- Run `npm install @fastify/cookie` to start work with cookies

# Tests

- Vitest `npm install vitest -D`
- Created script test in package.json to execute the tests `npm test or npm run test`
- Install supertest `npm install supertest -D ` to avoid to up a server when called app.listen
- Install the @types from supertest `npm install -D @types/supertest`
- Important to create a new db for tests
- Create a .env.test file
- When you run npm run test, vitest will create a node_env and set his value as a test
- Check in the .env folder to set the correct env to each enviroment
- Create a beforeEach in the spec.ts
- This beforeEach will run execSync('npm run knex migrate:latest') and create the tables inside table.db
- Important to be in beforeEach because each test must have a db empty to avoid conclicts

# Deploy

- Install tsup to convert ts in js besides use `npx tsc`
- Run `npm install tsup -D`
- Create in package.json the script build that will run `tsup src`
- Run `npm run build`
- Run `node dist/server.js` and see everthing running
- Create a .eslintignore to ignore the files that are in /dist
- Put the dist file inside gitignore

# Options of deploy

- render.com ( choosed for this project )
- fly.io
- railway.com

# Render (Cloud Service)

- Create a database with PostgreSQL 
- This database will be deleted in 90 days, so it`s necessary to create again in 90 days
- Our app needs do support PostgreSQL and sqlite
- Create a new env variable called DATABASE_CLIENT that will be a enum and set it in src/env
- Install postgree with `npm install pg`
- Change in database.ts to get DATABASE_CLIENT value 
- Inform engines in package.json to set node version compatible with render and the node from this project
- 