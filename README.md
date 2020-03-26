- [Overview](#overview)
- [About me](#about-me)
- [Philosophy](#philosophy)
- [Frontend](#frontend)
  * [Web](#web)
  * [Apps](#apps)
  * [Backend for frontend (BFF)](#backend-for-frontend--bff-)
- [Backend](#backend)
  * [Shared common library](#shared-common-library)
  * [Logging](#logging)
  * [Serverless](#serverless)
    + [Pros](#pros)
    + [Cons](#cons)
- [Data](#data)
  * [Ownership](#ownership)
  * [Versioning](#versioning)
  * [Data persistence](#data-persistence)
  * [Retrieval](#retrieval)
    + [Pagination](#pagination)
  * [Data warehouse](#data-warehouse)
    + [Best practices](#best-practices)
- [Caching](#caching)
- [Tracing](#tracing)
- [Protocols and communication patterns](#protocols-and-communication-patterns)
  * [API definitions](#api-definitions)
  * [API design](#api-design)
- [Access control](#access-control)
  * [Multi tenancy](#multi-tenancy)
- [Testing](#testing)
  * [Principles](#principles)
  * [Load test](#load-test)
  * [Code hygiene](#code-hygiene)
- [Devops](#devops)
  * [Philosophy](#philosophy-1)
  * [CI/CD](#ci-cd)
  * [Deployment](#deployment)
  * [Monitoring](#monitoring)
- [Theories of computing](#theories-of-computing)
  * [Complexity of algorithms](#complexity-of-algorithms)
  * [Concurrency](#concurrency)
- [Data science and machine learning](#data-science-and-machine-learning)

# Overview

A checklist of tech considerations when designing fullstack architecture with [SRE](https://en.wikipedia.org/wiki/Site_Reliability_Engineering) in mind.

# About me
Since the list is heavily biased towards my tech background, here's a summary of it.

* Frontend: [Typescript](https://www.typescriptlang.org/), [React](https://reactjs.org/), [Vue](https://vuejs.org/), [Angular](https://angularjs.org/), [Jekyll](https://jekyllrb.com/)/[Hugo](https://gohugo.io/)/[Wordpress](https://wordpress.org/)
* Backend: [Go](https://golang.org/), [Java (SE 5 - 14)](https://www.java.com/en/download/), [Node.js](https://nodejs.org/en/), [Scala](https://www.scala-lang.org/)/[Akka](https://akka.io/), [Python 3](https://www.python.org/downloads/)/[Flask](https://github.com/pallets/flask)/[gunicorn](https://gunicorn.org/), [Haskell](https://www.haskell.org/), [C](https://en.wikipedia.org/wiki/C_(programming_language)), [Ruby](https://www.ruby-lang.org/en/)
* Scripting: [Bash](https://www.gnu.org/software/bash/), [Python 3](https://www.python.org/downloads/), [Perl](https://en.wikipedia.org/wiki/Perl)
* Cloud: [AWS](https://aws.amazon.com/) 90%, [GCP](https://cloud.google.com/) 10%
* Virtualisation: [VirtualBox](https://www.virtualbox.org/)/[vmware](https://www.vmware.com/uk.html), [docker](https://www.docker.com/), [kubernetes](https://kubernetes.io/)
* CI/CD: [Circle CI](https://circleci.com/), [GitHub Actions](https://github.com/marketplace?type=actions), [Concourse](https://concourse-ci.org/), [Airflow](https://airflow.apache.org/), [Jenkins](https://jenkins.io/)
* DB/Big data: [PostgreSQL](https://www.postgresql.org/)/[MySQL](https://www.mysql.com/)/[Aurora](https://aws.amazon.com/rds/aurora/)/[Oracle](https://www.oracle.com/uk/index.html), [Cassandra](https://en.wikipedia.org/wiki/Apache_Cassandra)/[DynamoDB](https://aws.amazon.com/dynamodb/), [MongoDB](https://www.mongodb.com/)/[Firebase](https://firebase.google.com/docs/firestore), [BigQuery](https://cloud.google.com/bigquery)/[Snowflake](https://www.snowflake.com/)/[Parquet (storage format)](https://en.wikipedia.org/wiki/Apache_Parquet)/[Spark+Streaming](https://spark.apache.org/streaming/), [Prometheus](https://prometheus.io/), [Neo4j](https://neo4j.com/)
* Middleware: [Kafka](https://en.wikipedia.org/wiki/Apache_Kafka)/[Kinesis](https://aws.amazon.com/kinesis/)/[SQS](https://aws.amazon.com/sqs/)/[RabbitMQ](https://www.rabbitmq.com/)/[PubSub](https://cloud.google.com/pubsub)/[ZeroMQ](https://zeromq.org/), [Redis](https://redis.io/), [Fluentd](https://www.fluentd.org/), [Apigee](https://cloud.google.com/apigee)/[Kong](https://konghq.com/kong/)/[Tyk](https://tyk.io/)/[KrakenD](https://www.krakend.io/), [Auth0](https://auth0.com/), [GraphQL](https://graphql.org/), [LaunchDarkly](https://launchdarkly.com/)
* Serverless: [AWS Lambda](https://aws.amazon.com/lambda/), [Cloud Function](https://cloud.google.com/functions), [Step Functions](https://aws.amazon.com/step-functions/)

# Philosophy

* [Convention over configuration](https://en.wikipedia.org/wiki/Convention_over_configuration)
* Consistency over creativity (i.e., least surprise)
* [Single source of truth (SSOT)](https://en.wikipedia.org/wiki/Single_source_of_truth)
* [Batteries included](https://www.python.org/dev/peps/pep-0206/)
* Full configurability, with a default setting that works 90% of time.
* [Configuration as code](https://rollout.io/blog/configuration-as-code-everything-need-know/)
* [Infrastructure as code](https://en.wikipedia.org/wiki/Infrastructure_as_code)
* [Docs as code](https://www.writethedocs.org/guide/docs-as-code/)
* [Automate yourself out of a job](https://medium.com/graham-gnall/how-to-automate-yourself-out-of-a-job-bdd650142c27)
* Driven by empathy, not ego (fancy features/algorithms never beat a good user experience)
* Centralisation isn't evil, chaos is
* [Simplicity is the ultimate sophistication](https://www.fastcompany.com/1790791/steve-jobs-biographer-apple-founder-was-driven-simplicity-mystical-thinking-and-occasional-l)
* [Exceptions are not exceptional](https://medium.com/continuousdelivery/exceptional-exceptions-5110671b3028), they're part of the system and part of the story
* Make choices based on problem, not on hype or "I like X"

# Frontend

## Web
* Language: [Typescript](https://www.typescriptlang.org/) + [ES6](https://www.w3schools.com/js/js_es6.asp).  Full stop.
* Frameworks: 
    * [Reace >= 0.14]() with [functional components](https://hackernoon.com/react-stateless-functional-components-nine-wins-you-might-have-overlooked-997b0d933dbc) 
    * Get started with [create-react-app](https://create-react-app.dev/docs/getting-started/)
    * [hooks](https://reactjs.org/docs/hooks-intro.html) and [context](https://reactjs.org/docs/context.html), and when it gets too difficult, [redux](https://blog.isquaredsoftware.com/2018/03/redux-not-dead-yet/)
    * [Jest](https://jestjs.io/) > [Mocha](https://mochajs.org/)
    * [TestCafe](https://github.com/DevExpress/testcafe) > [Cypress](https://www.cypress.io/) > [Selenium](https://www.selenium.dev/)
* Shared common library.  [bit.dev](https://bit.dev/) has good UI and doubles as a package repo.  [lerna](https://github.com/lerna/lerna) may be hard to use.
* [yarn](https://yarnpkg.com/) > [npm](https://www.npmjs.com/)
* [webpack](https://webpack.js.org/) for bundling
* [GraphQL](https://graphql.org/) for data querying
* [axios](https://github.com/axios/axios) for HTTP requests
* [Single sign-on (SSO)](https://en.wikipedia.org/wiki/Single_sign-on)
* [Progressive web apps (PWA)](https://en.wikipedia.org/wiki/Progressive_web_application)
* [Deep linking](https://en.wikipedia.org/wiki/Deep_linking): a page can be addressed and shared by a link

## Apps

* [ReactNative](https://reactnative.dev/)
* [Flutter](https://flutter.dev/)
* Native language (Java or Swift)

## Backend for frontend (BFF)

One BFF per frontend app.

Usages:
* Resource intensive tasks
* Complex query/aggregation 
* Protecting FE from unstable API changes
* [OAuth 2 authorization code flow](https://auth0.com/docs/flows/concepts/auth-code)
* Special protocol (e.g., websocket)

# Backend

* Follow [the 12 factor app](https://12factor.net/)
* [SOLID](https://en.wikipedia.org/wiki/SOLID)
* Coordination with [leader election](https://en.wikipedia.org/wiki/Leader_election)

## Shared common library

The philosophy is to abstract common functionality into a shared layer for better governance and easier upgrades.

* Middleware
* Context: common fields across all request flows (e.g., trace ID, caller ID)
* Common data types (e.g., timestamp, currency, coordinates, country code, error codes)
* Authentication
* Configuration
* Cross service communication
    * Protocol abstraction: the underlying protocol used should be hidden from user.  This allows easier protocol updates (e.g., HTTP to gRPC)
    * Service discovery: services should be addressable by a name.
* Handlers base class (e.g., message handler, request handler)
* DAO base class
* Cache library
* Logging
* Metrics

## Logging

* [Structured logging](https://stackify.com/what-is-structured-logging-and-why-developers-need-it/): variables get their own fields, log messages are static strings
* What to log
    * Timestamp
    * Trace ID
    * Caller ID
    * Service
    * Environment
* When to log
    * Service starts.  Log configurations.
    * Service crashes
    * Assertions fail (a code path that should never happen)
    * Errors are handled
    * Log at least one message per happy path
* When not to log:
    * Error propagation without handling
    * Normal code flow
    * Duplicates

## Serverless

### Pros

* On demand (cost saving)
* No infrastructure 
* No single point of failure
* High scalability

### Cons

* Not suitable for long running tasks (due to timeout)
* Not suitable for resource intensive tasks
* Not suitable for programs with local persistence (e.g., memory cache)
* Reactive (i.e., requires external triggers to run), not suitable for pro-active tasks (e.g., periodic notification, heartbeating)
* Complex workflow with multiple functions needs careful orchestration (e.g., [step function](https://aws.amazon.com/step-functions/faqs/))
* Logs need different shipping mechanism (because you don't control the VM and cannot install log aggregation daemons)

# Data

## Ownership

* The owner should be the writer
* There should be only one writer to a data set (the moderator)
* The owner should provide libraries for reading the data.  The libraries should hide the low level details of how data is retrieved (e.g., directly from DB, or via the owner). 

## Versioning

* Data should have created and updated timestamps
* If multiple data versions can co-exist, several strategies:
    * New table: good for isolation, bad for management (especially if tables are created by CD pipeline)
    * A version column: good for management, bad for indexing and possible hot partition.
* If old version needs to be migrated to new version, consider a tool like [AWS Data Pipeline](https://aws.amazon.com/datapipeline/faqs/).

## Data persistence 

* [SQL](https://en.wikipedia.org/wiki/SQL)
    * Pros
        * Joint query is easy
        * Transaction is easy
    * Cons
        * Schema change is hard
        * Usually poor scalability
* [NoSQL](https://en.wikipedia.org/wiki/NoSQL)
    * Pros
        * Schema change is easy
        * Easy to scale
    * Cons
        * Can only query on indexes
        * No joining, making application code complex
        * Limited transaction support
        * Bad index design can result in [hot partitions](https://stackoverflow.com/questions/53631825/hot-partition-problem-in-dynamo-db-gone-with-the-new-on-demand-feature)

SQL DB usually scales computing and storage together, which can be wasteful.  An exception is [AWS Aurora](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/Aurora.Overview.html) which scales them independenly.

See [concurrency](#concurrency) for discussion on transaction and data consistency.

## Retrieval

When complex query (multi-fields, condition filter, pagination, sorting, etc) is needed, it's best to keep indexes in a search engine.

* [Elasticsearch](https://en.wikipedia.org/wiki/Elasticsearch): index search
* [Solr](https://lucene.apache.org/solr/): text search
* [Aloglia](https://www.algolia.com/): text search

### Pagination

* [Offset vs cursor](https://dev.to/jackmarchant/offset-and-cursor-pagination-explained-b89)

## Data warehouse

The data is usually structured, with repeated and nested fields (e.g., JSON, YAML).

The DW therefore needs to handle them correctly.  [Columnar storage](https://aws.amazon.com/nosql/columnar/) following [Google Dremel whitepaper](https://blog.twitter.com/engineering/en_us/a/2013/dremel-made-simple-with-parquet.html) is ideal (e.g., [Parquet](https://en.wikipedia.org/wiki/Apache_Parquet) format).

### Best practices

* Define schema with version for all data types, with validation rules
* Validate incoming data before storing
* Common schema fields:
    * Timestamp
    * Trace ID
    * Caller ID
    * Service
    * Environment
    * Dedupe ID
    * Is it test?  (without this, test and real data is mingled and it's painful to separate them later)

# Caching

* Cache eviction: prevent out of memory issue.  There is a number of [strategies](https://en.wikipedia.org/wiki/Cache_replacement_policies#Least_recently_used_(LRU)), with [LRU](https://en.wikipedia.org/wiki/Cache_replacement_policies#Least_recently_used_(LRU)) being the most popular.
* Cache invalidation
    * time-to-live (TTL)
    * Event driven invalidation

# Tracing

* Choices
    * [OpenTracing](https://opentracing.io/)
    * [Zipkin](https://logz.io/blog/zipkin-vs-jaeger/)(written in Scala)
    * [Jaeger](https://logz.io/blog/zipkin-vs-jaeger/)(written in Go)
    * [AWS X-Ray](https://aws.amazon.com/xray/faqs/)
* What tags to include with trace
    * environment
    * service 
    * API/endpoint invoked

# Protocols and communication patterns

## Types of communication
* Request-response
* [Long polling](https://en.wikipedia.org/wiki/Push_technology#Long_polling)
* [Websocket](https://en.wikipedia.org/wiki/WebSocket)
* [Task queue (aka. message queue)](https://taskqueues.com/)
* Broadcast

## API definitions

* [Protocol buffers (abv. protobuf)](https://en.wikipedia.org/wiki/Protocol_Buffers).  Usages:
    * [Remote procedure call (RPC)](https://en.wikipedia.org/wiki/Remote_procedure_call)
    * [Inter-process communication (IPC)](https://en.wikipedia.org/wiki/Inter-process_communication)
    * Message schema definition
* [OpenAPI (aka. Swagger)](https://swagger.io/docs/specification/about/)
* [Thrift](https://en.wikipedia.org/wiki/Apache_Thrift), less popular
* [Avro](https://en.wikipedia.org/wiki/Apache_Avro), less popular

SDKs for different languages can be generated from API definitions.

## API design

* Implement [API gateway](https://apigee.com/about/cp/api-gateway) to handle:
    * API routing
    * Protocol translation (e.g., REST to Protobuf)
    * Authentication
    * Logging/metrics
    * Usage auditing
* Limit the usage of [polymorphic](https://en.wikipedia.org/wiki/Polymorphism_(computer_science)) payload (if payload is different in structure, better to make it a different API)
* Error response is part of the design, not an after thought.
* Standardise and regulate the use of error codes.  Adhere to HTTP status code definitions.
* Treat HTTP 5xx status as system failures that require intervention (i.e., don't use them lightly).

## Failure and recovery

* [Circuit breaker](https://en.wikipedia.org/wiki/Circuit_breaker_design_pattern)
* [Exponential backoff](https://en.wikipedia.org/wiki/Exponential_backoff)
* [Rate limit](https://en.wikipedia.org/wiki/Rate_limiting)

# Access control

* [OAuth 2](https://oauth.net/2/) with [OpenID Connect](https://openid.net/connect/)
* [Role-based access control](https://en.wikipedia.org/wiki/Role-based_access_control)
* [JWT](https://en.wikipedia.org/wiki/JSON_Web_Token)

## Multi tenancy

This is relevant for SaaS systems, where multiple users/customers/partners share the same application and infrastructure but not data.

[Data segregation](https://docs.microsoft.com/en-us/azure/sql-database/saas-tenancy-app-design-patterns) is the most common technique used.

Infrastructure segration does not scale well.

# Testing

https://martinfowler.com/articles/practical-test-pyramid.html

## Principles

* Test the right thing, at the right level (API level > unit level > whole system level).  E.g., DAO (having more complexity presumably) deserves more testing than HTTP handlers.
* Aim for quality, not coverage.  E.g., 90% DAO test coverage with mocked DB isn't better than 70% with real DB.  
* Higher level tests should be more general, lower level tests should be more specific (e.g., cover edge cases)
* You can't cover everything in test, but you can make sure you know how to fix it when it breaks (e.g., with good monitoring/logging)
* Use [BDD style](https://en.wikipedia.org/wiki/Behavior-driven_development) (i.e., structure test as a [scenario](https://en.wikipedia.org/wiki/Behavior-driven_development#Behavioral_specifications)) but not BDD itself (i.e., don't do scenario-to-code translation)
* Make test data identifiable.  Test data should never intefere with real data.
* Not be afraid to run test in production.  This requires building application with testability in mind.

## Load test

* Scenario description
    * Number of users
    * Scenario of each user
    * Ramp up/cool down period
* Metrics
    * Response time
    * Throughput
    * Error rate
* Monitoring: make sure the load generator isn't stressed out, by monitoring its CPU/memory/network
* Scaling: runing multiple instances, and aggregate the logs.
* Tools
    * [Gatling](https://en.wikipedia.org/wiki/Gatling_(software)): open source, written in Scala, good report UI, own DSL
    * [JMeter](https://en.wikipedia.org/wiki/Apache_JMeter): open source, written in Java, hard to configure
    * [Locust](https://locust.io/): open source, written in Python
    * [NeoLoad](https://en.wikipedia.org/wiki/Apache_JMeter): commercial 
    * [BlazeMeter](https://www.blazemeter.com/load-testing/): commercial

## Code hygiene

* [Limit scope of variables](https://softwareengineering.stackexchange.com/questions/307346/why-is-it-good-programming-practice-to-limit-scope)
* Consistent naming
* Declare constants at top
* Always use a linter and integrate it into CI
* Encourage the use of IDEs
* [Reproducible builds](https://en.wikipedia.org/wiki/Reproducible_builds): Use a package manager that can lock dependency versions

# Devops

## Philosophy

* [Aim for level 5 of CI maturity](https://www.infoq.com/articles/Continuous-Delivery-Maturity-Model/)
* [Configuration as code](https://rollout.io/blog/configuration-as-code-everything-need-know/)
* [Infrastructure as code](https://en.wikipedia.org/wiki/Infrastructure_as_code)
* No ad-hoc fixes
* [Immutable infrastructure](https://www.hashicorp.com/resources/what-is-mutable-vs-immutable-infrastructure) (no hot fixes)
* Developers should self-service
* Pager is the last line of escalation.  Use it sparingly.

## CI/CD

* [Circle CI](https://circleci.com/)
* [Travis CI](https://travis-ci.org/)
* [GitHub Actions](https://github.com/features/actions)
* [Concourse CI](https://concourse-ci.org/): ususally as a deployment pipeline instead of code builder
* [Jenkins](https://jenkins.io/)
* [Bamboo](https://www.atlassian.com/software/bamboo): commercial

## Deployment

* Deploy from master (never branches)
* [Canary release](https://martinfowler.com/bliki/CanaryRelease.html)
* [Blue/green deployment](https://blog.christianposta.com/deploy/blue-green-deployments-a-b-testing-and-canary-releases/)
* Acceptance test on the full platform

## Monitoring

* Healthcheck endpoints for long running services
* [Tracing](#tracing)
* Service dependency graph based on traffic and healthcheck.  This makes service grade/decommission safer
* Service metrics and dashboard

# Theories of computing

## Complexity of algorithms

* [Big O notation](https://en.wikipedia.org/wiki/Big_O_notation) for both time and space complexity
* [Cyclomatic complexity](https://en.wikipedia.org/wiki/Cyclomatic_complexity): how many logical path a function has

## Concurrency

* Models of concurrency
    * [Thread](https://en.wikipedia.org/wiki/Thread_(computing))
        * [Locks, mutex, semaphor](https://stackoverflow.com/questions/2332765/lock-mutex-semaphore-whats-the-difference)
    * [Event loop](https://en.wikipedia.org/wiki/Event_loop) + [Asynchronous IO](https://en.wikipedia.org/wiki/Asynchronous_I/O)
    * [Message passing](https://en.wikipedia.org/wiki/Message_passing) and [CSP](https://en.wikipedia.org/wiki/Communicating_sequential_processes) (including [actor systems](https://en.wikipedia.org/wiki/Actor_model))
* Common errors
    * [Deadlock](https://en.wikipedia.org/wiki/Deadlock)
    * [Race condition](https://en.wikipedia.org/wiki/Race_condition#Software)
* Distributed systems
    * [Concensus algorithms](https://en.wikipedia.org/wiki/Consensus_algorithm): [Paxos](https://en.wikipedia.org/wiki/Paxos_(computer_science)), [Raft](https://en.wikipedia.org/wiki/Raft_(computer_science))
    * [Eventual consistency](https://en.wikipedia.org/wiki/Eventual_consistency)
        * [Gossip protocol](https://en.wikipedia.org/wiki/Gossip_protocol)
        * [BASE](https://en.wikipedia.org/wiki/Eventual_consistency)
        * **Warning** not suitable for systems requiring [ACID](https://en.wikipedia.org/wiki/ACID), e.g., bank account transfer.
    * [Leader election](https://en.wikipedia.org/wiki/Leader_election)
    * [Sharding](https://en.wikipedia.org/wiki/Shard_(database_architecture))
    * [CAP theorem](https://en.wikipedia.org/wiki/CAP_theorem)

# Data science and machine learning

TBC