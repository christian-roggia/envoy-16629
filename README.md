# Envoy #16629

This repository is used to reproduce https://github.com/envoyproxy/envoy/issues/16629 locally.

## Launch docker-compose

```
docker-compose up
```

## Test with HTTP/1.1

```
curl http://127.0.0.1:8080/v1alpha1/foo/bar.git/git-upload-pack -H "Content-Type: text/plain" --data 'foobar'
```

Response:

```json
{
  "code": 13,
  "message": "internal",
  "details": []
}
```

## Test with HTTP/2

```
curl --http2-prior-knowledge http://127.0.0.1:8080/v1alpha1/foo/bar.git/git-upload-pack -H "Content-Type: text/plain" --data 'foobar'
```

Expected response (same as before):

```json
{
  "code": 13,
  "message": "internal",
  "details": []
}
```

Actual response:

```json
{
 "code": 2,
 "message": "EOF",
 "details": []
}
```


