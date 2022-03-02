# Spring Cloud Stream Binder for AWS SNS

spring-cloud-stream-binder-sns lets you use [Spring Cloud Stream](https://spring.io/projects/spring-cloud-stream) with the AWS Simple Notification Service (SNS). Currently it only supports producing from your service to SNS, consuming will be added later.

## Installation

```xml
<dependencies>
    <dependency>
        <groupId>de.idealo.spring</groupId>
        <artifactId>spring-cloud-stream-binder-sns</artifactId>
        <version>1.0.3</version>
    </dependency>
</dependencies>
```

## Usage

With the library in your dependencies you can configure your Spring Cloud Stream bindings as usual. The type name for this binder is `sns`. There are no additional configuration options at the moment. The destination needs to match the topic name, the specific ARN will be looked up from the available topics in the account.

You may also provide additional configuration options:

- **Producers**
    - **sync** - Determines whether the message is sent synchronously. Default is false.

**Example Configuration:**

```yaml
spring:
  cloud:
    stream:
      sns:
        bindings:
          someFunction-out-0:
            consumer:
              sync: true
      bindings:
        someFunction-out-0:
          destination: topic-name
```

You may also provide your own beans of `AmazonSNSAsync` to override those that are created by [spring-cloud-aws-autoconfigure](https://github.com/spring-cloud/spring-cloud-aws/tree/master/spring-cloud-aws-autoconfigure).
