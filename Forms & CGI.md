# Summary of CSS lecture from CSCI 571 
(refer:http://cs-server.usc.edu:45678/lectures.html)
# Form Tag
Syntax   
              <FORM>...</FORM>
## Attribute Specifications

* ACTION=URI (form handler)
* METHOD=[ get | post ] (HTTP method for submitting form)
   GET	is the default; form contents are appended to the URL
   POST	causes the fill-out form contents to be sent in a data body as standard input
* ENCTYPE=ContentType (content type to submit form as)
   Defaults to application/x-www-urlencoded which returns name/value pairs, separated by &, spaces replaced by + and reserved characters (like #) replaced by %HH, H a hex digit
* ACCEPT-CHARSET=Charsets (supported character encodings)
* TARGET=FrameTarget (frame to render form result in, in HTML4) 
(a browsing context name or keyword, in HTML5, such as`` _self, _blank, _parent, _top, iframename``)
* ONSUBMIT=Script (form was submitted)
* ONRESET=Script (form was reset)


## Input Tag

* TYPE:CHECKBOX，FILE，HIDDEN，IMAGE，PASSWORD，RADIO，RESET，SUBMIT，TEXT，COLOR，DATE，DATETIME，DATETIME-LOCAL，EMAIL，MONTH，NUMBER，
  RANGE，SEARCH，TEL，TIME，URL，WEEK
* NAME:		Name of data entry object whose value the user will supply
* VALUE:		Required for radio and checkboxes
* CHECKED:	For radio buttons and checkboxes
* SIZE:		Specific to each type of field
* MAXLENGTH:	Limit on accepted characters
* SRC:	Image file used as a graphical submit button when TYPE=IMAGE
* DISABLED	unavailable in this context
* READONLY	for text and passwords

## <TEXTAREA> Tag
> Attribute：
* NAME=name specifies a name for the data entry object to be sent to the server-side script
* COLS=num Width (in characters) of a text-entry region on the screen If user types more than COLS characters, field is scrolled
* ROWS=num same as the above


## SELECT> Tag

>Attributes:
* NAME=name
* SIZE=num Number of lines of the list to display at a time
* MULTIPLE Specifies that multiple list items may be selected (whereas normally only 1 item can be selected)

> HTML5 adds more attributes:
* AUTOFOCUS: drop-down list should automatically get focus
* FORM: defines one of more forms the select fields belongs to
* REQUIRED
> <Option> Tag
Use <option> tag to specify the start of a new menu item in the selection list
Syntax as follows:
<OPTION attributes> Text


## <FIELDSET> TAG
The content of a FIELDSET element must begin with a LEGEND to provide a caption for the group of controls. Following the LEGEND FIELDSET may contain any HTML element, including another FIELDSET
ACCESSKEY=I                    ALT + ACCESSKEY  快捷键


# CGI
## CGI invoke
CGI脚本是用下列两种方法使用的:
1、作为一个表单的ACTION
2、作为一个页中的直接link。

## 工作示意：
1、一个URL指向一个CGI脚本. 一个CGI脚本的URL能如普通的URL一样在任何地方出现。
2、服务器接收请求, 按照那个URL指向的脚本文件(注意文件的位置和扩展名),执行脚本。
3、脚本执行基于输入数据的操作，包括查询数据库、计算数值或调用系统中其他程序。脚本产生某种Web服务器能理解的输出结果。
4、服务器接收来自脚本的输出并且把它传回浏览器，让用户了解结果

Scripts can deliver information that is not directly readable by clients
The reason for the term “common gateway” is these programs act as gateways between the WWW and any other type of data or service

## environment variable
环境变量是在操作系统中一个具有特定名字的对象，它包含了一个或者多个应用程序所将使用到的信息。 例如Windows和DOS操作系统中的path环境变量，当要求系统运行一个程序而没有告诉它程序所在的完整路径时，系统除了在当前目录下面寻找此程序外，
还应到path中指定的路径去找。 用户通过设置环境变量，来更好的运行进程。
CGI environment variables are created by the web server and set immediately before the web server executes a gateway script，the CGI script can retrieve the values

## CGI variable
### 1. Non-request specific
SERVER_SOFTWARE, the name and version of the information server software answering the request
e.g. SERVER_SOFTWARE = Apache/1.3.15
SERVER_NAME, server’s hostname, DNS alias, or IP address
e.g. SERVER_NAME = nunki.usc.edu
GATEWAY_INTERFACE, the revision of the CGI specification with which this server complies
SERVER_PROTOCOL, the name and revision of the information protocol with which this request came in
e.g. SERVER_PROTOCOL = HTTP/1.0
SERVER_PORT, the port number to which the request was sent

### 2. Request specific
> These variables are set depending on each request
* REQUEST_METHOD, the method with which the request was made; e.g., (GET, POST)
* PATH_INFO, the extra path information as given by the client;
* PATH_TRANSLATED, the PATH_INFO path translated into an absolute document path on the local system
* PATH_TRANSLATED = /auto/home-scf-03/csci571/WebServer/apache_1.2.5/htdocs/extra/path
* SCRIPT_NAME, the path and name of the script being accessed as referenced in the URL
* SCRIPT_NAME = /cgi-bin/test.cgi
* QUERY_STRING, the information that follows the ? in the URL that referenced this script
* REMOTE_HOST, Internet domain name of the host making the request
* REMOTE_ADDR, the IP address of the remote host making the request
* AUTH_TYPE, the authentication method required to authenticate a user who wants access
* REMOTE_USER, user name that server and script have authenticated
* REMOTE_IDENT, the remote user name retrieved by the server using inetd identification (RFC 1413)
* CONTENT_TYPE, for queries that have attached information, such as POST method, this is the MIME content type of the data
* CONTENT_LENGTH, the length of the content as given by the client
> Also, every item of information in an HTTP request header is stored in an environment variable
 * Capitalize the name in the request header field
 * Convert dashes to underscores
 * Add the prefix HTTP_


> Output from a script to the server could be:
* A document generated by a script
* The type of document could be: HTML, plain text, image, video or audio clip, and many other types
* Instructions to the server for retrieving the desired output elsewhere
* an error indicator

## Server Directives：
The output of scripts begins with a small header consisting of text lines containing server directives
This must be followed by a blank line
Any headers that are not server directives are sent directly back to the client
Server directives are used by CGI scripts to inform the server about the type of output
The current CGI specification defines three server directives:
	* Content-type
	* Location
	* Status
  1. Content-type: type/subtype
The MIME type of the document being returned
For example,
content-type: text/html	(HTML document)

2. Location
Alerts the server that the script is returning a reference to a document, not an actual document
If the argument is a URL, the server will issue a redirect to the client; for example,
location: http://www.ncsa.uiuc.edu/
If the argument is a path, the document specified will be retrieved by the server, starting at the document root; for example,
location: /path/doc.txt

3.Status
This is used to give the server an HTTP/1.1 status line to send to the client
  E.g., 403 Forbidden
