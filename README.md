# go-load

A simple load testing tool using go.

⚠️  DISCLAIMER: This was originally forked from github.com/kshyju/go-load. Overstating? Yup.

## Usage

NOTE: This adaptation of Go-Load adds a dynamically generated `X-Request-Id` header with every request. This is to support min. level of distributed tracing.

### Prerequisites

Make sure you have installed[ go runtime in your machine](https://golang.org/dl/)

### Install go-load binary

Open a terminal/command prompt and run the below code which will install the go-load binary.

    go get github.com/kshyju/go-load

### Command line options

* -c : Specifies the number of concurrent connections(goroutines) to use. You can consider this as the RPS you want for the test. Ex: `-c=50` will send 50 requests/second.
* -d : Specifies the duration of the load test in seconds. Ex: `-d=30` will run the tests for 30 seconds.
* -h : Specifies the request headers to send in a comma-separated form. Each header item can use the `key:value` format. Ex: `my-apikey:foo,cookie:uid`
* -body : Specifies the path to the file name that has the request payload data present. go-load will read the content of this file and use that as the request body. When this option is passed, POST method will be used to send the request.
* -u : Specifies the request URL explicitly.

### Add a suffix signature to the request IDs used for the load

    go-load -c 10 -d 30 -sig hello_aliens https://www.bing.com

### Send 10 requests/sec to bing.com for 30 seconds

    go-load -c 10 -d 30 https://www.bing.com

If you have special characters like `&` in your URL, you need to pass the value in quotes.

    go-load -c 10 -d 30 "https://www.bing.com?how=are&you=today"

### Sending request headers

Request headers can be passed as a comma-separated string with the `-h` flag. The string should have a header key and value in the `key:value` format. Ex: `User-Agent:Go-http-client/1.1`

    go-load -c=10 -d=30 -h my-apikey:foo,cookie:uid:bar https://www.bing.com

The above example is sending 2 request headers, "my-apikey" and "cookie".

### Sending HTTP POST request with payload from a local file

    go-load -c=10 -d=30 -body="C:\\temp\\my-payload.json" "http://your.app/which/accepts/http-post?foo=bar"

## Upgrade/Remove

### Windows

To update to a newer version, you need to manually delete it in Windows.

Go to `%GOPATH%` (type `%GOPATH%` in Start and open the directory). Go to `src` and delete the `go-load` directory under `github`. I also deleted the `go-load.exe` in bin directory in `%GOPATH%`
