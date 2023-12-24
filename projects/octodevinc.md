# OctoDevInc Projects

## Contact

Company: Octo Development Inc, Information Technology & Services Toronto
https://www.linkedin.com/company/octo-development-inc/about/
Co-founder : Alex A

- Linkedin: https://www.linkedin.com/in/alex-a-b10607167/
- Freelancer:
  Manager: Ivan Carosati

## Project Overview

- Domain: http://octodev.com/
- Skills: Angular.js + Laravel
- Repo: git clone https://ivica5859@bitbucket.org/octodevelopment/lmse-membersite.git

## Instructions

Membersite configuration for staging.

Setup local environment under HTTPS (self-signed certificate)
under the following URLS:

'[http://lmse.local](http://lmse.local/)',
'[http://exams.lmse.local](http://exams.lmse.local/)',

If you need the port you can use :4200
'[http://lmse.local:4200](http://lmse.local:4200/)',
'[http://exams.lmse.local:4200](http://exams.lmse.local:4200/)',

Those are the only whitelisted websites for CORS.

On the membersite code change the following lines in the environment file
(src/environments/environment.ts)

endpoint: 'https://api.lmse.local/v1',
pointsUrl: 'exams.lmse.local',

to

endpoint: 'https://staging-api.idcert.io/v1',
pointsUrl: '[staging-exams.idcert.io](http://staging-exams.idcert.io/)',

To compile you can run `npm run ng-watch` just make sure your local config
can route [https://lmse.local](https://lmse.local/) to localhost:4200 or set a domain to the npm script
in package.json. It won't work unless you're under [https://lmse.local](https://lmse.local/).

Please never commit those changes in environment.ts or package.json.

The branch you'll be working on is: `feature/LMSE-339_FAQ_Page`.
Please commit all the changes there, for the codestyle make sure your editor is
using the .editorconfig in the root of the project, webstorm preferred.
