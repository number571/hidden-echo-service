# hidden-echo-service

Example of simple application in the «Hidden Lake» anonymity network. The configuration file of the production environment is used. 

### Download HLS

```bash
$ wget https://github.com/number571/hidden-lake/releases/latest/download/hlc_amd64_linux && \
    mv hlc_amd64_linux hlc && \
    chmod +x hlc && \
    cp hlc client/hlc
```

### Running

Terminal 1 (running echo-service):
```bash
$ go run ./main.go
```

Terminal 2 (running HLC service-node):
```bash
$ ./hlc
```

Terminal 3 (running HLC client-node):
```bash
$ cd client && ./hlc
```

### Request

Do request:
```bash
curl -i -X POST http://localhost:9532/api/network/request --data '{
    "receiver":"service-node",
    "req_data":{
        "method":"POST",
        "host":"hidden-echo-service",
        "path":"/echo",
        "body":"aGVsbG8sIHdvcmxkIQ=="
    }
}'
```

Get response:
```json
HTTP/1.1 200 OK
Content-Type: text/plain
Date: Sun, 04 Aug 2024 09:59:50 GMT
Content-Length: 102

{"code":200,"head":{"Content-Type":"text/plain; charset=utf-8"},"body":"ZWNobyhoZWxsbywgd29ybGQhKQ=="}
```

```bash
echo "ZWNobyhoZWxsbywgd29ybGQhKQ==" | base64 -d
# echo(hello, world!)
```
