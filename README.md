# basic.http #

A basic HTTP client library built on top of HttpURLConnection.

## Usage examples ##

A simple GET request:

```java
HttpRequest request = HttpRequest().from(url).build();
HttpResponse response = HttpClient.execute(request);
```

A GET request with query parameters:

```java
HttpRequest request = HttpRequest
		.from(url)
		.using(Parameters.newInstance()
			.add("name", "value"))
		.build();
		
HttpResponse response = HttpClient.execute(request);
```

A POST request with parameters:

```java
HttpRequest request = HttpRequest
		.from(url)
		.using(Method.POST)
		.using(Parameters.newInstance()
			.add("name1", "value1")
			.add("name2", "value2"))
		.build();
		
HttpResponse response = HttpClient.execute(request);
```

A multipart POST request:

```java
HttpRequest request = HttpRequest
		.from(url)
		.using(Method.POST)
		.using(MultiPartRequestBody.newInstance()	
			.addBinaryPart("name", new File(path), MediaType.APPLICATION_OCTET_STREAM))
		.build();
		
HttpResponse response = HttpClient.execute(request);
```
A GET request with a ResponseHandler:

```java

HttpRequest request = HttpRequest
                .from(url)
                .using(Parameters.newInstance()
                        .add("name", "value"))
                .build();

HttpResponse response = HttpClient.execute(request);
String content = new BasicResponseHandler().handleResponse(response);
```

A POST request with JSON:

```java
String JSON = "...";

HttpRequest request = HttpRequest
        	.from(url)
        	.using(Method.POST)
        	.using(Header.newInstance()
                	.add(Header.Field.CONTENT_TYPE, MediaType.APPLICATION_JSON))
        	.using(RequestBody.newInstance()
                	.setContent(JSON))
        	.build();
		
HttpResponse response = HttpClient.execute(request);
```
