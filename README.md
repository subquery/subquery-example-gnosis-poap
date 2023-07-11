# SubQuery - Example Gnosis Poap project

This example project indexes all POAPs mints and transactions on the Gnosis mainnet

A SubQuery project defines which data SubQuery will index from the blockchain, and how it will store it.

## Preparation

#### Environment

- [Typescript](https://www.typescriptlang.org/) are required to compile project and define types.

- Both SubQuery CLI and generated Project have dependencies and require [Node](https://nodejs.org/en/).

#### Install the SubQuery CLI

Install SubQuery CLI globally on your terminal by using NPM:

```
npm install -g @subql/cli
```

Run help to see available commands and usage provide by CLI

```
subql help
```

## Initialize the starter package

Inside the directory in which you want to create the SubQuery project, simply replace `project-name` with your project name and run the command:

```
subql init --starter project-name
```

Then you should see a folder with your project name has been created inside the directory, you can use this as the start point of your project. And the files should be identical as in the [Directory Structure](https://doc.subquery.network/directory_structure.html).

Last, under the project directory, run following command to install all the dependency.

```
yarn install
```

## Configure your project

In the starter package, we have provided a simple example of project configuration. You will be mainly working on the following files:

- The Manifest in `project.yaml`
- The GraphQL Schema in `schema.graphql`
- The Mapping functions in `src/mappings/` directory

For more information on how to write the SubQuery,
check out our doc section on [Define the SubQuery](https://doc.subquery.network/define_a_subquery.html)

#### Code generation

In order to index your SubQuery project, it is mandatory to build your project first.
Run this command under the project directory.

```
yarn codegen
```

## Build the project

In order to deploy your SubQuery project to our hosted service, it is mandatory to pack your configuration before upload.
Run pack command from root directory of your project will automatically generate a `your-project-name.tgz` file.

```
yarn build
```

## Indexing and Query

#### Run required systems in docker

Under the project directory run following command:

```
docker-compose pull && docker-compose up
```

#### Query the project

Open your browser and head to `http://localhost:3000`.

Finally, you should see a GraphQL playground is showing in the explorer and the schemas that ready to query.

For the `subql-starter` project, you can try to query with the following code to get a taste of how it works.

```graphql
query {
  tokens(first: 5, orderBy: MINT_BLOCK_HEIGHT_DESC) {
    nodes {
      id
      mintBlockHeight
      mintReceiverId
      mintDate
      eventId
    }
  }
  addresses(first: 5, orderBy: TOKENS_BY_CURRENT_HOLDER_ID_COUNT_DESC) {
    nodes {
      id
      tokensByCurrentHolderId(first: 5) {
        totalCount
        nodes {
          id
        }
      }
    }
  }
}
```

You might get data back that looks like this

```json
{
  "data": {
    "tokens": {
      "nodes": [
        {
          "id": "16947",
          "mintBlockHeight": "12293177",
          "mintReceiverId": "0xbcb0d39073ad99aa68fb6d7b2c2a433892af6fb3",
          "mintDate": "2020-10-01T17:04:40",
          "eventId": "361"
        },
        {
          "id": "16946",
          "mintBlockHeight": "12292651",
          "mintReceiverId": "0x05b512f909daae5575afb47b3eeb0b0afeb14c00",
          "mintDate": "2020-10-01T16:20:30",
          "eventId": "69"
        },
        {
          "id": "16945",
          "mintBlockHeight": "12291133",
          "mintReceiverId": "0x0542e8f95f765b81cd6a08db37d914f664db5d3e",
          "mintDate": "2020-10-01T14:13:20",
          "eventId": "405"
        },
        {
          "id": "16944",
          "mintBlockHeight": "12290462",
          "mintReceiverId": "0xa615f34b170329507b37c142f8f812b8e1393beb",
          "mintDate": "2020-10-01T13:16:35",
          "eventId": "405"
        },
        {
          "id": "16943",
          "mintBlockHeight": "12290460",
          "mintReceiverId": "0xe07e487d5a5e1098bbb4d259dac5ef83ae273f4e",
          "mintDate": "2020-10-01T13:16:25",
          "eventId": "405"
        }
      ]
    },
    "addresses": {
      "nodes": [
        {
          "id": "0xb8d7b045d299c9c356bc5ee4fe2dddc8a31280a5",
          "tokensByCurrentHolderId": {
            "totalCount": 1,
            "nodes": [
              {
                "id": "16924"
              }
            ]
          }
        },
        {
          "id": "0xba993c1fee51a4a937bb6a8b7b74cd8dffdca1a4",
          "tokensByCurrentHolderId": {
            "totalCount": 1,
            "nodes": [
              {
                "id": "16912"
              }
            ]
          }
        },
        {
          "id": "0x2b098ce1d5a4f9c2729268a4a3f04b387d4cc7ec",
          "tokensByCurrentHolderId": {
            "totalCount": 1,
            "nodes": [
              {
                "id": "16921"
              }
            ]
          }
        },
        {
          "id": "0x60df279f7cc51d2f0ff903f68c3a8dfcf65419f7",
          "tokensByCurrentHolderId": {
            "totalCount": 1,
            "nodes": [
              {
                "id": "16916"
              }
            ]
          }
        },
        {
          "id": "0x626ea6d1e5ea3fbaba22f5d4005d98e7039d0c99",
          "tokensByCurrentHolderId": {
            "totalCount": 1,
            "nodes": [
              {
                "id": "16919"
              }
            ]
          }
        }
      ]
    }
  }
}
```
