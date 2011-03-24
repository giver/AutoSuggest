AutoSuggest
===========
Copyright 2009-2010 Drew Wilson

[http://www.drewwilson.com](http://www.drewwilson.com)

[http://code.drewwilson.com/entry/autosuggest-jquery-plugin](http://code.drewwilson.com/entry/autosuggest-jquery-plugin)

**Version 1.4 - Updated: Mar. 23, 2010**

This Plug-In will auto-complete or auto-suggest completed search queries
for you as you type. You can add multiple selections and remove them on
the fly. It supports keybord navigation (UP + DOWN + RETURN), as well
as multiple AutoSuggest fields on the same page.

Inspied by the Autocomplete plugin by: J�rn Zaefferer
and the Facelist plugin by: Ian Tearle (iantearle.com)

This AutoSuggest jQuery plug-in is dual licensed under the MIT and GPL licenses:
[http://www.opensource.org/licenses/mit-license.php](http://www.opensource.org/licenses/mit-license.php)
[http://www.gnu.org/licenses/gpl.html](http://www.gnu.org/licenses/gpl.html)

Options
-------
* **asHtmlID**: string (false by default) - Enables you to specify your own custom ID that will be appended to the top level AutoSuggest UL element's ID name. Otherwise it will default to using a random ID. Example: id="CUSTOM_ID". This is also applies to the hidden input filed that holds all of the selected values. Example: id="as-values-CUSTOM_ID"
* **startText**: string ("Enter Name Here" by default) - Text to display when the AutoSuggest input field is empty.
* **emptyText**: string ("No Results" by default) - Text to display when their are no search results.
* **preFill**: object or string (empty object by default) - Enables you to pre-fill the AutoSuggest box with selections when the page is first loaded. You can pass in a comma separated list of values (a string), or an object. When using a string, each value is used as both the display text on the selected item and for it's value. When using an object, the options selectedItemProp will define the object property to use for the display text and selectedValuesProp will define the object property to use for the value for the selected item. Note: you must setup your preFill object in that format. A preFill object can look just like the example objects laid out above.
* **limitText**: string ("No More Selections Are Allowed" by default) - Text to display when the number of selections has reached it's limit.
* **selectedItemProp**: string ("value" by default) - Name of object property to use as the display text for each chosen item.
* **selectedValuesProp**: string ("value" by default) - Name of object property to use as the value for each chosen item. This value will be stored into the hidden input field.
* **searchObjProps**: string ("value" by default) - Comma separated list of object property names. The values in these objects properties will be used as the text to perform the search on.
* **queryParam**: string ("q" by default) - The name of the param that will hold the search string value in the AJAX request.
* **retrieveLimit**: number (false by default) - If set to a number, it will add a '&limit=' param to the AJAX request. It also limits the number of search results allowed to be displayed in the results dropdown box.
* **extraParams**: string ("" by default) - This will be added onto the end of the AJAX request URL. Make sure you add an '&' before each param.
* **matchCase**: true or false (false by default) - Make the search case sensitive when set to true.
* **minChars**: number (1 by default) - Minimum number of characters that must be entered into the AutoSuggest input field before the search begins.
* **keyDelay**: number (400 by default) - Number of milliseconds to delay after a keydown on the AutoSuggest input field and before search is started.
* **resultsHighlight**: true or false (true by default) - Option to choose whether or not to highlight the matched text in each result item.
* **neverSubmit**: true or false (false by default) - If set to true this option will never allow the 'return' key to submit the form that AutoSuggest is a part of.
* **selectionLimit**: number (false by default) - Limits the number of selections that are allowed to be made to the number specified.
* **showResultList**: true or false (true by default) - If set to false, the Results Dropdown List will never be shown at any time.
* **start:** callback function - Custom function that is run only once on each AutoSuggest field when the code is first applied.
* **selectionClick**: callback function - Custom function that is run when a previously chosen item is clicked. The item that is clicked is passed into this callback function as 'elem'.
      Example: selectionClick: function(elem){ elem.fadeTo("slow", 0.33); }
* **selectionAdded**: callback function - Custom function that is run when a selection is made by choosing one from the Results dropdown, or by using the tab/comma keys to add one. The selection item is passed into this callback function as 'elem'.
      Example: selectionAdded: function(elem){ elem.fadeTo("slow", 0.33); }
* **selectionRemoved**: callback function - Custom function that is run when a selection removed from the AutoSuggest by using the delete key or by clicking the "x" inside the selection. The selection item is passed into this callback function as 'elem'.
      <pre>Example: selectionRemoved: function(elem){ elem.fadeTo("fast", 0, function(){ elem.remove(); }); }</pre>
* **formatList**: callback function - Custom function that is run after all the data has been retrieved and before the results are put into the suggestion results list. This is here so you can modify what & how things show up in the suggestion results list.
* **beforeRetrieve**: callback function - Custom function that is run right before the AJAX request is made, or before the local objected is searched. This is used to modify the search string before it is processed. So if a user entered "jim" into the AutoSuggest box, you can call this function to prepend their query with "guy_". Making the final query = "guy_jim". The search query is passed into this function. Example: beforeRetrieve: function(string){ return string; }
* **retrieveComplete**: callback function - Custom function that is run after the ajax request has completed. The data object MUST be returned if this is used. Example: retrieveComplete: function(data){ return data; }
* **resultClick**: callback function - Custom function that is run when a search result item is clicked. The data from the item that is clicked is passed into this callback function as 'data'.
      <pre>Example: resultClick: function(data){ console.log(data); }</pre>
* **resultsComplete**: callback function - Custom function that is run when the suggestion results dropdown list is made visible. Will run after every search query.

The formatList option will hand you 2 objects:

* **data**: This is the data you originally passed into AutoSuggest (or retrieved via an AJAX request)
* **elem**: This is the HTML element you will be formatting (the 'result' li item).

In order to add extra things to the 'result' item (like an image) you will need to make sure you pass that data into AutoSuggest.
Below is an example of formatList in action: 

<pre>formatList: function(data, elem){
    var my_image = data.image;
    var new_elem = elem.html("add/change stuff here, put image here, etc.");
    return new_elem;
}</pre>