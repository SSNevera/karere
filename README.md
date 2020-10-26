# Overview
Karere is a message driven backend microservice framework for serverless applications. It uses a Pub/Sub service to invoke functions in a [choreography saga](https://microservices.io/patterns/data/saga.html). Clients connect to the framework via Websockets, allowing sagas to return data to the client multiple times throughout the saga.

## Error Reconciliation
In order to handle errors in parallel paths of a given saga, we suggest building an alternative error function along side all of your functions such that each function can handle their own side effects without needing an understanding of the greater saga. That being said, Karere is not opinionated on saga structures and you can implement your error reconciliation however you choose.

## Cloud Service Providers
Currently, Karere is built on top of AWS using SNS as the Pub/Sub service and API Gateway to maintain faux websocket connections with the client. DynamoDB is used for the caching of messages that were unable to be delivered and the creation of a pub/sub service that operates over API Gateway's websocket API (see more [here](https://www.npmjs.com/package/lambda-websocket-pubsub). Karere is ultimately abstracted from any individual service providers so any contributors are more than welcome to introduce alternative Cloud Service Providers in another branch.
