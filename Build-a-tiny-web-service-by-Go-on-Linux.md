---
title: build-a-tiny-web-service-by-Go-on-Linux.md
tags:Go,Web,Service,Linux
grammar_cjkRuby: true
---

# Build a tiny web service by Go

## Objective

Build a web API by using Go language on Linux

## Setup Go
- Download
wget https://dl.google.com/go/go1.12.4.linux-amd64.tar.gz
tar -C /usr/local -xzf ./go1.12.4.linux-amd64.tar.gz

- Configure PATH
Add Go to PATH in ~/.bash_profile
``` bash
export PATH=$PATH:/usr/local/go/bin
```

- Source
```

Blockquote

> Blockquote

. ~/.bash_profile
```

- [Reference](https://golang.org/doc/install)

## Create a Go project
``` bash
mkdir -p /opt/ws/go/src/blue/http
cd /opt/ws/go/src/blue/http
vim BlueHTTPServer.go
```

``` golang
package main;

import (
	"net/http"
)

func say(res http.ResponseWriter, req *http.Request) {
	res.Write([]byte("Hey Bruce!"));
}

func main(){
	http.HandleFunc("/say", say);
	http.Handle("/say2", http.HandlerFunc(say));
	http.ListenAndServe(":10001", nil);
	select{};
}

```

## Build and run
``` bash
go build BlueHTTPServer.go
./BlueHTTPServer
```

## Test
``` bash
curl http://localhost:10001/say
curl http://localhost:10001/say2
```
I can see output like this: Hey Bruce!
