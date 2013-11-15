jquery-plugin-query-object
==========================

Query String Modification and Creation for jQuery

This extension creates a singleton query string object for quick and readable query 
string modification and creation. This plugin provides a simple way of taking a page's 
query string and creating a modified version of this with little code.

Usage:

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
