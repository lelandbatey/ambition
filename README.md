# ambition

Action tracking

## Setup


### 1. Download
`$ go get github.com/myambition/ambition`

### 3. Setup Config
Edit config.json for database settings and server port.

### 2. Get static files with bower
`$ cd static`
`$ bower install`


### Setup Postgresql

```
$ sudo apt-get install postgresql

# set password to be ambition for it to be easy
$ sudo adduser ambition

$ sudo -i -u postgres

$ createdb ambition

# let them be superuser
$ createuser ambition

$ psql

$ # ALTER USER ambition PASSWORD ‘ambition';

$ exit
```

## Usage

### Setup

`./cmd/main.go` must be run from the root of this repo. All paths are relative to the root of this repo

`go run cmd/main.go`

```
// Create tables
$ ambition create
// Seed tables with example data from json
$ ambition seed
// Drop tables
$ ambition drop
```

### Webserver

```
localhost:3000/
```

## Basic structure

### main.go

- Checks for command line arguments for setup.
- If no command line arguments, start web server on port 3000 loading routes from `routes.go`

### routes.go

- Sets routes with http methods, paths, and parameters to functions in `hander.go`
- TODO: Add better description of all routes. Currently `docs/structure.md` has all information, it needs to be more formalized.

### handler.go

Possibly change handler.go to formatter.go and use it to parse the request and send it the right way. Then change jsonHandler.go to hander.go and only interact with db.go there

**Input**
- Parameters in url
- Optional: Query parameters
- Optional: Post body parameters
**Result**
- Calls jsonHandler.go functions to handle both input and output json
- database selection and returning of json
- database insertion

I just realized that handler.go, db.go, and jsonHandler.go are much more entwined than I thought. handler.go with jsonHandler.go; both calling db.go methods.

### jsonHandler.go

The idea was just to handle json here, but it also works with the database. May change to handler.go see handler.go

### db.go

Wraps postgres with go functions so that all SQL interaction happens here. SQL strings are only allowed in db.go

### types.go

All types used in ambition. May want to add custom struct tags for sql here. Like sql value name and sql value type, for generic database methods in db.go.

### commands.go

Functions for command line arguments go here

### util.go

Custom utils snippits go here.


