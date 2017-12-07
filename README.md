

# Catalogue
A microservices-demo service that provides catalogue/product information.
This service is built, tested and released by travis.


### Setup instructions

```
sudo su
apt-get update && apt-get install -yq curl git wget
cd /tmp
wget -c https://storage.googleapis.com/golang/go1.8.1.linux-amd64.tar.gz
tar -xzf go1.8.1.linux-amd64.tar.gz -C /usr/local --strip-components=1
export GOPATH=/go
export GOROOT=/usr/local
which go
go version
mkdir -p /go/src/github.com/microservices-demo
cd /go/src/github.com/microservices-demo
git clone https://github.com/udbc/catalogue.git
cd catalogue/
go get -u github.com/FiloSottile/gvt
export PATH="/go/bin:$PATH"
which gvt
gvt restore
cd cmd/cataloguesvc/
CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo -o /app/main github.com/microservices-demo/catalogue/cmd/cataloguesvc

# Make sure you have mysql connection configurations done before launching the app
#echo "172.20.0.2 catalogue-db" >> /etc/hosts

/app/main -port 8081
```

### API Spec

Checkout the API Spec [here](http://microservices-demo.github.io/api/index?url=https://raw.githubusercontent.com/microservices-demo/catalogue/master/api-spec/catalogue.json)


### To build this service


### Check whether the service is alive
`curl http://localhost:8081/health`

### Use the service endpoints
`curl http://localhost:8081/catalogue`
