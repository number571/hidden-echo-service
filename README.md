# hidden-echo-service

Example of simple application in the «Hidden Lake» anonymity network. The configuration file of the production environment is used. 

### Download HLS

```bash
wget https://github.com/number571/go-peer/releases/latest/download/hls_amd64_linux
mv hls_amd64_linux hls
chmod +x hls
cp hls client/hls
```

### Running

Terminal 1 (running echo-service):
```bash
go run ./main.go
```

Terminal 2 (running HLS service-node):
```bash
./hls
```

Terminal 3 (running HLS client-node):
```bash
cd client && ./hls
```

### Request

Do request:
```bash
curl -i -X POST http://localhost:9572/api/network/request --data '{
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
