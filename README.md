# go-angular2-material-auth0-and-more

this is a starter kit i was missing when I first started to learn go.
which wasn't that long ago :) so if you have any suggestions to improve it, 
please let me know.

included go features:

- https web server
- go-ini - ini parser
- negroni with the negroni-gorelic package
- mux

included javascript features:

angular2 rc3
* angular2 router 3.0.0-beta.2
* angular2-material 2.0.0-alpha.6
* typescript
* webpack
* auth0 - auth0lock 10.0.0-rc.1
* tslint
* codelyzer
* Google Material Icons

## how to build

### building go related packages

welp, first you need to have Go Installed :) then you need to use go to download the following go modules:

- github.com/go-ini/ini
- github.com/urfave/negroni
- github.com/phyber/negroni-gzip/gzip
- github.com/jingweno/negroni-gorelic
- github.com/unrolled/secure
- github.com/gorilla/mux

just execute `go get <MODULE_NAME>` on each package in the list.

### building client (javascript) related packages

first you need to have the following nodejs global packages installed:

- typescript
- typings
- webpack

if you don't, please download and install nodejs, after that execute `npm install -g <PACKAGES_NAMES_DIVIDED_BY_SPACES>`. that will install the packges globally.

now all you need is to execute `npm install` in the project's root directory to install the required packages.

### webpack
since we are using webpack, we need to use the globally installed webpack package to build our client source files.
simply execute `npm run build` in the project's root directory.

### configuration

###- config.ini

please copy `config/config.ini.defaults` to `config/config.ini`, open it with your favorite text editor, and change it according to your configuration.

in general you have 3 categories in config.ini

- `Server` - which includes the host name of the server and a flag that indicates if it's in a production environment or not.
- `SslCert` - which contains the pem and key files locations to property start an HTTPS Server.
- `NewRelic` - which includes the license key of your newrelic account and the application name that will appear on the dashboard
- `WebServer` - which includes the https port to open, and finally the readn write timeouts for https requests.

###- app.config.js

please copy `config/app.config.js.defaults` to `config/app.config.js`, open it with your favorite text editor, and change it according to your configuration.  

for now there is only one category to modify

- `auth0` - which includes the api key and domain name of your auth0 account.
- `webServer` - which includes the APP_BASE_HREF value to be set.

### compile the go project

execute from the project's root directory the following command: `go build src/main/WebServer.go`

# Things to notice

##-  Go Package github.com/unrolled/secure

I've installed and configured for you this awesome security package for your web server.
you should check and understand the ContentSecurityPolicy of the secureMiddleware variable in the main go file (at src/main/WebServer.go).
I configured the content security policies to allow all the wonderful features that this project has, but if you don't quite understand this subject,
I would strongly recommend to checkout `http://content-security-policy.com/` in order for you to quickly resolve future security issue
that are detected by your own code or 3rd party libraries.

##- Angular Routes Configuration

### auth0
after a succesfull login, the redirection for some reason works but provides errors in the javascript console about not finding a valid route.
in order to work-around this problem, I created a wildcard route so every invalid route will be routed back to the
welcome component. the routes are configured at `client/ts/app/routers.ts`.

# Tested

this package was tested on a Mac Pro with OS X El Capitan 10.11.5, using nodejs 6.2.2 (installed with nvm) and go 1.7beta2.

if for some reason you encounter problems with different versions of node or go, please let me know.