# Final Capstone Survival Guide
This is an *unofficial* guide with some helpful tips for the final capstone. Basically I'm circling landmines in this project to avoid and offering some advice. I've collated the experience of years worth of mentees together here I hope it helps.

## Setup

Before you get started on the user stories you want to get your database ship shape and ready to go.

You're building a restaurant app and you need to keep track of the reservations and the physical tables on the premises.

You'll need to create two database tables a `reservationsTable` to keep track of the reservations and a `tablesTable` (great name) to keep track of the tables.

They have seed data for reservations provided. Note that the seed data is in `.json` files, not to be confused with the seed files themselves which are `.js` files. You'll need to write your own seed data json for the table data. The data the tests are expecting is buried in the backend instructions.

Write the seed files to define the tables. This should be pretty straightforward if you've done the We Love Movies app. There is one catch though.

IMPORTANT: Set the status field of the reservations table to default to 'pending'.

The seed data does not have a status field for each entry. This means that if you don't set a default value the status will be null when the seed is run which will break `where` clauses in your knex queries.

Now that you have created your seed and migration files make sure they work.

IMPORTANT: Make sure that when you run knex commands you are in the backend subdirectory, NOT the top level directory.

The following commands will be helpful:

`npx knex migrate:make [your table name]` creates a new migration. Replace '[your table name]' with your table name e.g. 'reservationsTable'.
`npx knex migrate:latest` runs all your migrations.
`npx knex migrate:rollback --all` rolls back all your migrations. See below.
`npx knex seed:run` runs your seed files.

IMPORTANT: if you need to edit your migration files make sure you have rolled back the migrations first. Failing to do this will corrupt your database and the above commands will not work.

Fortunately if this occurs the fix is pretty easy. Delete the tables in your db manually. The easiest way to do this is through the DBeaver gui. Make sure you delete all of them including knex_migrations and knex_migrations_lock. Then you should be able to run your migrations and seeds with no problem.

## Running Tests

Now that your migrations are good to go you should be able to run your tests. Note that tests should be run from the top level directory. This is a part of the project that likes to break in lots of ways.

Run the command `npm run test`. If this command does not work *please* ask me or someone else for help. Depending on the speed of your machine running all the tests might take a while.

As you go you should run tests one user story at a time. Here are some commands.

`npm run test:1` runs end to end tests where 1 is the user story you're testing.
`npm run test:backend` runs the backend tests for all the user stories.
`npm run test:1:backend` runs the backend tests for user story 1.

IMPORTANT: do not run your tests while the app is running locally. That's gonna cause problems.

## Doing User Stories

The instructions say to work through the user stories one at a time and sort of encourage bouncing back and forth between the frontend and backend. I propose two alternatives.

1. If you're working on user stories one at a time with others or are less confident with backend then for each user story get the backend tests for that user story working first before touching the frontend. This will give you some confidence the backend is doing what its supposed to while working on the frontend.
2. If you're confident with backend and working alone go ahead and get *all* the backend tests working across the user stories before starting frontend. Bouncing around from front to back takes a lot of mental overhead.
