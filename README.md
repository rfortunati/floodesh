# floodesh
Floodesh is middleware based web spider written with Nodejs. "Floodesh" is a combination of two words, `flood` and `mesh`.

# Requirement

# Install
	
	$ npm install floodesh

# Useage
Before you use floodesh make sure you have [gearman](http://gearman.org/) server running 	on localhost

	$ mkdir floodesh_demo
	$ cd floodesh_demo
	$ floodesh --init

# Context
A context instance is a kind of [Finite-State Machine](https://en.wikipedia.org/wiki/Finite-state_machine) implemented by `Generators` which is [ECMAScript 6](http://es6-features.org/#GeneratorFunctionIteratorProtocol) feature. By context, we can access almost all fields in `response` and `request`, like:

```javascript
worker.responsemw.use( (ctx,next) => {
	ctx.content = ctx.body.toString();
	return next();
})
```

## Request

###ctx.is(types)
  *  `type`s String|Array
  *  Return: String|false|null

Check if the incoming request contains the "Content-Type" header field, and it contains any of the give mime `type`s.If there is no request body, `null` is returned.If there is no content type, `false` is returned.Otherwise, it returns the first `type` that matches.

###ctx.querystring()
  *  String

Get querystring.

###ctx.idempotent
  *  Boolean
  
Check if the request is idempotent.

###ctx.search
  *  String
  
Get the search string. It includes the leading "?" compare to querystring.

###ctx.method
  *  String
  
Get request method.

###ctx.query
  *  Object
  
Get parsed query-string.

###ctx.path
  *  String
  
Get the request pathname

###ctx.url
  *  String
  
Return request url, the same as __ctx.href__.

###ctx.origin
  *  String
  
Get the origin of URL, for instance, "https://www.google.com".

###ctx.protocol
  *  String
  
Return the protocol string "http" or "https"

###ctx.host
  * String, hostname:port
  
Parse the "Host" header field host and support X-Forwarded-Host when a proxy is enabled.

###ctx.hostname
  * String
  
Parse the "Host" header field hostname and support X-Forwarded-Host when a proxy is enabled.

###ctx.secure
  * Boolean
  
Check if protocol is https.

## Response

###ctx.status
  *  Number
  
Get status code from response.

###ctx.message
  *  String
  
Get status message from response.

###ctx.body
  *  Buffer
  
Get the response body in Buffer.

###ctx.length
  *  Number
  
Get length of response body.

###ctx.type
  *  String
  
Get the response mime type, for instance, "text/html"

###ctx.lastModifieds
  *  Date
  
Get the Last-Modified date in Date form, if it exists.

###ctx.etag
  *  String
  
Get the ETag of a response.

###ctx.header
  *  Object
  
Return the response header.

###ctx.href
  *  String

###ctx.uri
  *  String

###ctx.contentType
  *  String

###ctx.get(key)
  *  `key` String
  *  Return: String
  
Get value by key in response headers



First install Gearman

	wget https://launchpad.net/gearmand/1.2/1.1.12/+download/gearmand-1.1.12.tar.gz | tar zxf
	cd gearmand-1.1.12
	./configure
	make
	make install

You may first install `libboost-all-dev`, `gperf`, `libevent-dev`, `uuid-dev`
