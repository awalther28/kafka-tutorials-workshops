# Kafka Tutorial Workshops

Code supporting meetup workshops based on [Kafka Tutorials](https://kafka-tutorials.confluent.io/).

##  Provision a new ccloud-stack on Confluent Cloud

This part assumes you have already set-up an account on [Confluent CLoud](https://confluent.cloud/) and you've installed the [Confluent Cloud CLI](https://docs.confluent.io/ccloud-cli/current/install.html). We're going to use the `ccloud-stack` utility to get everything set-up to work along with the workshop.  

Clone https://github.com/confluentinc/examples.

Run:
```
cd ccloud/ccloud-stack
./ccloud-stack.sh
# type 'y' for both questions
```

The `create` command generates a local config file, `java-service-account-NNNNN.config` when it completes. The `NNNNN` represents the service account id.  Take a quick look at the file:

```
cat stack-configs/java-service-account-*.config
```

You should see something like this:

```
# ENVIRONMENT ID: <ENVIRONMENT ID>
# SERVICE ACCOUNT ID: <SERVICE ACCOUNT ID>
# KAFKA CLUSTER ID: <KAFKA CLUSTER ID>
# SCHEMA REGISTRY CLUSTER ID: <SCHEMA REGISTRY CLUSTER ID>
# ------------------------------
ssl.endpoint.identification.algorithm=https
security.protocol=SASL_SSL
sasl.mechanism=PLAIN
bootstrap.servers=<BROKER ENDPOINT>
sasl.jaas.config=org.apache.kafka.common.security.plain.PlainLoginModule required username="<API KEY>" password="<API SECRET>";
basic.auth.credentials.source=USER_INFO
schema.registry.basic.auth.user.info=<SR API KEY>:<SR API SECRET>
schema.registry.url=https://<SR ENDPOINT>
```

## Working with nested JSON
Kafka-tutorial link: https://kafka-tutorials.confluent.io/working-with-nested-json/ksql.html#problem-description

Because we setup our Kafka cluster and ksqlDB application in CCloud, we will need to deviate from the instructions a little bit:

- Instead of using the ksqlDB cli, we can use the ksqlDB editor in CCloud
- Instead of using the kafka-console-producer, we can use `ccloud kafka topic produce financial_txns`
- Use teh "add properties" button in the ksqlDB editor to set the auto.offset.reset policy to 'earliest'
- Use "ksqlDB" and "Data Flow" section of the CCloud UI to see data 


## Working with hetergeneous JSON
Kafka-tutorial link: https://kafka-tutorials.confluent.io/working-with-nested-json/ksql.html#problem-description

Because we setup our Kafka cluster and ksqlDB application in CCloud, we will need to deviate from the instructions a little bit:

- Instead of using the ksqlDB cli, we can use the ksqlDB editor in CCloud
- Instead of using the kafka-console-producer, we can use `ccloud kafka topic produce source_data`
- Use teh "add properties" button in the ksqlDB editor to set the auto.offset.reset policy to 'earliest'
- Use "ksqlDB" and "Data Flow" section of the CCloud UI to see data 


##  Clean Up

If you haven't done so already, now is a good time to shut down all the resources we've created and started.  Because your Confluent Cloud cluster is using real cloud resources and is billable, delete the connector and clean up your Confluent Cloud environment when you complete this tutorial. You can use Confluent Cloud CLI or Confluent UI, but for this tutorial you can use the ccloud_library.sh library again. Pass in the `SERVICE_ACCOUNT_ID` that was generated when the `ccloud-stack was` created.

First clean up the `ccloud-stack`:

```
ccloud::destroy_ccloud_stack $SERVICE_ACCOUNT_ID
```

