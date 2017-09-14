# Getting Started
- *SLIDE(S) Introduce topic - Node/express/npm etc*
- Open PowerShell
- `npm install -g express-generator`
- Check with `express --help`
- `cd <where you want to create your app>`
- `express --git --view=pug myapp`

# VSCode & Starting the Node app
- `code myapp`
- Take a look around
- Open Package.json and explain demystify
- Open VSCode terminal **CTRL-'** make sure you are on the TERMINAL tab, not OUTPUT
- `npm install`
- `npm start` Firewall window might popup - allow it!
- Open browser - http://localhost:3000
- Gasp in horror at ugly app!

# Improve the app
- Copy & paste & save from here - https://github.com/benc-uk/devops-labs/blob/master/node-lab/app-snippets.md

- `CTRL-C` in terminal might need to press Y
- `npm start` again
- Refresh browser - cool! Note spelling mistake we will fix later

# Git
- *SLIDE(S) Introduce topic - Git*
- Back in VSCode terminal:
  - `git init`
  - `git add .`
  - `git status` (check node_modules is **not** in staged files)
  - `git commit -m "Created new webapp"`

# VSTS
- *SLIDE(S) Introduce topic - Git*
- *SLIDE(S) Introduce topic - VSTS!*
- Go to your existing account or create one via [my.visualstudio.com](my.visualstudio.com)
- Create new VSTS project call it "DevOps Lab"
  - Pick Git as source control
  - Take other defaults other than share with "Team Members" only

- On new project page in VSTS
  - Expand "push an existing repository from command line" box
  - Copy commands there
  - Paste and run in VSCode terminal
  - **Explain Git remote** 
  - Back in VSTS click on "Code" on menu (validate your code is there!)

*(FROM HERE MY NOTES GET ROUGHER!)*

# VSTS - Build process
- Click setup build
- pick empty process
- rename "Build My Node App"
- pick agent queue - "Hosted"
- Click on add task
- search for "npm"
- add npm task
- leave defaults
- click save & queue
- click queue
- click on build number (opens in new tab)
- watch & wait!

- return to build process tab (close the build tab)
- click add task
- search "publish"
- add "pubish build artifacts" task
  - path = .
  - artifact name = 'myapp' *NOTE. maybe a better name?**
- save & queue
- queue build as before and wait for complete
- click on build number in the breadcrumb
- click on artifacts
- click explore - review and check

## Add CI
back in build
click options
enable continuous int
hit save
no comment
go to build screen
back in vs code
change code
go to SCM in vscode (maybe have to sync)
message
tick
... push

## Add CD - Create ARM
Go into Azure portal
search for template
"custom template"
create your own
---- intro to arm 
----- into to app svc & paas
add resource
- app serviceplan "myAppServicePlan"
add web app
- myWebApp
- choose existing plan
EDIT VARIBLE to mywebapp-202076 *hardcode* !!
Hit save
click edit parameters
add name
{{
   Change to Basic
   Click download
   download to app dir
   click save
   click edit template
   download
   download app dir
   Commit and push
}} TO be replaced with download template from git

## CD - in VSTS
VSTS - Build & Release - Release
+ New Definition
"Deploy Node.js App to Azure App Service"
Name environment staging

add artifact
source = build my node app
click add

Set env level params for Azure (sub and web app name)
add new task
search for reasource add deploy azure resource
drag above deploy

pick RG = MyAppRG-$(Release.EnvironmentName)
Loc = West Europe
browse to template & param file
override params
pickname for web app param = mynodeappbc-$(Release.EnvironmentName) 