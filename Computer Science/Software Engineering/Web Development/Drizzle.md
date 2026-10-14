# Querying
## Relational Query
Inside the `find` method, use these parameters:
- `columns`: determines SELECT clause (columns to include), using boolean values
	- setting column: true, include only these columns
	- setting column: false, include all other columns
- `where`: conditionals
- 

List of conditional operators:
All operators take two parameters (col, value).
The value can be string, int, array, etc.
- Basic
	- eq
	- ne
	- gt
	- gte
	- lt
	- lte
- String
	- like
	- ilike
	- notLike
- Set and Range
	- inArray
	- notInArray
	- between
	- notBetween
- Null checks
	- isNull
	- isNotNull
These operators are grouped by:
- and
- or
- not
They are grouped in this way:
`and(eq(), gt(), like())...`
# Drizzle Basic Workflow
## Step 1: Prerequisites & Installation
Prerequisites: Node.js installed and a fresh Next.js project.
1. Install the ORM and Postgres driver: npm install drizzle-orm postgres
2. Install the development kit: npm install -D drizzle-kit
3. Add your DATABASE_URL to .env.local.

## Step 2: Define the Schema
Prerequisites: Knowledge of your data model (the ProjectData type you wrote).
1. Create src/db/schema.ts.
2. Use pgSchema("firma") to declare your namespace.
3. Define your projects table and status enum within that schema object.

## Step 3: Drizzle Configuration
Prerequisites: Your DATABASE_URL must be accessible to the CLI.
1. Create a drizzle.config.ts file in your root directory.
2. Specify the out directory (where migrations go), the schema path, and the dbCredentials.
3. Ensure you set schemaFilter: ["firma"] so Drizzle knows which namespace to manage.

## Step 4: Generate then Migrate the Schema to Supabase
Prerequisites: Supabase database is online.
1. Run `npx drizzle-kit generate` (will create an SQL file that contains how supabase will migrate the schemas)
2. Run `npx drizzle-kit migrate`j
3. Verify the firma schema and projects table appeared in the Supabase Table Editor UI.

## Step 5: Initialize the DB Client
Prerequisites: The connection string in your environment variables.
1. Create src/db/index.ts.
2. Initialize the postgres client and pass it into the drizzle function.
3. Export the db instance to use throughout your app.

## Step 6: Querying in a Server Component
Prerequisites: At least one row of data in your DB (add one manually in Supabase UI to test).
1. In src/app/page.tsx, import your db instance and the projects schema.
2. Make the component async.
3. Use await db.select().from(projects) to fetch your array.

## Step 7: Deployment Configuration
Prerequisites: Vercel or similar hosting setup.

1. Add your DATABASE_URL to your production environment variables.
2. Ensure your connection string uses the Transaction mode (Port 6543) if you encounter connection pooling issues on serverless functions.