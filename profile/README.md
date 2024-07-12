# What are the movie sites you use for free in 2024?

Watching free movies online is a convenient and frugal way to see the films you love right from the comfort of your own home. Yes, there are plenty of sites where you can get movies "for free" but I've taken the time to confirm that the ones listed below, although ad-supported, are clean from viruses and, importantly, 100% legal to use.

There's a huge variety of freely available movies on these sites, from dramas and comedies to action and horror films. There are movies from big-name studios, but also many older and independent movies that you'll love to watch over and over again. Just be sure you have the best TV you can to ensure a great viewing experience.

I spend some time each month looking for the best free movie websites. This list was last updated in June to confirm that they still work, are still free, and are still worth your time.

SOURCE : [Organization](https://github.com/YrtzFilms)

## Introduction

**food-diary** is a web application for tracking calories count for meals eaten daily. It represents an interactive diary, which is able to record notes about products and their quantities and calculate calories for each note (or group of notes) recorded.

## Main idea and goal

The diary consists of **pages**. Each page is associated with some date and contains **notes** grouped by meal types (_breakfast, lunch etc._). Note contains information about **product** and its quantity. Products are grouped by **categories**. Each product has _name_ and _calories cost_ per 100 g of product's quantity recorded. Using this information the application is capable of calculating calories count of:

- single note
- notes group (e.g. for specific meal type)
- the entire page.

This information can be extremely useful for people who want to keep track of energy value of meals they eat every day.

## Local start

1. Start PostgreSQL database:

    ```shell
    docker run -p 5432:5432 --name postgres \
        -e POSTGRES_USER=postgres \
        -e POSTGRES_PASSWORD=postgres \
        -e POSTGRES_DB=FoodDiary \
        -d postgres:15.1-alpine
    ```

    _Optional_: PgAdmin can be started like this:

    ```shell
    docker run -p 5050:80 --name pgadmin -e "PGADMIN_DEFAULT_EMAIL=name@example.com" -e "PGADMIN_DEFAULT_PASSWORD=postgres" -d dpage/pgadmin4
    ```

1. Install .NET SDK 8.0.100 or higher

1. Install Node.js 18.16.0 or higher

1. Install [yarn](https://yarnpkg.com/getting-started/install) package manager

1. Fill necessary secrets:

    ```shell
    dotnet user-secrets --project src/backend/src/FoodDiary.API set "Auth:AllowedEmails:0" "<your_email>"

    dotnet user-secrets --project src/backend/src/FoodDiary.API set "ConnectionStrings:Default" "<your_db_connection_string>"
    ```

    _Allowed email should be compatible with Google Identity Provider_

1. Run migrations:

    ```shell
    dotnet run --project src/backend/src/FoodDiary.Migrator
    ```

1. Start backend application:

    ```shell
    dotnet run --project src/backend/src/FoodDiary.API
    ```

1. Start frontend application:

    ```shell
    cd src/frontend
    yarn start
    ```

1. Navigate to <https://localhost:8080>

## How to run frontend without backend

Go to frontend project directory:

```shell
cd src/frontend
```

Create local env config:

```shell
touch env.local
```

Fill `env.local` with this values:

```text
VITE_APP_MSW_ENABLED=true
VITE_APP_FAKE_AUTH_ENABLED=true
VITE_APP_FAKE_AUTH_LOGIN_ON_INIT=true
```

## Frontend environment variables

Name                                       | Type      | Description
-------------------------------------------|-----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
`VITE_APP_API_URL`                         | `string`  | Specifies a backend API base URL without a trim slash, e.g. `https://localhost:8080`
`VITE_APP_AUTH_CHECK_INTERVAL`             | `number`  | Specifies the auth status check interval in milliseconds to ensure that users with expired cookies will not be able to use the application without refreshing the page in the browser. Not used if `VITE_APP_FAKE_AUTH_ENABLED` is `true`
`VITE_APP_DEMO_MODE_ENABLED`               | `boolean` | Enables demo mode. In demo mode, some features related to file system or external integrations are disabled
`VITE_APP_FAKE_AUTH_ENABLED`               | `boolean` | Setups fake authentication flow without using a backend server and OAuth Identity provider. Used for local development
`VITE_APP_FAKE_AUTH_LOGIN_ON_INIT`         | `boolean` | Defines whether the user is authenticated by default when using a fake authentication flow. Used for local development
`VITE_APP_MSW_ENABLED`                     | `boolean` | Enables mockServiceWorker to intercept and mock all API requests. Used for testing or local development purposes
`VITE_APP_GOOGLE_ANALYTICS_ENABLED`        | `boolean` | Enables Google Analytics
`VITE_APP_GOOGLE_ANALYTICS_MEASUREMENT_ID` | `string`  | Measurement (data stream) ID for Google Analytics
`VITE_APP_MOCK_API_RESPONSE_DELAY` | `number` | Sets delay (in milliseconds) before all mock API responses. Not used if `VITE_APP_MSW_ENABLED` is `false`

## How to generate database migrations

```shell
dotnet ef migrations add <migration_name> \
    -s src/backend/src/FoodDiary.API \
    -p src/backend/src/FoodDiary.Infrastructure \
    -o Migrations
```

## Copyright notes

### Favicon

This favicon was generated using the following graphics from Twitter Twemoji:

- Graphics Title: 1f96c.svg
- Graphics Author: Copyright 2020 Twitter, Inc and other contributors (<https://github.com/twitter/twemoji>)
- Graphics Source: <https://github.com/twitter/twemoji/blob/master/assets/svg/1f96c.svg>
- Graphics License: CC-BY 4.0 (<https://creativecommons.org/licenses/by/4.0/>)
