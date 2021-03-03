# SPA + RESTAPI + Mongo Website

Website consists Shared component (header,footer), SPA, REST API and Mongo DB

## Install website

```shell
kubectl create namespace websitecd-examples
kubectl apply -n websitecd-examples -f https://raw.githubusercontent.com/websitecd/websitecd-examples/main/websites/03-spa-restapi-mongo/deployment-preprodonly.yaml
```

### Local Live Development by Okteto

Install [okteto](https://okteto.com/docs/getting-started/installation).

#### Website

Start Dev container
```shell
cd websites/03-spa-restapi-mongo
okteto up --namespace websitecd-examples
```

Website is ready under `http://localhost:8080`.
Any change to all components are automatically synced to dev container.

#### REST API

Start Dev container
```shell
cd websites/03-spa-restapi-mongo/searchapi
kubectl apply -f k8s.yaml -n websitecd-examples
okteto up --namespace websitecd-examples
```
Now your terminal is attached to dev container and 
```shell
 ✓  Development container activated
 ✓  Connected to your development container
 ✓  Files synchronized
    Namespace: websitecd-examples
    Name:      searchapi-mongo
    Forward:   4000 -> 4000
               9229 -> 9229
               27017 -> mongodb:27017

Welcome to your development container. Happy coding!
websitecd-examples:searchapi-mongo app>
```

Now your terminal is your dev container in k8s.

```shell
npm install
nodemon index.js
```

Ports are forwarded to localhost and your API is under `4000` port and mongodb under `27017`.

To use api:
```shell
curl -X POST -H "Content-Type: application/json" http://localhost:4000/api/students -d '{"name":"Student 1" }'
curl http://localhost:4000/api/students
```

More info: [Okteto NodeJS Example](https://okteto.com/docs/samples/node).

## Delete website

```shell
kubectl delete -n websitecd-examples websites.websitecd.io advanced
```