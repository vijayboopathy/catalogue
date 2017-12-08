

# Catalogue
A microservices-demo service that provides catalogue/product information.
This service is built, tested and released by travis.


### Setup instructions

```
sudo su
apt-get update && apt-get install -yq curl git wget
cd /tmp

echo "I: Setting up path for go and gvt"
export GOPATH=/opt/go
export GOROOT=/usr/local/go
export PATH="/opt/go/bin:$PATH"

mkdir /opt/go

echo "I: Install go from source..."

wget -c https://storage.googleapis.com/golang/go1.8.1.linux-amd64.tar.gz
tar -xzf go1.8.1.linux-amd64.tar.gz -C /usr/local


echo "Validating..."
which go
go version

echo "Install gvt..."
go get -u github.com/FiloSottile/gvt
which gvt

echo "I: Setup the repo..."
mkdir -p /opt/go/src/github.com/microservices-demo
cd /go/src/github.com/microservices-demo
git clone https://github.com/udbc/catalogue.git


echo "I: Compile the code ..."
cd catalogue/
cp -r images /images
gvt restore
cd cmd/cataloguesvc/
CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo -o /app/main github.com/microservices-demo/catalogue/cmd/cataloguesvc

echo "I: Launch the app...."
# Make sure you have mysql connection configurations done before launching the app
#echo "172.20.0.2 catalogue-db" >> /etc/hosts

/app/main -port 7081
```

### API Spec

Checkout the API Spec [here](http://microservices-demo.github.io/api/index?url=https://raw.githubusercontent.com/microservices-demo/catalogue/master/api-spec/catalogue.json)


### To build this service


### Check whether the service is alive
`curl http://localhost:8081/health`

### Use the service endpoints
`curl http://localhost:8081/catalogue`
