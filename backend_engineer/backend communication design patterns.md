## Request Response

## Sync / Async

## Push
Bidirectional connection.
Clients receive data from server without need of requests.
example like websocket

## Short polling

send the request and get back the request id
frequently checking for result (make request every amount of time to check for result)
## Long polling

send the request and get back the request id
block the request until the process is finish for return
## Server sent events

client send request, server send back multiple responses (multiple events as response)
header content type: "text/event-stream"
## Pub/Sub

one publisher - many readers
## Multiplexing vs Demultiplexing vs Connection pooling

## Stateless vs Stateful

Stateless: backend does not save the state of the client in the server. The client will transfer the state on every request
Stateful: store state about clients on the memory
## Sidecar Pattern