# TODO
Make mistake in snippet - DONE!

# Basics
npm install -g express-generator

express --help

cd <where you want to create your app>

express --git --view=pug myapp

# VSCode
code myapp

ctrl-'
(make sure you are on the TERMINAL tab)

npm install

npm start
(Firewall window)

open browser - http://localhost:3000

# Improve the app
https://github.com/benc-uk/azure-node-docker-paas/blob/master/extras/app-snippets.md
!TODO! Comment where the files are
Copy paste & save

CTRL-C in terminal
npm start again
refresh browser

# Git
git init
git add .
git status
(check node_modules)
git commit -m "Created nodejs webapp"

# VSTS
Create new project "DevOps Lab"
- git
- defaults other than Team Members

In new project
"expand" or push an existing repository from command line
copy commands
run in vscode
back in vsts click on "code"

click setpu build
pick empty
name "Build My Node App"
pick agent queue hosted

**comment on environments**

Click on add task
search for npm
add npm
leave defaults
click save & queue
click queue
click on build #123
wait!

add task
search publish
"pubish build artifacts"
path = .
name = 'myapp'
save & queue
queue build

click on build number
click on artifacts
click explore - review 

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