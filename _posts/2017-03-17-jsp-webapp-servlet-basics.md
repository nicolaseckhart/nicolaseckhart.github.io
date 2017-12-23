---
layout: post
title: "JSP Webapp Servlet Basics"
date: 2017-03-17 00:00:00 +0100
tags: jsp servlet java
author: nicolaseckhart
---

### web.xml

First you need to open `src/main/webapp/WEB-INF/web.xml` and add some lines to configure your new servlet.
We will call ours the HelloWorldServlet. The Servlet name can be whatever you want, but to make it easy we'll
just use the classes name with a small first letter.

In `servlet-class` you need to reference the actuall servlet class, which we'll create in a moment.
The `url-pattern` you need to specify the url path, where the servlet will be executed when visited.

```xml
<web-app>
...
  <servlet>
  	<servlet-name>helloWorldServlet</servlet-name>
  	<servlet-class>ch.zhaw.psit.budgetizer.servlets.HelloWorldServlet</servlet-class>
  </servlet>
  <servlet-mapping>
  	<servlet-name>helloWorldServlet</servlet-name>
  	<url-pattern>/helloWorld</url-pattern>
  </servlet-mapping>
...
</web-app>
```

### HelloWorldServlet.java

Now it's time to create the servlet itself. With the `@WebServlet` annotation you can specify the Servlets name, which usually
is the same as the class name.

If you want to respond to a HTTP GET request, then create a method called `doGet(..., ...)` as demonstrated in the example.
If you want to respond to a HTTP POST request, then create a `doPost(..., ...)` method. (There are links below for further
tutorials and context)

In our `doGet(..., ...)` all we do is to set a request attribute called message, which contains the string "Hello World".
Then on the second line we foreward the request and response objects to our view (our jsp file).

```java
package ch.zhaw.psit.budgetizer.servlets;

import java.io.IOException;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

@WebServlet(name = "HelloWorldServlet")
public class HelloWorldServlet extends HttpServlet {
	protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		request.setAttribute("message", "Hello World");
		getServletContext().getRequestDispatcher("/views/helloWorld.jsp").forward(request, response);
	}
}
```

### helloWorld.jsp

As you saw above, the servlet forwards to a page at `src/webapp/views/helloWorld.jsp`. Here is a simple implementation
of that page. In the heading tag you can see how we access the variable we've set in our servlet. There we can
now access our "Hello World" string and display it in the browser.

```html
<%@ page contentType="text/html; charset=UTF-8" %>
<!DOCTYPE html>
<html>
	<head>
		<title>HelloWorldServlet Test Page</title>
	</head>
	<body>
		<h1>${message}</h1>
	</body>
</html>
```

### Conclusion

Now, when you run your application on your local server, you can check out the servlets function at
http://localhost:8080/budgetizer/helloWorld just as specified in your web.xml:

![Image of Web App](http://i.imgur.com/IuF7HY9.png)

There is a ton of further information on servlets here: http://www.tutorialspoint.com/servlets/
