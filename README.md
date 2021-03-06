# `terraform-plugin-kafka-connect`
[![CircleCI](https://circleci.com/gh/Mongey/terraform-provider-kafka-connect.svg?style=svg)](https://circleci.com/gh/Mongey/terraform-provider-kafka-connect)

A [Terraform][1] plugin for managing [Apache Kafka Connect][2].

## Installation

Download and extract the [latest
release](https://github.com/Mongey/terraform-provider-kafka-connect/releases/latest) to
your [terraform plugin directory][third-party-plugins] (typically `~/.terraform.d/plugins/`)

## Example

Configure the provider directly, or set the Env variable `KAFKA_CONNECT_URL`
```hcl
provider "kafka-connect" {
  url = "http://localhost:8083"
}

resource "kafka-connect_connector" "sqlite-sink" {
  name = "test-sink"

  config = {
    "name"            = "test-sink"
    "connector.class" = "io.confluent.connect.jdbc.JdbcSinkConnector"
    "tasks.max"       = "1"
    "topics"          = "orders"
    "connection.url"  = "jdbc:sqlite:test.db"
    "auto.create"     = "true"
  }
}
```

[1]: https://www.terraform.io
[2]: https://kafka.apache.org/documentation/#connect
[third-party-plugins]: https://www.terraform.io/docs/configuration/providers.html#third-party-plugins


## Build
```bash
go mod download
GOOS=linux GOARCH=amd64 go build -o terraform-provider-jira-linux main.go
GOOS=darwin GOARCH=amd64 go build -o terraform-provider-jira-macos main.go
```