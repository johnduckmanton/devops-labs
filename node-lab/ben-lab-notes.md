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

### *(FROM HERE MY NOTES GET ROUGHER!)*

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
- click on artifacts (tiny link)
- click explore - review and check

## Add CI
- back in build
- click options
- enable continuous int
- hit save no need to put a comment
- go to main VSTS "builds" screen and wait
- back in vs code
- change code - FIX SPELLING MISTAKE
- Go to SCM icon (Y like symbol) in vscode, should be a 1 next to it
   - Enter commit message
   - Click tick
   - Click the '...' select push from menu

### *(NOTES GET ROUGHER STILL!)*

## Create ARM template
- *SLIDE(S) Introduce topic - ARM*
- *SLIDE(S) Introduce topic - App Svc & PaaS*
- Go into Azure portal
- search for template
- "custom template"
- create your own
- add resource
  - app serviceplan "myAppServicePlan"
- add web app
  - myWebApp
  - choose existing plan
- STOP HERE
- ***Download working template from git, add to project and commit and push as before***

## Release pipeline in VSTS
#### NOTE I THINK THIS IS TOO COMPLEX - Replace with importing a working process from json file? then just edit it
#### I think I've got a working release .json in vsts folder [here](/vsts) they will still need to pick the azure sub, the unique prefix for their webapp name, and use the file picker to select the folder to deploy, & the location of the ARM templates - but that is all in the linked parameters so they only need to go to one place to set everything - I THINK!
- back in VSTS goto Build & Release -> Release
- Click '+ New Definition'
- Pick template 
- "Deploy Node.js App to Azure App Service"
- Name environment staging
- add artifact
  - source = "build my node app" build process
  - click add
- Click into "staging" environment tasks & phases
- Set environment level params for Azure 
  - Click on staging at top 
  - Connect to your Azure subscription (Authorize)
  - enter app name = "mywebapp-$(Release.EnvironmentName)"
- add new task
- search for "resource" add deploy azure resource
- drag above deploy
- Edit settings
  - pick RG = "MyAppRG-$(Release.EnvironmentName)"
  - Location = "West Europe"
  - browse to template & param file in your artifacts (click [...] buttons)
  - override params
    - name for web app name param = "$(Parameters.WebAppName)"