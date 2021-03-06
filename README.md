# Plaid quickstart

This repository accompanies Plaid's [**quickstart guide**][quickstart].

Here you'll find full example integration apps using our [**client libraries**][libraries]:

![Plaid quickstart app](/assets/quickstart.jpeg)

## Table of contents

<!-- toc -->

- [1. Clone the repository](#1-clone-the-repository)
  - [Special instructions for Windows](#special-instructions-for-windows)
- [2. Set up your environment variables](#2-set-up-your-environment-variables)
- [3. Run the quickstart](#3-run-the-quickstart)
  - [Run with Docker](#run-with-docker)
    - [Pre-requisites](#pre-requisites-1)
    - [Running](#running-1)
      - [Start the container](#start-the-container)
      - [View the logs](#view-the-logs)
      - [Stop the container](#stop-the-container)
  - [Run without Docker](#run-without-docker)
    - [Pre-requisites](#pre-requisites)
    - [1. Running the backend](#1-running-the-backend)
      - [Node](#node)
      - [Python](#python)
      - [Ruby](#ruby)
      - [Go](#go)
      - [Java](#java)
    - [2. Running the frontend](#2-running-the-frontend)
- [Testing OAuth](#testing-oauth)

<!-- tocstop -->

## 1. Clone the repository

Using https:

```
$ git clone https://github.com/plaid/quickstart
$ cd quickstart
```

Alternatively, if you use ssh:

```
$ git clone git@github.com:plaid/quickstart.git
$ cd quickstart
```

#### Special instructions for Windows

Note - because this repository makes use of symlinks, to run this on a windows machine please use
the following command when cloning the project

```
$ git clone -c core.symlinks=true https://github.com/plaid/quickstart
```

## 2. Set up your environment variables

```
$ cp .env.example .env
```

Copy `.env.example` to a new file called `.env` and fill out the environment variables inside. At
minimum `PLAID_CLIENT_ID` and `PLAID_SECRET` must be filled out. Get your Client ID and secrets from
the dashboard: https://dashboard.plaid.com/account/keys

> NOTE: `.env` files are a convenient local development tool. Never run a production application
> using an environment file with secrets in it.

## 3. Run the quickstart

There are two ways to run the various language quickstarts in this repository. You can simply choose to use Docker, or you can run the
code directly. If you would like to run the code directly, skip to the
[Run without Docker](#run-without-docker) section.

If you are using Windows and choose not to use Docker, this quickstart assumes you are using some
sort of Unix-like environment on Windows, such as Cygwin or WSL. Scripts in this repo may rely on
things such as `bash`, `grep`, `cat`, etc.

### Run with Docker

#### Pre-requisites

- `make` available at your command line
- Docker installed on your machine: https://docs.docker.com/get-docker/
- Your environment variables populated in `.env`

#### Running

There are three basic `make` commands available

- `up`: builds and starts the container
- `logs`: tails logs
- `stop`: stops the container

Each of these should be used with a `language` argument, which is one of `node`, `python`, `ruby`,
`java`, or `go`. If unspecified, the default is `node`.

##### Start the container

```
$ make up language=node
```

The quickstart backend is now running on http://localhost:8000 and frontend on http://localhost:3000.

If you make changes to one of the server files such as `index.js`, `server.go`, etc, or to the
`.env` file, simply run `make up language=node` again to rebuild and restart the container.

##### View the logs

```
$ make logs language=node
```

##### Stop the container

```
$ make stop language=node
```

### Run without Docker

#### Pre-requisites

- The language you intend to use is installed on your machine and available at your command line.
  This repo should generally work with active LTS versions of each language such as node >= 12,
  python >= 3.8, ruby >= 2.6, etc.
- Your environment variables populated in `.env`

#### 1. Running the backend

Once started with one of the commands below, the quickstart will be running on http://localhost:8000 for the backend. Enter the additional commands in step 2 to run the frontend which will run on http://localhost:3000.

##### Node

```
$ cd ./node
$ npm install
$ ./start.sh
```

##### Python

```
$ cd ./python

# If you use virtualenv
# virtualenv venv
# source venv/bin/activate

$ pip install -r requirements.txt
$ ./start.sh
```

##### Ruby

```
$ cd ./ruby
$ bundle
$ ./start.sh
```

##### Go

```
$ cd ./go
$ go build
$ ./start.sh
```

##### Java

```
$ cd ./java
$ mvn clean package
$ ./start.sh
```

#### 2. Running the frontend

```
$ cd ./frontend
$ npm install
$ npm start

```

## Testing OAuth

Some European institutions require an OAuth redirect authentication flow, where the end user is
redirected to the bank’s website or mobile app to authenticate. For this flow, you should set
`PLAID_REDIRECT_URI=http://localhost:3000/` in `.env`. You will also need to
register this localhost redirect URI in the [Plaid dashboard under Team Settings > API > Allowed
redirect URIs][dashboard-api-section].

OAuth flows are only testable in the `sandbox` environment in this quickstart app due to an https
`redirect_uri` being required in other environments. Additionally, if you want to use the [Payment
Initiation][payment-initiation] product, you will need to [contact Sales][contact-sales] to get this
product enabled.

[quickstart]: https://plaid.com/docs/quickstart
[libraries]: https://plaid.com/docs/api/libraries
[payment-initiation]: https://plaid.com/docs/payment-initiation/
[node-example]: /node
[ruby-example]: /ruby
[python-example]: /python
[java-example]: /java
[go-example]: /go
[docker]: https://www.docker.com
[dashboard-api-section]: https://dashboard.plaid.com/team/api
[contact-sales]: https://plaid.com/contact
