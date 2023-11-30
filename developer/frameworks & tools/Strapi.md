# What’s Strapi?

---

Strapi is a self-hosted and an op**en source headless CMS** that helps developers to easily build, deploy, and manage APIs. It’s 100% JavaScript and fully customizable.

- It’s free to use as a self-hosted application
  - WIX and Shopify is not self-hosted
- Strapi is developed as an open source project
- Strapi is a headless CMS
  - Monolithic CMS (WordPress, OpenCart, Magento) vs Headless CMS
- Strapi is based on Node.js and admin panel is built with Next.js
- Easily customize the admin panel as well as the API.

# How it works

---

1. Effortlessly create content structures that flex to your needs.
2. Seamlessly write, edit and manage any content types
3. Easily build apps and digital experiences without the distraction of CMS complexities
4. Consume Strapi API from any client using REST or GraphQL API
5. Deploy on Strapi Cloud or on any cloud platforms

## Why Strapi?

---

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/bbbdc29f-09c5-4f11-a0ea-531f6a210717/Untitled.png)

Accelerating the delivery of modern digital experiences.

1. Drastically shorten your time-to-deploy
2. Manage your content, deliver it anywhere
3. A seamless multi-device experience

## The story of Strapi

---

![TIMELINE_2015_2023_1_5db63280d0.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/18980bc9-336e-4cd6-b4f3-82592e1aa033/TIMELINE_2015_2023_1_5db63280d0.png)

## Strapi Release Notes

v1.0.0 ~ oct 1, 2015 by \***\*Loïc Saint-Roch, France\*\***

v1.5.4 ~ Jan 20, 2016

v1.5.7 ~ Apr 12, 2017 by ********\*\*\*\*********Aurélien GEORGET, France********\*\*\*\*********

v1.6.0 ~ Apr 18, 2017 by \***\*Pierre Burgy, Co-founder & CEO of Strapi, France\*\***

v1.6.3 ~ May 8, 2017

v3.0.0 ~ Jul 20, 2017 by ********\*\*\*\*********Aurélien GEORGET, France********\*\*\*\*********

v3.0.0-alpha ~ May 2, 2019 by \***\*Jim LAURIE, France\*\***

v3.0.0-beta ~ May 7, 202 by \***\*Alexandre BODIN, France\*\***

Stable version: v3.0.0, May 26, 2020

v3.1.0 ~ Jul 23, 2020

v3.2.0 ~ Oct 6, 2020

v4.7.0 ~ Mar 3, 2023

# Configurations

---

응용프로그람의 설정정보는 .config등록부에 있다. 이 설정정보는 응용프로그람이 실행되는 시점에서 적재된다.

1. .config/server.js가 다음과 같이 설정되였다면 host설정정보를 다음과 같이 얻을수 있다. `strapi.config.get('server.host', 'default value if undefined')`

   ```jsx
   module.exports = {
     host: "0.0.0.0",
   };
   ```

2. 설정정보화일은 js혹은 json일수 있다.
3. 각종 설정화일들
   - Database
   - Server
   - Admin panel
   - Middlewares
   - API configration
   - API tokens configuration
   - cron jobs
     - `cron.enabled` 설정이 ./config/server.js에서 TRUE여야 한다.
     - 형식: _ (sec) _ (minute) _ (hour) _ (day) _ (month) _ (day of week)
     - `node-schedule` 를 리용하고 있다.
     - step:
       1. create a cron job
          - ./config/cron-tasks.js
            ```jsx
            module.exports = {
              /**
               * Simple example.
               * Every monday at 1am.
               */

              myJob: {
                task: ({ strapi }) => {
                  // Add your own logic here (e.g. send a queue of email, create a database backup, etc.).
                },
                options: {
                  rule: "0 0 1 * * 1",
                  tz: "Asia/Dhaka",
                  // start 10 seconds from now
                  start: new Date(Date.now() + 10000),
                  // end 20 seconds from now
                  end: new Date(Date.now() + 20000),
                },
                // only run once after 10 seconds
                options: new Date(Date.now() + 10000),
              },
            };
            ```
       2. Enable cron jobs in ./config/server.js

          ```jsx
          const cronTasks = require("./cron-tasks");

          module.exports = ({ env }) => ({
            host: env("HOST", "0.0.0.0"),
            port: env.int("PORT", 1337),
            cron: {
              enabled: true,
              tasks: cronTasks,
            },
          });
          ```
   - environment variables
   - lifecycle functions
   - plugins configuration
   - public assets configuration
   - RBAC
   - SSO
   - TypeScript configuration

# Deploy to Heroku

---

> Content-type Builder is disabled in production.

### Setup a Strapi project for deployment

---

1. Add a production configuration environment by creating a sub-directory `./config/env/production`.
2. Create `database.js` inside the `./config/env/production` directory.
3. Add the following code snippet to the `database` configuration file:

   ```jsx
   const { parse } = require("pg-connection-string");

   module.exports = ({ env }) => {
     const { host, port, database, user, password } = parse(
       env("DATABASE_URL")
     );

     return {
       connection: {
         client: "postgres",
         connection: {
           host,
           port,
           database,
           user,
           password,
           ssl: { rejectUnauthorized: false },
         },
         debug: false,
       },
     };
   };
   ```

4. Create `server.js` inside the `./config/env/production` directory.
5. Add the following code snippet to the `server` configuration file:

   ```jsx
   module.exports = ({ env }) => ({
     proxy: true,
     url: env("MY_HEROKU_URL"), // Sets the public URL of the application.
     app: {
       keys: env.array("APP_KEYS"),
     },
   });
   ```

6. Add PostgreSQL dependencies by installing `[pg` package](https://www.npmjs.com/package/pg) and `[pg-connection-string` package](https://www.npmjs.com/package/pg-connection-string):

   ```bash
   npm install pg && npm install pg-connection-string
   ```

7. Add `package-lock.json` to the end of the `.gitignore` file at the root of the Strapi project:
8. Verify that all of the new and modified files are saved locally.
9. Commit the project to a local repository:

   ```bash
   git init
   git add .
   git commit -m "commit message"
   ```

### Create and configure a Heroku App

---

1. Install and use the Heroku CLI
   1. Use the following OS-specific installation instructions to install the Heroku CLI tool:

      ```bash
      # Mac
      brew tap heroku/brew && brew install heroku
      https://cli-assets.heroku.com/heroku.pkg

      # Ubuntu
      sudo snap install --classic heroku

      # Windows
      https://cli-assets.heroku.com/heroku-x64.exe
      https://cli-assets.heroku.com/heroku-x86.exe
      ```

   2. Login to Heroku from the CLI, following the command-line instructions:

      ```bash
      heroku login
      ```
2. Create a Heroku project

   ```bash
   heroku create

   heroku git:remote -a your-heroku-app-name
   ```

3. Create a Heroku database

   ```bash
   heroku addons:create heroku-postgresql:<PLAN_NAME>
   # PLAN_NAME: (https://devcenter.heroku.com/articles/heroku-postgres-plans)
   # mini, basic, etc..

   heroku config
   ```

4. Populate the env variables

   ```bash
   # new
   heroku config:set APP_KEYS=$(openssl rand -base64 32)
   heroku config:set API_TOKEN_SALT=$(openssl rand -base64 32)
   heroku config:set ADMIN_JWT_SECRET=$(openssl rand -base64 32)
   heroku config:set JWT_SECRET=$(openssl rand -base64 32)
   heroku config:set MY_HEROKU_URL=$(heroku info -s | grep web_url | cut -d= -f2)
   heroku config:set NODE_ENV=production

   # existing
   heroku config:set APP_KEYS=$(cat .env | grep APP_KEYS | cut -d= -f2-)
   heroku config:set API_TOKEN_SALT=$(cat .env | grep API_TOKEN_SALT | cut -d= -f2)
   heroku config:set ADMIN_JWT_SECRET=$(cat .env | grep ADMIN_JWT_SECRET | cut -d= -f2)
   heroku config:set JWT_SECRET=$(cat .env | grep -w JWT_SECRET | cut -d= -f2)
   heroku config:set MY_HEROKU_URL=$(heroku info -s | grep web_url | cut -d= -f2)
   heroku config:set NODE_ENV=production
   ```

5. Deploy an application to Heroku

   ```bash
   git push heroku HEAD:main

   # open from the cli:
   heroku open
   ```

### Update your project

---

```bash
git add .
git commit -am "Changes to my-project noted"
git push heroku HEAD:main
heroku open
```

# REST API

The REST API allows accessing the content-types through API endpoints. Strapi automatically creates API endpoints when a content-type is created.

<aside>
ℹ️ The REST API by default does not populate any relations, media fields, components, or dynamic zones. Use the populate parameter to populate specific fields.

</aside>

## Endpoints

---

```bash
GET: /api/:ID # Get a list of entries
POST: /api/:ID # Create an entry
GET: /api/:ID/:documentID # Get an entry
PUT: /api/:ID/:documentID # Update an entry
DELEET: /api/:ID/:documentID # Delete an entry
```

## Requests

---

Requests return a response as an object which usually includes the following keys:

```jsx
{
	"data": [{
		"id": number
		"attributes": object
		"meta": object
	}]
	"meta": object // info about pagination, publication state, locales, etc
	"error": object
}
```

## REST API parameters

---

1. sort

   ```jsx
   GET /api/:ID?sort=value # to sort on 1 field
   GET /api/:ID?sort[0]=value1&sort[1]=value2 # to sort on multiple fields
   GET /api/:ID?sort[0]=value1:asc&sort[1]=value2:desc # asc or desc
   ```

2. filters

   ```jsx
   # Syntax: GET /api/:pluralApiId?filters[field][operator]=value
   # operator: $eq, $eqi, $ne, $lt, $lte, $notIn, $contains, $null ....
   # e.g.

   // Find users having 'John' as first name
   GET /api/users?filters[username][$eq]=John

   // Find multiple restaurants with ids 3, 6, 8
   GET /api/restaurants?filters[id][$in][0]=3&filters[id][$in][1]=6&filters[id][$in][2]=8

   // Find books with 2 possible dates and a specific author
   GET /api/books?filters[$or][0][date][$eq]=2020-01-01&filters[$or][1][date][$eq]=2020-01-02&filters[author][name][$eq]=Kai%20doe

   // Find restaurants owned by a chef who belongs to a 5-star restaurant
   GET /api/restaurants?filters[chef][restaurants][stars][$eq]=5
   ```

3. populate
4. fields
5. pagination

   ```jsx
   # page with pageSize, start, limit
   GET /api/:ID?pagination[page]=1&pagination[pageSize]=10

   # The default and maximum values for pagination[limit] can be configured in the ./config/api.js file with the api.rest.defaultLimit and api.rest.maxLimit keys.

   GET /api/articles?pagination[start]=0&pagination[limit]=10
   ```

6. publication state
7. locale

   <aside>
   ℹ️ Prerequisites
   • The **[Internationalization (i18n) plugin](https://docs.strapi.io/dev-docs/plugins/i18n)** should be installed.
   • **[Localization should be enabled for the content-type](https://docs.strapi.io/user-docs/content-type-builder/creating-new-content-type#creating-a-new-content-type)**.

   </aside>

# Entity Service API

Strapi provides an Entity Service API. The Entity Service is the layer that handles Strapi’s complex data structures like components and dynamic zones.

The Entity Service API is the recommended API to interact with your application’s database.

````jsx
# USAGE
## The entity service is available through ```strapi.entityService```
const entry = await strapi.entityService.findOne('api::article.article', 1, {
  populate: { someRelation: true },
});
````

<aside>
ℹ️ Components: it’s a set of fields that you want to reuse in multiple places (content-types) across your app.

</aside>

<aside>
ℹ️ Dynamic zones: It’s “areas” of your application where you let content editors choose what component to include

</aside>
