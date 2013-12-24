---
layout: post
title: Introduction to Server-side Technologies
tagline: ... from the early 2000s
date: 2004-10-04 23:10:00+00:00
tags: [web, server-side, cgi, java, servlet, jsp, http, ssi]
category: architecture
comments: false
---
Server-side scripting refers to the dynamic generation of Web pages served up by the Web server, as opposed to "static" web pages in the server storage that are served up to the Web browser.  In other words, some part of the content sent in response to a HTTP request is determined on-the-fly by a program that executes on the server after the HTTP request has been received and generates content as a result of the execution.

<!-- more -->

##Detailed purpose and major uses of server-side scripting
1. Insertion of continuously changing content into a web page, for example - weather or stock quotes.  Also, any arbitrary logic can be used to determine certain content will be shown or not.  This purpose and (10) below are the primary purposes of server-side scripting.
2. Authentication, authorization and session tracking - although rudimentary authentication and authorization is supported by most Web servers, anything more than the "BASIC" http authentication and ACLs (access control lists) over static resources requires server-side programs.  Similarly, handling cookies and keeping information about the session and/or the user is best handled by server-side scripting.
3. Template-driven page generation.  Including repeated content like header/footers and navigation menus around the "content area" of a web page.
4. Personalization and customization of content based on authentication and authorization defined above in (2).  This also includes the serving of content based on the content of the page (e.g. ads) or the browsing behavior of the user.
5. Dynamic image generation, e.g. page counters, human-readable characters for security, maps, overlays etc.
6. Dynamic generation of CSS and Javascript.
7. Generating and reading HTTP headers.  Although web servers provide rudimentary abilities, server-side scripting can best generate cache control and other complex headers.
8. Handling POST form input - accepting the input of a form and writing it to storage (file system, database, session etc.).  This also includes business transaction commitment control (ALL or NONE)  and input error handling.
9. Device mapping - generating different types of content (HTML, XML, WML) based on the user agent that sent the HTTP request.
10. Retrieval of data in response to query string parameters and insertion into a web page.  This is perhaps the most common purpose of utilizing scripting in generating content as part of a GET request.  e.g. sports statistics, staff list, downloadable files list etc.  The data can be retrieved from a database, file system or other forms of storage.
11. Communication with other programs, libraries and APIs - e.g. sending out e-mail, handling message queues, LDAP etc.
12. Re-use of persistent business objects.  HTTP is stateless, but the setup and tear-down of business objects has a very high overhead in terms of time and server resources. Server-side scripting allows us to interact with such re-usable business objects e.g. application servers, EJBs, .NET services and Web services.

##Popular server-side scripting languages - and examples
Before we look at popular server-side scripting languages, we will divide them into three groups based on how the scripting programs:
1. Older, standards-based scripting languages - these include SSI (server-side includes) and CGI (common gateway interface) and were defined in the original NCSA standards for web servers.
2. In-process scripting languages like PHP, ASP and Perl (sometimes).
3. Out-of-process scripting languages like JSP and servlets (Java) and XSLT.

Another classification is based on whether it is page-centric or script-centric.  A page-centric language is an HTML page with embedded special tags (SSI and all the \*SP languages) while script-centric are Perl and servlets.  Scripts in script-centric languages can produced multiple "pages" and have to output the entire HTML using program functions. 

Page-centric scripts are embedded into an HTML page only where dynamic content is required; but they can also be used to generate the entire content, e.g. images, XML, headers etc.  These usually run in-process and use the filesystem namespace of the web server.

### SSI (Server Side Includes)
[1](#references): These are extended comment tags inserted into a static HTML page to include other pages (templates), variables, and also execute external programs and include them in the input.  Any static HTML file defined with a special extension (commonly “.shtml”) forces a properly configured Web server to parse the file before sending and replace the special tags with the appropriate content.  This is perhaps the simplest model of server-side scripting but surprisingly, it is the essential mechanism of server-side scripting.
{% highlight html %}
<!--#set var="title" value="A Title" -->
<html><head><title><!--#echo var="title" --></title></head>
<body
<!--#include virtual="head" -->
<table>. . . . </table>
<!--#include virtual="foot" -->
</body>
</html>
{% endhighlight %}

###CGI (Common Gateway Interface) 
[2](#references): This is a mechanism that instructs a properly configured Web server to execute a specific file and send the output of the execution instead of sending it "as-is" to the client.  Any program (shell scripts, DOS batch files, C programs, Perl) can be executed through this mechanism.  Information about the request, the query string and any form parameters are sent as environment variables to the executed program.  Any output by the executed program is sent directly back to the browser.  It should be noted that the program is responsible for generating all headers.  The most commonly used language for CGI was Perl, due to its powerful text-handling capabilities.

{% highlight perl %}
$q = new CGI;
if (cgi_error()) {
  print "Content-type: text/plain\n\n";
  print "There was an error in your request!\n";
  print "Error is: ", cgi_error(), "\n";
  exit(1);
}

# print HTML headers
print $q->header, "\n";
print $q->start_html(-title => 'Your information request', -bgcolor => '#98B8D8'), "\n";
print $q->h1('Your information request'), "\n";

# print the HTML form
print $q->start_form(-method => 'POST'), "\n";
print "What's your name? ", "\n";
print $q->textfield(-name => 'yourname',
    -default => 'Your name here',
    -override => $override), "\n";
{% endhighlight %}

###Perl
[3](#references): This is an interpreted language characterised by its intuitive text handling, loose type-checking, associative arrays, handy loop constructs and simple file and environment handling.  It was the most popular server-side scripting language for many years and it supports a modular expansion system [4](#references).  A Perl script can be executed through the Perl Interpreter from the CGI interface (see above) or through a Web server extension that embeds the Perl Interpreter in the Web Server processes (in-process).  For example, see CGI above.  Its main drawback is that it pre-dates the Web and it is difficult to lay out HTML in the code.

###PHP (Hypertext Preprocessor)
[5](#references): I like to describe this as a cross between Perl, C++ and SSI.  This language was developed specifically for Web server-side scripting and its utility has made it one of the most popular server-side scripting languages.  As opposed to Perl, it is embedded into a fully laid out HTML page and gives complete control over HTTP request, response, cookie and session.  It contains more robust type-checking (if required) and can be programmed in an object-oriented way.  It is most commonly executed in-process and its biggest drawback is the lack of memory persistence of business objects.  Pages identified by certain extensions (commonly .phtml, .php, .php3) are parsed by the Web server and passed on to the PHP plugins that passes the content back to the Web server.  It follows the same directory structure as HTML static pages and images and is thus very easy to program and maintain.  It has an extensive library and API system and some third-party vendors (Zend etc.) offer accelerators for PHP that show considerable performance improvement for complex applications.
{% highlight php %}
<?php
  $title = "Sample PHP Script";
  $greeting = "Welcome to Sample PHP Script";
?>
<html>
  <head>
  <title><?php echo($title) ?></title>
</head>
<body>
  <h1><?php echo($title) ?></h1>
  <p><?php echo($greeting) ?></p>
  </body>
</html>
{% endhighlight %}

###ASP (Active Server Pages)
[6](#references): This is the Microsoft page-centric solution.  It only runs on the IIS (Internet Information Server) although third party implementations on other platforms are available, making it less proprietary than Cold Fusion below.  Like other page-centric languages, it embeds dynamic constructs into HTML pages:
{% highlight html %}
<html>
  <body>
  <%
    response.write("Hello World!")
  %>
  </body>
</html>
{% endhighlight %}

###Cold Fusion
[7](#references): This is a Macromedia page-centric solution.  However, instead of having ONE special tag to embed dynamic content, it defines a number of tags that are parsed by a Web server plugin in-process.  These special tags (in red below) make it very powerful and combined with Macromedia Web Authoring tools, make it the choice of many corporations.  However, it is proprietary:
{% highlight html %}
<cfquery name="customer" datasource="customer" username="abc" password="123" debug="yes">
  SELECT *  FROM custmast;
</cfquery>
<cfoutput query="cust">
  <tr>
    <td>#Customer_No#</td>
    <td>#name#</td>
    <td>#Street#</td>
  </tr>
</cfoutput>
</table>
{% endhighlight %}


###JSP/Servlets
[8](#references): This is standards-based, popular, hybrid and out-of-process -- based on Java and J2EE standards[9](#references) .  Although JSPs are page-centric at author-time, they are not parsed by a web server-plugin.  They are compiled into servlets and deployed in a separate Web Container.  The Web server communicates with the web container using sockets.  Most web containers implement a simple web server built into them which are usually not as robust and scalable as the leading Web servers but are good for testing and debugging.

Servlets are script-centric and are regular Java programs.  The compilation of JSPs into servlets gives us the best of both worlds (author-time page-centric and compiled out-of-process) and both of these have access to the full suite of Java libraries and APIs.  The web container also defines sophisticated authorisation, authentication and URL mapping techniques that make this an enterprise-level Web development platform.  Due to its being out of process, session objects and business objects can be cached and re-used by multiple HTTP requests.

Here is an example of the same code in servlet mode and JSP mode:
Servlet:
{% highlight java %}
  public void doGet (HttpServletRequest req, HttpServletResponse res)
    throws ServletException, IOException {
    String title = "Hello World Servlet";
    res.setContentType("text/html");
    ServletOutputStream out = res.getOutputStream();
    out.println("<html>");<br/>    out.println("<head><title>+title+</title></head>");
    out.println("<body>");<br/>    out.println("<h1>+title+</h1>");
    out.println("</body></html>");
  }

JSP:
<HTML>
  <HEAD>
    <% String title = "Hello World JSP"; %>
    <TITLE><%= title %></TITLE>
  </HEAD>
  <BODY>
    <H1><%= title %></H1>
  </BODY>
</HTML>
{% endhighlight %}

<a name="references">&nbsp;</a>
##References
1. [http://hoohoo.ncsa.uiuc.edu/docs/tutorials/includes.html](http://hoohoo.ncsa.uiuc.edu/docs/tutorials/includes.html)
2. [http://hoohoo.ncsa.uiuc.edu/cgi/](http://hoohoo.ncsa.uiuc.edu/cgi/)
3. [http://www.perl.org/](http://www.perl.org/)
4. [http://www.cpan.org/](http://www.cpan.org/)
5. [http://www.php.net/](http://www.php.net/)
6. [http://www.asp.net/](http://www.asp.net/)
7. [http://www.macromedia.com/go/gnavtray_cfmx_home](http://www.macromedia.com/go/gnavtray_cfmx_home)
8. [http://java.sun.com/products/jsp/](http://java.sun.com/products/jsp/)
9. [http://java.sun.com/j2ee/index.jsp](http://java.sun.com/j2ee/index.jsp)


