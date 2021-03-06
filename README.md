# Crynamo

[![Build Status](https://travis-ci.org/timkendall/crynamo.svg?branch=master)](https://travis-ci.org/timkendall/crynamo)
[![GitHub release](https://img.shields.io/github/release/timkendall/crynamo.svg)](https://github.com/timkendall/crynamo/releases)


Crynamo is a simple interface to [Amazon's DynamoDB](https://aws.amazon.com/dynamodb/) written in Crystal. Right now it is a fairly low-level wrapper that provides type marshalling between your Crystal program and DynamoDB.

- ✔️ Simple API with `get`, `put`, and `delete` support
- ✔️ DynamoDB type marshalling
- ✔️ Native exceptions for every AWS error
- ✔️ Non-blocking

## Installation

Add this to your application's `shard.yml`:

```yaml
dependencies:
  crynamo:
    github: timkendall/crynamo
    version: ~> 0.1.1
```

## Usage

1. [Configuration](#Configuration)
1. [Client](#Client)

### Configuration

```crystal
require "crynamo"

config = Crynamo::Configuration.new(
  access_key_id: "aws-access-key",
  secret_access_key: "aws-secret-key",
  region: "us-east-1",
  endpoint: "http://localhost:8000",
)
dynamodb = Crynamo::Client.new(config)

```

### Client

Crynamo exposes `Crynamo::Client` as a basic DynamoDB client. The client's API is low-level and mimics the base [DynamoDB Low-Level HTTP API](http://docs.aws.amazon.com/amazondynamodb/latest/developerguide/Programming.LowLevelAPI.html).

```crystal
# Get an item
dynamodb.get!("pets", { name: "Doobie" })

# Insert an item
dynamodb.put!("pets", { name: "Thor", lifespan: 100 })

# Remove an item
dynamodb.delete!("pets", { name: "Doobie" })
```

## Development

1. Follow the instructions here to setup [Local DynamoDB](http://docs.aws.amazon.com/amazondynamodb/latest/developerguide/DynamoDBLocal.html)
1. Install Crystal deps with `shards install`
1. Use [icr](https://github.com/crystal-community/icr) to play with things

## Tip

It's useful to define a bash command for launching DynamoDB. Add this to your `.bash_profile` to start DynamoDB with a simple `dynamodb` command.

```bash
dynamodb() {
 cd /path/to/dynamodb
 java -Djava.library.path=./DynamoDBLocal_lib -jar DynamoDBLocal.jar -sharedDb
}
```

## Contributing

1. Fork it ( https://github.com/[your-github-name]/crynamo/fork )
2. Create your feature branch (git checkout -b my-new-feature)
3. Commit your changes (git commit -am 'Add some feature')
4. Push to the branch (git push origin my-new-feature)
5. Create a new Pull Request

## Contributors

- [timkendall](https://github.com/timkendall)  - creator, maintainer
