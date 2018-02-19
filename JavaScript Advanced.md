
# Built-in Objects
JavaScript contains a set of built in objects related to the browser. Each object includes a set of properties and methods
## window object
1.Some properties of the Window object include:
* window.closed – a boolean indicating if the window is closed or not
* window.history – returns the history object
* window.location – returns the location object
* window.navigator – returns the navigator object
* Window.parent – returns the parent window of the current window
* Window.self – returns the current window
* Window.status – sets the text in the statusbar window
2.Some methods of the Window object include:
* open() – opens a new window
* blur () – removes focus from the current window
* close() – closes the current window
* focus() – sets the focus to the current window
* resizeBy () – resizes the window by the specified pixels


open() 方法用于打开一个新的浏览器窗口或查找一个已命名的窗口。

语法 ：window.open(URL,name,features,replace)
参数描述
URL	一个可选的字符串，声明了要在新窗口中显示的文档的 URL。如果省略了这个参数，或者它的值是空字符串，那么新窗口就不会显示任何文档。
name	一个可选的字符串，该字符串是一个由逗号分隔的特征列表，其中包括数字、字母和下划线，该字符声明了新窗口的名称。这个名称可以用作标记 <a> 和 <form> 的属性 target 的值。如果该参数指定了一个已经存在的窗口，那么 open() 方法就不再创建一个新窗口，而只是返回对指定窗口的引用。在这种情况下，features 将被忽略。
features	一个可选的字符串，声明了新窗口要显示的标准浏览器的特征。如果省略该参数，新窗口将具有所有标准特征。在窗口特征这个表格中，我们对该字符串的格式进行了详细的说明。
replace 一个可选的布尔值。规定了装载到窗口的 URL 是在窗口的浏览历史中创建一个新条目，还是替换浏览历史中的当前条目。支持下面的值：

true - URL 替换浏览历史中的当前条目。
false - URL 在浏览历史中创建新的条目


Three possible ways to invoke open window:
Triggered at page load time
<body onload="[open new window code];"> </body>
Triggered by clicking on a hyperlink
<a href="javascript:[open new window code]; void 0;">click me to open a new window!</a>
Triggered by clicking on a button
<input type="button" value="click me to open a new window" onclick="[open new window code];" />

## navigator object
navigator is a built-in object with properties that describe the browser
* navigator.appName is a string with the browser name
* navigator.appVersion is a string with the version number
to determine the correct version you may need to convert from string to number; parseFloat returns a number from a string, and ignores any part of the string after the number
* navigator.cookieEnabled determines whether cookies are enabled
* navigator.language returns the language of the browser
* navigator.userAgent returns the user-agent header sent by the browser


来自 navigator 对象的信息具有误导性，不应该被用于检测浏览器版本，这是因为：
navigator 数据可被浏览器使用者更改
浏览器无法报告晚于浏览器发布的新操作系统



One can refer to any name in a conditional and if it is undefined the conditional returns false
    newItem = something;

  produces an error if something is undefined

    if ( something ) { newItem = something; }

 does not produce an error, but only changes newItem if something exists

## document object
 Each HTML document loaded into a browser window becomes a Document object.
 The Document object provides access to all HTML elements in a page, from within a script
Some properties of the document object include:
* Document.anchors – returns a collection of all anchors in the document
* Document.applets – returns a collection of all applets in the document
* Document.body – returns the body element of the document
* Document.cookie – returns all name/value paris of cookies in the document
* Document.forms – returns a collection of all forms in the document
* Document.images – returns a collection of all the images in the document
* Document.lastModified – returns the date/time the document was last modified
Some methods of the document object include:
* Document.close() – closes the output stream previously opened
* Document.open() – opens an output stream to collect the output from document.write
* Document.write() – writes HTML expressions or JavaScript to a document


## The Location Object
A reference to the URL of the current document
Properties: hash, host, hostname, top, status, defaultStatus, window
No Methods and no Event Handlers
## history object
The history object contains the URLs visited by the user within a browser window
The history object is part of the window object

## Image object
To manipulate an image in JavaScript one can refer to it EITHER by its NAME attribute or by a built-in array of images that is automatically created by JavaScript, e.g.
document.images.name
document.images[index] where index is either a number or a string containing the name of the image


```html
<HTML><HEAD><TITLE>Using Multiple Selection Lists</TITLE>
<SCRIPT LANGUAGE="JavaScript">
function displaySelectionValues(objectName) { var ans = ""
	for (var i = 0; i < objectName.length; i++) {
		if(objectName.options[i].selected) {
			ans += objectName.options[i].text + "<BR>" } }
	myWin = window.open("", "Selections", "height=200,width=400")
	myWin.document.write("you picked these teams<BR>")
	myWin.document.write(ans) }
</SCRIPT></HEAD><BODY>
<FORM NAME="myform" method="POST">
<SELECT NAME="teams" size=3 multiple>
<OPTION value="dodgers">Dodgers<OPTION value="yankees">Yankees
<OPTION value="angels">Angels </SELECT><BR>
<INPUT TYPE="button" value="Show Selected Items"
onClick="displaySelectionValues(this.form.teams)">
</FORM></BODY></HTML>


<HTML><HEAD><TITLE>Using Selection Lists</TITLE>
<SCRIPT LANGUAGE="JavaScript">
function getSelectValue(selectObject) {
	return selectObject.options[selectObject.selectedIndex].value
	}
</SCRIPT></HEAD>
<BODY>
<FORM NAME=“myform” method=“POST”>没用，可删
<SELECT NAME="teams">
<OPTION value="dodgers">Dodgers
<OPTION value="yankees">Yankees
<OPTION value="angels">Angels
</SELECT><BR>
<INPUT TYPE="button" value="Show Selected Item "
onClick="alert(getSelectValue(this.form.teams))">
</FORM>
</BODY></HTML>
```

The addEventListener() method attaches an event handler to the specified element.

You can add event listeners to any DOM object not only HTML elements. i.e the window object


函数是第一类对象：函数和对象相同
Therefore functions can be treated as an object
assigned to new variables
stored in arrays
assigned to properties of objects
passed as arguments to functions


If func() is a function, and obj is an object,
		obj.method = func; assigns the function as an object method
To invoke the method, do
		obj.method()

|       | Copied by|	 Passed by|	Compared by|
|-------|----------|------------|------------|
numbers	|value		|value		|value|
boolean	|value		|value		|value|
string		immutable	immutable	value
object		reference	reference	reference
array		reference	reference	reference
function	reference	reference	reference

"One\ntwo".length // result = 7
（一个反斜杠不算）


# regular expressions
RegExp 对象的方法
RegExp 对象有 3 个方法：test()、exec() 以及 compile()。
test and exec are methods of object RegExp
exec executes a search for a match in a string; it returns an array
test tests for a match and returns true/false
Both exec and test set properties during execution
match and search are methods of String
match executes a search for a match in a string and returns an array or null
search tests for a match in a string and returns the index or -1
Uses exec method to locate a string
<script language=javascript1.2>
myRe = /d(b+)d/g;		//a d,1 or more b, and a d
myArray = myRe.exec("cdbbdbsbz");
</script>
An alternate approach
<script language=javascript1.2>
myArray = /d(b+)d/g.exec("cdbbdbsbz");
</script>
An alternate approach
<script language=javascript1.2>
myRe = new RegExp ("d(b+)d", g:);
myArray = myRe.exec("cdbbdbsbz");
</script>
