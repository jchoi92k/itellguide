# Getting started

## Applications and Databases

iTELL requires the following applications and databases to be set up to function properly.

+ Frontend (NextJS): <https://github.com/learlab/itell>
+ Backend - scoring engine and API (FastAPI): <https://github.com/learlab/textbook-summary-api>
+ Database (Postgres)

Follow the steps below to deploy your own intelligent textbook.


## Step 1. Set up a Postgres database

Set up a Postgres database of your choice. The default iTELL application uses [Supabase](https://supabase.com/). Migration will be handled by [Prisma](https://www.prisma.io/) as part of Step 3. All required files for the migration are included in [the prisma folder in the frontend application's Github repository](https://github.com/learlab/itell/tree/main/apps/example-poe/prisma).


## Step 2. Set up the Backend
The backend was developed using Python's [FastAPI](https://fastapi.tiangolo.com/). You can use different setups and cloud services for local development and deployment.

### Local development
Clone [the backend github repository](https://github.com/learlab/textbook-summary-api) and 1) install the requirements from the pipfile and 2) download the required models from SpaCy and Huggingface for use in a local environment:

```
git clone https://github.com/learlab/textbook-summary-api)
cd textbook-summary-api
pip install -r requirements.txt
python .\download_models.py
```

### Deployment
You can deploy the application using any web hosting service of your preference. A Dockerfile is included in the repository for use. Note that a server with a GPU is required to run the summary and QA evaluation models at a practical speed. After deployment, test whether the GPU is enabled by using the `/gpu` endpoint.

You can read more about the development and deployment from the repo's `read.me` [file](https://github.com/learlab/textbook-summary-api/blob/main/README.md).


## Step 3. Frontend deployment

Use a web hosting provider of your choice to deploy the frontend. The default iTELL application uses [Vercel](https://vercel.com/). We will first go over the general setup requirements, and then we will provide a short example of what the deployment will look like when using Vercel.

### Environment variables

The following environment variables must be defined first
Set up [Google OAuth 2.0](https://developers.google.com/identity/protocols/oauth2) and [NextAuth](https://next-auth.js.org/) for user authentication.

```bash
GOOGLE_CLIENT_ID=<YOUR_GOOGLE_CLIENT_ID>
GOOGLE_CLIENT_SECRET=<YOUR_GOOGLE_CLIENT_SECRET>
NEXTAUTH_URL=<YOUR_BASEAPP_URL>
NEXTAUTH_SECRET=<YOUR_NEXTAUTH_SECRET>
DATABASE_URL=<YOUR_DATABASE_URI> # from Step 1
NEXT_PUBLIC_SCORE_API_URL=<YOUR_SCORE_API_ENDPOINT> # from Step 2
```

### Install packages, migrate data, and build

Install the required dependencies with pnpm, migrate the prisma schema after connecting your database, and build the web application:
```bash
pnpm install
npx prisma migrate dev --name init
turbo run build
```

### Example deployment: Vercel

Use Vercel to deploy a quick testable version of iTELL.

1. Create a Vercel account and connect your Github account to Vercel.
2. Fork the frontend repository.
3. Start a new Vercel project and import the frontend repo.
![3](images/deploy_1.png)
4. Specify environment variables (listed above) and hit deploy.
![4](images/deploy_2.png)
5. Confirm that your web application has been deployed.
![5](images/deploy_3.png)

Refer to [Vercel's documentation](https://vercel.com/docs/concepts/deployments/overview) for more information about deploying your webapp in Vercel.





