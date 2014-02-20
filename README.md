jquery-plugin-query-object
==========================

Original docs http://www.jquery-plugins.info/query-string-object-00014864.htm

Query String Modification and Creation for jQuery

This extension creates a singleton query string object for quick and readable query 
string modification and creation. This plugin provides a simple way of taking a page's 
query string and creating a modified version of this with little code.

Example
-------------------------

```
var url = location.search;
> "?action=view&section=info&id=123&debug&testy[]=true&testy[]=false&testy[]"
var section = $.query.get('section');
> "info"
var id = $.query.get('id');
> 123
var debug = $.query.get('debug');
> true
var arr = $.query.get('testy');
> ["true", "false", true]
var arrayElement = $.query.get('testy[1]');
> "false"
var newUrl = $.query.set("section", 5).set("action", "do").toString();
> "?action=do&section=5&id=123"
var newQuery = "" + $.query.set('type', 'string');
> "?action=view&section=info&id=123&type=string"
var oldQuery = $.query.toString();
> "?action=view&section=info&id=123"
var oldQuery2 = $.query;
> ?action=view&section=info&id=123
var newerQuery = $.query.SET('type', 'string');
> ?action=view&section=info&id=123&type=string
var notOldQuery = $.query.toString();
> "?action=view&section=info&id=123&type=string"
var oldQueryAgain = $.query.REMOVE("type");
> ?action=view&section=info&id=123
var emptyQuery = $.query.empty();
> ""
var stillTheSame = $.query.copy();
> ?action=view&section=info&id=123
```

Features
-------------------------

 * **Chainability**  
    Like much of jQuery, this object supports chaining set methods to add new key 
    value pairs to the object. In addition, this chain does not modify the original 
    object, but returns a copy which can be modified without changing the original object. 
    You can use the method the 'loud' alternate methods to perform destructive 
    modifications on the original object.

 * **Direct Object 'get' Accessor**  
   The query string object returned contains the keys of the query string through a method named 'get'
   ```
   $.query.get(keypath)
   ```
 * **Easy String Creation**  
   All modern browsers convert JavaScript objects to their string representation through 
   their 'toString' method. So because this object creates a toString method for itself, 
   when evaluated in a string context, this object returns a valid query string. If the 
   query string object has no keys set, it returns an empty string. If it has keys set, 
   it automatically prefixes the output with a question mark so you don't need to worry 
   about appending one yourself. It's there if you need it and gone if you don't. 
   It also supports arrays and associative arrays inside the query string. Both regular 
   and associative arrays use "base[key1]=value1&base[key2]=value2" syntax in the query string.
   Originally arrays could forgo the square bracket and were simply printed out in their insertion 
   order but with the new deep object support in version 2.0 this had to be removed for the sake of 
   unambiguous keys.

 * **Custom url loading**  
   You can create a new query object based on a provided url through the load method

 * **Query String Parsing**  
   The original url parsing code was created by Jörn Zaefferer and modified by me.   
   The new parsing features added are:  
   1. **Parsing Integers**  
      The original code parsed floats out of strings but left integers as is. 
      In my release, '123' will be converted to the number 123.  
   2. **Boolean Values**  
      Query strings can often contain query parameters with no value set. This implies a simple boolean:  
      ```
      index.php?debug
      ```  
      implies a query string variable 'debug' set to true
   3. **Improved number parsing**
      Parsing features introduced in version 1.2 include better support for number formats and differentiating between number-looking strings and numbers.
   4. **Array syntax parsing**
      Array shaped query string keys will create an array in the internal jQuery.query structure and using square brackets without an index will generate an array dynamically.
   5. **Ampersand or semi-colon delimiters**
      Because it has been requested of me, the parser now supports both semi-colons and ampersands as delimiting marks between key value pairs.
   6. **Hash parameter parsing**
      Because it has been requested of me, the parser now supports both query string parsing and parsing of query string like strings in the url hash.

 
