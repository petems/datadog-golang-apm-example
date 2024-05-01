# Simple Go app

A basic Golang app for demoing Golang APM. It's a very simple app that runs several endpoints to trigger specific APM scenarios (errors, spans, tags, errors etc)

## Running 

You need DD_API_KEY set in your shell environment. 

On OSX, consider https://github.com/sorah/envchain (eg. `envchain datadog docker-compose up --build -d`)

```
$ docker-compose down
$ docker-compose build
$ docker-compose up -d
$ curl http://localhost:8000/
```

It'll be running on [http://localhost:8000/](http://localhost:8000/) 

Check that the APM traces are showing in your Datadog org: ![image](https://github.com/petems/datadog-golang-apm-example/assets/1064715/4a02d3e8-1bf6-4e1d-be7c-64eca5de225c)

You can then hit the endpoints listed below

## Endpoints

Endpoints are defined in the `main.go` file:
* `/`: this endpoints returns a hello world, and generate a trace with no custom instrumentation.
![image](https://user-images.githubusercontent.com/65819327/215073485-abb6f4c8-5e1f-4ae2-884f-e5369421c43f.png)

* `/add-tag`: here, using custom instrumentation, we add a tag to the active span.
![image](https://user-images.githubusercontent.com/65819327/215073532-c7d0fa02-5fa5-428b-b155-2e916beaef83.png)

* `/set-error`: here we add an error on the current span. The error is made trying to read a file that does not exist.
![image](https://user-images.githubusercontent.com/65819327/215073546-6489b92a-360a-4f74-a04d-9feacef39ac6.png)

* `/add-span`: we add a child span to the current one, using context, and then we add a new child with `ChildOf`.
![image](https://user-images.githubusercontent.com/65819327/215073566-552bda15-4000-48a2-8708-00aad4a8209a.png)


## Tear down

Run `docker-compose down`
