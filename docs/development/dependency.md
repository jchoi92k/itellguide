## Project structure

iTELL requires the following applications and databases to be set up to function properly.
* Base web application: <https://github.com/learlab/itell>
* Scoring engine and API: <https://github.com/learlab/textbook-summary-api>
* Postgres database: [schema]()

## Deploying the base web application

### Environment variables

The following enviornment variables must be defined first

Set up [Google OAuth 2.0](https://developers.google.com/identity/protocols/oauth2) and [NextAuth](https://next-auth.js.org/) for user authentication.

```bash
GOOGLE_CLIENT_ID=<YOUR_GOOGLE_CLIENT_ID>
GOOGLE_CLIENT_SECRET=<YOUR_GOOGLE_CLIENT_SECRET>
NEXTAUTH_URL=<YOUR_BASEAPP_URL>
NEXTAUTH_SECRET=<YOUR_NEXTAUTH_SECRET>
```

After setting up a Postgres database using the schema provided above
```bash
DATABASE_URL=<YOUR_DATABASE_URI>
```

After setting up the scoring engine and API
```bash
NEXT_PUBLIC_SCORE_API_URL=<YOUR_SCORE_API_ENDPOINT>
```

### Install packages, generate prisma client, and build



```bash
pnpm install
pnpm prisma generate
next build
```

```bash
pnpm prisma generate
```

## Setting up Supabase

Access the sql file from this link.





## Install packages

After cloning the textbook's repository, you can install all the dependencies for this project with yarn (see the previous section)

```bash
git clone https://github.com/aialoe/macro-economics-textbook
cd macro-economics-textbook
yarn install
```

## Start the server

After installation ends, verify your setup by running

```
yarn dev
```

It may take some minutes to start the project for the first time, if you see the following messages in the end it means things are working

```
success run static queries - 0.029s - 2/2 68.56/s
success run page queries - 0.009s - 3/3 319.64/s
⠀
You can now view principles-of-macroeconomics in the browser.
⠀
  http://localhost:8000/
⠀
View GraphiQL, an in-browser IDE, to explore your site's data and schema
⠀
  http://localhost:8000/___graphql
⠀
Note that the development build is not optimized.
To create a production build, use gatsby build
```

Finally, navigate to <http://localhost:8000/>, if everything is set up correctly you will see the textbook's homepage similar as what is shown below.

![](home.png)
