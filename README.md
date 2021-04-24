# 🎓 Netflix Clone using DataStax and GraphQL

This project was bootstrapped with [Create React App](https://github.com/facebook/create-react-app).

TO DO: remove unneeded dependencies from package.json

## Table of content

1. [Prerequisites](#1-prerequisites)
2. [Create Astra Instance](#2-create-astra-instance)
3. [Create a security token](#3-create-a-security-token)
4. [Create table **genre** with GraphQL](#4-create-table-genre-with-graphql)
5. [Insert data in**genre**  with GraphQL](#5-insert-data-in-the-table-with-graphql)
6. [Retrieve values of **genre** table](#6-retrieving-list-of-values)
7. [Create **movie** table](#7-creating-a-movies-table)
8. [Insert values in **movie** table](#8-insert-values-in-movie-table)
9. [Retrieve values from **movie** table](#9-retrieve-values-from-movie-tables)
10. [Start the Project](#10-start-the-project)


## 1. Prerequisites

1. Make sure to install Netlify CLI
```
npm install netlify-cli -g
```

## 2. Create Astra Instance

> *When creating your instance use the promotion code **ANIA200** to get 200$ of free credit allowing you about 30 million writes + 30 Million reads  + 50GB a month of monthly storage!!*


**`ASTRA`** is the simplest way to run Cassandra with zero operations at all - just push the button and get your cluster. No credit card required, $25.00 USD credit every month, roughly 5M writes, 30M reads, 40GB storage monthly - sufficient to run small production workloads.  

✅ Register (if needed) and Sign In to Astra [https://astra.datastax.com](https://dtsx.io/workshop): You can use your `Github`, `Google` accounts or register with an `email`.

_Make sure to chose a password with minimum 8 characters, containing upper and lowercase letters, at least one number and special character_

✅ Create a "pay as you go" plan

Follow this [guide](https://docs.datastax.com/en/astra/docs/creating-your-astra-database.html), to set up a pay as you go database with a free $25 monthly credit.

- **Select the pay as you go option**: Includes $25 monthly credit - no credit card needed to set up.

You will find below which values to enter for each field.

- **For the database name** - `code_with_ania_kubow.` While Astra allows you to fill in these fields with values of your own choosing, please follow our recommendations to ensure the application runs properly.

- **For the keyspace name** - `netflix`. It's really important that you use the name "free" for the code to work.

_You can technically use whatever you want and update the code to reflect the keyspace. This is really to get you on a happy path for the first run._

- **For provider and region**: Choose and provider (either GCP or AWS). Region is where your database will reside physically (choose one close to you or your users).

- **Create the database**. Review all the fields to make sure they are as shown, and click the `Create Database` button.

You will see your new database `pending` in the Dashboard.

![my-pic](https://github.com/datastaxdevs/shared-assets/blob/master/astra/dashboard-pending-1000-update.png?raw=true)

The status will change to `Active` when the database is ready, this will only take 2-3 minutes. You will also receive an email when it is ready.

[🏠 Back to Table of Contents](#table-of-content)


## 3. Create a security token

✅ [Create a token for your app](https://docs.datastax.com/en/astra/docs/manage-application-tokens.html) to use in the settings screen

Copy the token value (eg `AstraCS:KDfdKeNREyWQvDpDrBqwBsUB:ec80667c....`) in your clipboard and save the CSV this value would not be provided afterward.

**👁️ Expected output**
![image](pics/astra-token.png?raw=true)

[🏠 Back to Table of Contents](#table-of-content)



## 4. Create table **genre** with GraphQL

✅ Open **GraphQL Playground** by 
1. Click on your active database
2. Click `Connect` TAB
3. Click `GRAPHQL API`
4. Clik link to you playground.

*as show on the picture below*
![image](img/open-playground.png?raw=true)


✅ Populate HTTP HEADER variable `x-cassandra-token` on the bottom of the page with your token as shown below

![image](img/graphql-playground.png?raw=true)

✅ In GraphQL Playground, create a table with the following mutation, making sure to replace `netflix`:
```yaml
mutation {
  reference_list: createTable(
    keyspaceName:"netflix",
    tableName:"reference_list",
    ifNotExists:true
    partitionKeys: [ 
      { name: "label", type: {basic: TEXT} }
    ]
    clusteringKeys: [
      { name: "value", type: {basic: TEXT}, order: "ASC" }
    ]
  )
}
```

[🏠 Back to Table of Contents](#table-of-content)

## 5. Insert data in the Table with GraphQL

✅ In graphQL playground, change tab to now use `graphql`. Edit the end of the URl to change from `system` to the name of your keyspace: `netflix`

✅ Populate HTTP HEADER variable `x-cassandra-token` on the bottom of the page with your token as shown below (again !! yes this is not the same tab)

![image](img/graphql-playground-2.png?raw=true)

✅ In GraphQL Playground,populate the `reference_list` table with the following values:

```yaml
mutation insertGenres {
  action: insertreference_list(value: {label:"genre", value:"Action"}) {
    value{value}
  }
  anime: insertreference_list(value: {label:"genre", value:"Anime"}) {
     value{value}
  }
  award: insertreference_list(value: {label:"genre", value:"Award-Winning"}) {
     value{value}
  }
  children: insertreference_list(value: {label:"genre", value:"Children & Family"}) {
     value{value}
  }
  comedies: insertreference_list(value: {label:"genre", value:"Comedies"}) {
     value{value}
  }
  documentaries: insertreference_list(value: {label:"genre", value:"Documentaries"}) {
     value{value}
  }
  drama: insertreference_list(value: {label:"genre", value:"Dramas"}) {
     value{value}
  }
  fantasy: insertreference_list(value: {label:"genre", value:"Fantasy"}) {
     value{value}
  }
  french: insertreference_list(value: {label:"genre", value:"French"}) {
     value{value}
  }
  horror: insertreference_list(value: {label:"genre", value:"Horror"}) {
     value{value}
  }
  independent: insertreference_list(value: {label:"genre", value:"Independent"}) {
     value{value}
  }
  music: insertreference_list(value: {label:"genre", value:"Music & Musicals"}) {
     value{value}
  }
  romance: insertreference_list(value: {label:"genre", value:"Romance"}) {
     value{value}
  }
  scifi: insertreference_list(value: {label:"genre", value:"Sci-Fi"}) {
     value{value}
  }
  thriller: insertreference_list(value: {label:"genre", value:"Thriller"}) {
     value{value}
  }  
}
```

[🏠 Back to Table of Contents](#table-of-content)

## 6. Retrieving list of values

✅ In GraphQL Playground, not changing tab (yeah) list values from the table with the following command.

```yaml
query getAllGenre {
    reference_list (value: {label:"genre"}) {
      values {
      	value
      }
    }
}
```

*👁️ Expected output*
![image](img/graphql-playground-3.png?raw=true)

[🏠 Back to Table of Contents](#table-of-content)

## 7. Creating a Movies Table

✅ Move to tab `GRAPHQL-SCHEMA`, everything should be set, use the following mutation to create a new table:

```yaml
mutation {
  movies_by_genre: createTable(
    keyspaceName:"netflix",
    tableName:"movies_by_genre",
    ifNotExists: true,
    partitionKeys: [
      { name: "genre", type: {basic: TEXT} }
    ]
    clusteringKeys: [ 
      { name: "year", type: {basic: INT}, order: "DESC" },
      { name: "title", type: {basic: TEXT}, order: "ASC" }
    ]
    values: [
      { name: "synopsis", type: {basic: TEXT} },
      { name: "duration", type: {basic: INT} },
      { name: "thumbnail", type: {basic: TEXT} }
    ]
  )
}
```

*👁️ Expected output*
![image](img/graphql-playground-4.png?raw=true)

[🏠 Back to Table of Contents](#table-of-content)

## 8. Insert Values in Movie table

✅ Move to tab `GRAPHQL`, everything should be set, use the following mutation to populate movies table: 

```yaml
mutation insertMovies {
  inception: insertmovies_by_genre(
    value: { 
      genre:"Sci-Fi", 
      year:2010,
      title:"Inception",
      synopsis:"Cobb steals information from his targets by entering their dreams.",
      duration:121,
      thumbnail:"https://i.imgur.com/RPa4UdO.mp4"}) {
    value{title}
    }
  
  prometheus: insertmovies_by_genre(value: { 
      genre:"Sci-Fi", 
      year:2012,
      title:"Prometheus",
      synopsis:"After a clue to mankind's origins is discovered, explorers are sent to the darkest corner of the universe.",
      duration:134,
      thumbnail:"https://i.imgur.com/L8k6Bau.mp4"}) {
    value{title}
    }
  
  	aliens: insertmovies_by_genre(value: { 
      genre:"Sci-Fi", 
      year:1986,
      title:"Aliens",
      synopsis:"Ellen Ripley is sent back to the planet LV-426 to establish contact with a terraforming colony.",
      duration:134,
      thumbnail:"https://i.imgur.com/QvkrnyZ.mp4"}) {
    value{title}
    }
  
    bladeRunner: insertmovies_by_genre(value: { 
      genre:"Sci-Fi", 
      year:1982,
      title:"Blade Runner",
      synopsis:"Young Blade Runner K's discovery of a long-buried secret leads him to track down former Blade Runner Rick Deckard.",
      duration:145,
      thumbnail:"https://i.imgur.com/xhhvmj1.mp4"}) {
    value{title}
    }
  }
```
> ℹ️ To get more movie data check the file queries.md file

*👁️ Expected output*
![image](img/graphql-playground-5.png?raw=true)

[🏠 Back to Table of Contents](#table-of-content)

## 9. Retrieve values from Movie tables

✅ In GraphQL Playground, not changing tab (yeah) list values from the table with the following command.

```
query getMovieAction {
    movies_by_genre (
      value: {genre:"Sci-Fi"},
       orderBy: [year_DESC]) {
      values {
      	year,
        title,
        duration,
        synopsis,
        thumbnail
      }
    }
}
```

*👁️ Expected output*
![image](img/graphql-playground-6.png?raw=true)


## 10. Start the project

✅ Create `.env` file

```ini
ASTRA_DB_APPLICATION_TOKEN={ your_token }
ASTRA_GRAPHQL_ENDPOINT={ your_endpoint }
```
👩‍💻  Install all the packages

```bash
npm install
```

👩‍💻 Inject all the secret variables and runthe project using

```bash
netlify dev
```

TADA
![image](img/ui.png?raw=true)
