## Muhammad Haekal Kalipaksi

## 2206817490

## Reflections

### Number 1

_What are the key differences between unary, server streaming, and bi-directional streaming RPC (Remote Procedure Call) methods, and in what scenarios would each be most suitable?_

**Answer**

Unary:

In Unary RPC, client send a single request to server, and the server responses single response. Unary concept is almost simmilar what REST API do and suitible for task that only need one interaction between client and server. In this tutorial we use unary for payment request since client only send a payment request and server will resposne it.

Server streaming:

In Server streaming, client send a single request to server, and server send multiple response back to client. Server streaming can be use if server need to send multiple data to client over time, for the example in this tutorial we use server streaming for get payment history.

Bi-directional:

In Bi-directonal, client and server can send multiple request to each other. Bi-directonal can be use for task that need to interactive between client and server for the example in this tutorial bi-directional handle chat service.

### Number 2

_What are the potential security considerations involved in implementing a gRPC service in Rust, particularly regarding authentication, authorization, and data encryption?_

**Answer**

In the context of authentication, authorization, and data encyprtion using gRPC that there are several security consideration to make sure gRPC that implemented is secure, here several considerations:

- Use robust authentication and authorization methods. For every request received by the server, it must verify that the request is authorized.
- Use TLS for encryption to prevent man in the middles attack.
- Use end-to-end encryption to make sure the data that transmitted between server and client its encrypted.

### Number 3

_What are the potential challenges or issues that may arise when handling bidirectional streaming in Rust gRPC, especially in scenarios like chat applications?_

**Answer**

In my opinion the main potential challenges wheh handling bidirectional streaming in rust gRPC is concurency. Bidirectional streaming, especially in chat applications need robust concurrenncy in order to handle asyncrhonous messages sending, receiving in server and client. When using rust, i have to make sure the concurenncy that i implement have robust implementation. And for me, at this point as i know rust actually doesn't have standard libary for asynchrnous programming and relies to another library (in this tutorial is using tokio), so i think concunrency and async programming still be a challenge for me to implement bidirectonal streaming (or maybe skill issues :D)

### Number 4

_What are the advantages and disadvantages of using the tokio_stream::wrappers::ReceiverStream for streaming responses in Rust gRPC services?_

**Answer**

**Advantages**

- Provides a easy way to convert async receiver into stream.
- Integrates well with Rust's asynchronous ecosystem, making it easy to handle streaming responses.

**Disadvantages**

- Requires careful handling of concurrency and error propagation, as issues with the stream or receiver can lead to unexpected behavior.

### Number 5

_In what ways could the Rust gRPC code be structured to facilitate code reuse and modularity, promoting maintainability and extensibility over time?_

**Answer**

In my opinion the correct way gRPC code to be structured is using modularization, so every service will have own module which contain interface, impementation for both server and client. In both server and client main function, every implementaion will be called.

### Number 6

_In the MyPaymentService implementation, what additional steps might be necessary to handle more complex payment processing logic?_

**Answer**

In my opinion, additional steps that necessary is to handle the request is authorized, and make sure that the request have valid implementation.

### Number 7

_What impact does the adoption of gRPC as a communication protocol have on the overall architecture and design of distributed systems, particularly in terms of interoperability with other technologies and platforms?_

**Answer**

The adaption of gRPC as communication protocol have benefits especially for using protocol buffers which have strong typing and data consistency in server and client. And with using gRPC that relies on HTTP/2 communicity between system will be more efficient.

### Number 8

_What are the advantages and disadvantages of using HTTP/2, the underlying protocol for gRPC, compared to HTTP/1.1 or HTTP/1.1 with WebSocket for REST APIs?_

**Answer**

**Advantages**

- HTTP/2 support multiplexing, HTTP/2 allows multiple request and response send with single TCP connection.
- HTTP/2 support header compression make the request or response more smaller and efficient.

**Disadvanates**

- Not all harddware support HTTP/2.
- HTTP/2 doesn't support websocket for real time bideractional communication.

### Number 9

_How does the request-response model of REST APIs contrast with the bidirectional streaming capabilities of gRPC in terms of real-time communication and responsiveness?_

**Answer**

REST APIs release on syncrhonous process:

```
client -> send request -> server received -> server process -> server send response -> client received
```

The problem is for every single request there is only one request and one response. gRPC have capability of biderectional streaming using HTTP/2 protocol which support multiplexing. gRPC also support continously communication between server and client, so its asynchornous.

### Number 10

_What are the implications of the schema-based approach of gRPC, using Protocol Buffers, compared to the more flexible, schema-less nature of JSON in REST API payloads?_

**Answer**

The main implication of schema-based approach of gRPC is more complex implementation. As i know, schema-based approach will have strong typing which leads to have impelement multiple adapters to convert the request/response object to object that suitible for some use case.
