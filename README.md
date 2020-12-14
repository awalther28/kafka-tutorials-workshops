# Kafka Tutorial Workshops

Code supporting meetup workshops based on [Kafka Tutorials](https://kafka-tutorials.confluent.io/).

##  Provision a new ccloud-stack on Confluent Cloud

This part assumes you have already set-up an account on [Confluent Cloud](https://confluent.cloud/) and you've installed the [Confluent Cloud CLI](https://docs.confluent.io/ccloud-cli/current/install.html). We're going to use the `ccloud-stack` utility to get everything set-up to work along with the workshop. 

Run (note this will take up to 12 minutes!):
```
git clone git@github.com:confluentinc/examples.git
cd examples/ccloud/ccloud-stack
./ccloud-stack.sh
# type 'y' for both questions
```
Once completed, you need to allow the ksqlDB app's service account access to create, read, and write to all topics.

1. Locate the ksqlDB application service account ID:

![ccloud-ksqlDBapp-settings-service-account-id](https://raw.githubusercontent.com/awalther28/kafka-tutorials-workshops/main/images/ksqlDBserviceAccount.jpg)

2. Run ```ccloud kafka acl create --allow --service-account <service-account-ID> --operation READ --operation WRITE --operation CREATE --topic '*'```

## Kafka-Tutorials on CCloud
Because we setup our Kafka cluster and ksqlDB application in CCloud, we will need to deviate from the instructions a little bit:

- Instead of using the ksqlDB cli, we can use the ksqlDB editor in CCloud
- Instead of using the kafka-console-producer, we can use `ccloud kafka topic produce <topic>`
- Use the "add properties" button in the ksqlDB editor to set the auto.offset.reset policy to 'earliest'
- Use "ksqlDB" and "Data Flow" section of the CCloud UI to see data 

### Working with nested JSON
Kafka-tutorial link: https://kafka-tutorials.confluent.io/working-with-nested-json/ksql.html#problem-description

### Working with hetergeneous JSON
Kafka-tutorial link: https://kafka-tutorials.confluent.io/working-with-json-different-structure/ksql.html#problem-description


##  Clean Up

If you haven't done so already, now is a good time to shut down all the resources we've created and started.  Because your Confluent Cloud cluster is using real cloud resources and is billable, delete the connector and clean up your Confluent Cloud environment when you complete this tutorial. You can use Confluent Cloud CLI or Confluent UI, but for this tutorial you can use the ccloud_library.sh library again. Pass in the `SERVICE_ACCOUNT_ID` that was generated when the `ccloud-stack` was created.

Run:

```
./ccloud_stack_destroy.sh stack-configs/<config file>
```

