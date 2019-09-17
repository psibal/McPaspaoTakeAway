McPaspao Take Away
==================

*Enable Docker 19.x experimental features*

Build
-----

```bash
docker buildx build --target=order-service -t paspaola/order-service:0.0.1 . &&\
docker buildx build --target=kitchen-service -t paspaola/kitchen-service:0.0.1 . &&\
docker buildx build --target=delivery-service -t paspaola/delivery-service:0.0.1 . &&\
docker buildx build --target=kong-mcpaspao -t paspaola/kong-mcpaspao:0.0.1 .
```

Run
---

    docker app render mcpaspao.dockerapp| docker-compose -f - up
    
Stop
----

    docker app render mcpaspao.dockerapp| docker-compose -f - down

Example
-------


    http://localhost:8090/swagger-ui.html
    
    

    curl -X POST "http://localhost:8080/kitchen/add?hamburgerType=KOBE&quantity=6" -H "accept: application/json"
    curl -X POST "http://localhost:8090/order/create" -H "accept: application/json" -H "Content-Type: application/json" -d "{ \"addressDTO\": { \"number\": \"string\", \"street\": \"string\" }, \"cookingType\": \"BLOOD\", \"hamburgerList\": [ { \"hamburgerType\": \"KOBE\", \"quantity\": 2 } ], \"price\": 10}"
    curl -X GET "http://localhost:8080/kitchen/status" -H "accept: application/json"
    
    curl -X GET "http://localhost:8001/kitchen-service/kitchen/status" -H "accept: application/json"
    curl -X POST "http://localhost:8001/kitchen-service/kitchen/add?hamburgerType=KOBE&quantity=6" -H "accept: application/json"
    curl -X POST "http://localhost:8001/order-service/order/create" -H "accept: application/json" -H "Content-Type: application/json" -d "{ \"addressDTO\": { \"number\": \"string\", \"street\": \"string\" }, \"cookingType\": \"BLOOD\", \"hamburgerList\": [ { \"hamburgerType\": \"KOBE\", \"quantity\": 2 } ], \"price\": 10}"