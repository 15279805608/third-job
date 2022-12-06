1. 通过 spring stream 访问 rabbit mq 与kafka【简单】

    a. 运行producer-service，运行前需指定消息中间件的类型，指定要连接binders中kafka或rabbitmq；

    rabbitmq

       spring.cloud.stream.binders.rabbit.type=rabbit
       spring.cloud.stream.bindings.newOrders.binder=rabbit
    kafka

       spring.cloud.stream.binders.kafka.type=kafka
       spring.cloud.stream.bindings.newOrders.binder=kafka

    b. 运行consumer-service，运行前需指定消息中间件的类型，指定要连接binders中kafka或rabbitmq，如上配置；

    c. 使用postman，调用http://localhost:8080/order/，创建订单

        POST /order/ HTTP/1.1
        Accept: application/json;charset=UTF-8
        Content-Type: application/json
        User-Agent: PostmanRuntime/7.29.2
        Cache-Control: no-cache
        Postman-Token: eeb1dd99-d31f-4cf3-a6aa-1b82eada26fe
        Host: localhost:8080
        Accept-Encoding: gzip, deflate, br
        Connection: keep-alive
        Content-Length: 56
     
        {
        "customer": "Li Lei",
        "items": [
        "mocha"
        ]
        }
     控制台可以看到发送消息的输出；

    d. 再调用http://localhost:8080/order/1，支付订单

        PUT /order/1 HTTP/1.1
        Content-Type: application/json
        User-Agent: PostmanRuntime/7.29.2
        Accept: */*
        Cache-Control: no-cache
        Postman-Token: 9354f252-3202-4cd4-a808-aabd5fe08d53
        Host: localhost:8080
        Accept-Encoding: gzip, deflate, br
        Connection: keep-alive
        Content-Length: 20

        {
        "state": "PAID"
        }
      控制台可以看到接收消息的并处理的输出。